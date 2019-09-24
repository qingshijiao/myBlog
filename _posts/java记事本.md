---
title: java记事本

date: {{date}}
categories:
- 项目
tags:
- java
- 项目

---
# 题目
java实现记事本

# 题解

```
package NotePad;


import javax.swing.*;
import javax.swing.event.*;
import javax.swing.undo.CannotUndoException;
import javax.swing.undo.UndoManager;
import java.awt.*;
import java.awt.datatransfer.Clipboard;
import java.awt.datatransfer.DataFlavor;
import java.awt.datatransfer.StringSelection;
import java.awt.datatransfer.Transferable;
import java.awt.event.*;
import java.io.*;
import java.util.Calendar;
import java.util.Date;


/**
 * Demo class
 *
 * @author: Mr.Li
 * @date: 2019-09-15 15:05
 **/
public class NotePad extends JFrame implements ActionListener, DocumentListener {

    /**
     * 菜单
     */
    private JMenu fileMenu, editMenu, formatMenu, viewMenu, helpMenu;
    /**
     * 右键弹出菜单项
     */
    private JPopupMenu popupMenu;
    private JMenuItem popupMenuUndo, popupMenuCut, popupMenuCopy, popupMenuPaste, popupMenuDelete, popupMenuSelectAll;
    /**
     * “文件”的菜单项
     */
    private JMenuItem fileMenuNew, fileMenuOpen, fileMenuSave, fileMenuSaveAs, fileMenuPageSetUp, fileMenuPrint, fileMenuExit;
    /**
     * “编辑”的菜单项
     */
    private JMenuItem editMenuUndo, editMenuCut, editMenuCopy, editMenuPaste, editMenuDelete, editMenuFind, editMenuFindNext, editMenuReplace, editMenuGoTo, editMenuSelectAll, editMenuTimeDate;
    /**
     * “格式”的菜单项
     */
    private JCheckBoxMenuItem formatMenuLineWrap;
    private JMenuItem formatMenuFont;
    /**
     * “查看”的菜单项
     */
    private JCheckBoxMenuItem viewMenuStatus;
    /**
     * “帮助”的菜单项
     */
    private JMenuItem helpMenuHelpTopics, helpMenuAboutNotepad;
    /**
     * “文本”编辑区域
     */
    private JTextArea editArea;
    /**
     * 状态栏标签
     */
    private JLabel statusLabel;
    /**
     * 系统剪切板
     */
    private Toolkit toolkit = Toolkit.getDefaultToolkit();
    private Clipboard clipboard = toolkit.getSystemClipboard();
    /**
     * 创建撤销操作管理器（与撤销操作有关）
     */
    protected UndoManager undo = new UndoManager();
    protected UndoableEditListener undoHandler = new UndoHandler();

    /**其它变量*/
    /**
     * 存放编辑区原来的内容，用于比较文本是否有改动
     */
    private String oldValue;
    /**
     * 是否新文件（未保存过的）
     */
    private boolean isNewFile = true;
    /**
     * 当前文件
     */
    private File currentFile;

    /**
     * 构造函数开始
     */
    public NotePad() {
        super("Java记事本");
        //改变系统默认字体
        Font font = new Font("Dialog", Font.PLAIN, 12);
        java.util.Enumeration keys = UIManager.getDefaults().keys();
        while (keys.hasMoreElements()) {
            Object key = keys.nextElement();
            Object value = UIManager.get(key);
            if (value instanceof javax.swing.plaf.FontUIResource) {
                UIManager.put(key, font);
            }
        }

        //创建菜单条
        JMenuBar menuBar = new JMenuBar();

        //创建文件菜单及菜单项并注册事件监听
        fileMenu = new JMenu("文件(F)");
        //设置快捷键ALT + F
        fileMenu.setMnemonic('F');

        fileMenuNew = new JMenuItem("新建(N)");
        fileMenuNew.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_N, InputEvent.CTRL_DOWN_MASK));
        fileMenuNew.addActionListener(this);

        fileMenuOpen = new JMenuItem("打开(O)...");
        fileMenuOpen.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_O, InputEvent.CTRL_DOWN_MASK));
        fileMenuOpen.addActionListener(this);

        fileMenuSave = new JMenuItem("保存(S)");
        fileMenuSave.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_S, InputEvent.CTRL_DOWN_MASK));
        fileMenuSave.addActionListener(this);

        fileMenuSaveAs = new JMenuItem("另存为(A)...");
        fileMenuSaveAs.addActionListener(this);

        fileMenuPageSetUp = new JMenuItem("页面设置(U)...");
        fileMenuPageSetUp.addActionListener(this);

        fileMenuPrint = new JMenuItem("打印(P)...");
        fileMenuPrint.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_P, InputEvent.CTRL_DOWN_MASK));
        fileMenuPrint.addActionListener(this);

        fileMenuExit = new JMenuItem("退出(X)");
        fileMenuExit.addActionListener(this);

        //创建编辑菜单及菜单项并注册事件监听
        editMenu = new JMenu("编辑(E)");
        //设置快捷键ALT + E
        editMenu.setMnemonic('E');
        //当选择编辑菜单时，设置剪切、复制、粘贴、删除等功能的可用性
        editMenu.addMenuListener(new MenuListener() {
            //选择某个菜单时调用
            @Override
            public void menuSelected(MenuEvent menuEvent) {
                //设置剪切、复制、粘贴、删除等功能的可用性
                checkMenuItemEnabled();
            }

            //取消选择某个菜单时调用
            @Override
            public void menuDeselected(MenuEvent menuEvent) {
                //设置剪切、复制、粘贴、删除等功能的可用性
                checkMenuItemEnabled();
            }

            //取消菜单时调用
            @Override
            public void menuCanceled(MenuEvent menuEvent) {
                //设置剪切、复制、粘贴、删除等功能的可用性
                checkMenuItemEnabled();
            }
        });

        editMenuUndo = new JMenuItem("撤回(U)");
        editMenuUndo.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_Z, InputEvent.CTRL_DOWN_MASK));
        editMenuUndo.addActionListener(this);
        editMenuUndo.setEnabled(false);

        editMenuCut = new JMenuItem("剪切(T)");
        editMenuCut.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_X, InputEvent.CTRL_DOWN_MASK));
        editMenuCut.addActionListener(this);

        editMenuCopy = new JMenuItem("复制(C)");
        editMenuCopy.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_C, InputEvent.CTRL_DOWN_MASK));
        editMenuCopy.addActionListener(this);

        editMenuPaste = new JMenuItem("粘贴(P)");
        editMenuPaste.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_V, InputEvent.CTRL_DOWN_MASK));
        editMenuPaste.addActionListener(this);

        editMenuDelete = new JMenuItem("删除(D)");
        editMenuDelete.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_DELETE, 0));
        editMenuDelete.addActionListener(this);

        editMenuFind = new JMenuItem("查找(F)...");
        editMenuFind.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_F, InputEvent.CTRL_DOWN_MASK));
        editMenuFind.addActionListener(this);

        editMenuFindNext = new JMenuItem("查找下一个(N)");
        editMenuFindNext.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_F3, 0));
        editMenuFindNext.addActionListener(this);

        editMenuReplace = new JMenuItem("替换(R)...", 'R');
        editMenuReplace.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_H, InputEvent.CTRL_DOWN_MASK));
        editMenuReplace.addActionListener(this);

        editMenuGoTo = new JMenuItem("转到(G)...", 'G');
        editMenuGoTo.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_G, InputEvent.CTRL_DOWN_MASK));
        editMenuGoTo.addActionListener(this);

        editMenuSelectAll = new JMenuItem("全选", 'A');
        editMenuSelectAll.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_A, InputEvent.CTRL_DOWN_MASK));
        editMenuSelectAll.addActionListener(this);

        editMenuTimeDate = new JMenuItem("时间/日期(D)", 'D');
        editMenuTimeDate.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_F5, 0));
        editMenuTimeDate.addActionListener(this);

        //创建格式菜单及菜单项并注册事件监听
        formatMenu = new JMenu("格式(O)");
        //设置快捷键ALT + O
        formatMenu.setMnemonic('O');

        formatMenuLineWrap = new JCheckBoxMenuItem("自动换行(W)");
        //设置快捷键ALT + W
        formatMenuLineWrap.setMnemonic('W');
        formatMenuLineWrap.setState(true);
        formatMenuLineWrap.addActionListener(this);

        formatMenuFont = new JMenuItem("字体(F)...");
        formatMenuFont.addActionListener(this);

        //创建查看菜单及菜单项并注册事件监听
        viewMenu = new JMenu("查看(V)");
        //设置快捷键ALT + V
        viewMenu.setMnemonic('V');

        viewMenuStatus = new JCheckBoxMenuItem("状态栏(S)");
        //设置快捷键ALT + S
        viewMenuStatus.setMnemonic('S');
        viewMenuStatus.setState(true);
        viewMenuStatus.addActionListener(this);

        //创建帮助菜单及菜单项并注册事件监听
        helpMenu = new JMenu("帮助(H)");
        //设置快捷键ALT + H
        helpMenu.setMnemonic('H');

        helpMenuHelpTopics = new JMenuItem("帮助主题(H)");
        helpMenuHelpTopics.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_F1, 0));
        helpMenuHelpTopics.addActionListener(this);

        helpMenuAboutNotepad = new JMenuItem("关于记事本(A)");
        helpMenuAboutNotepad.addActionListener(this);

        //向菜单条添加“文件”菜单及菜单项
        menuBar.add(fileMenu);
        fileMenu.add(fileMenuNew);
        fileMenu.add(fileMenuOpen);
        fileMenu.add(fileMenuSave);
        fileMenu.add(fileMenuSaveAs);
        //分隔线
        fileMenu.addSeparator();
        fileMenu.add(fileMenuPageSetUp);
        fileMenu.add(fileMenuPrint);
        //分隔线
        fileMenu.addSeparator();
        fileMenu.add(fileMenuExit);

        //向菜单条添加“编辑”菜单及菜单项
        menuBar.add(editMenu);
        editMenu.add(editMenuUndo);
        editMenu.addSeparator();
        editMenu.add(editMenuCut);
        editMenu.add(editMenuCopy);
        editMenu.add(editMenuPaste);
        editMenu.add(editMenuDelete);
        //分隔线
        editMenu.addSeparator();
        editMenu.add(editMenuFind);
        editMenu.add(editMenuFindNext);
        editMenu.add(editMenuReplace);
        editMenu.add(editMenuGoTo);
        //分隔线
        editMenu.addSeparator();
        editMenu.add(editMenuSelectAll);
        editMenu.add(editMenuTimeDate);

        //向菜单条添加"格式"菜单及菜单项
        menuBar.add(formatMenu);
        formatMenu.add(formatMenuLineWrap);
        formatMenu.add(formatMenuFont);

        //向菜单条添加"查看"菜单及菜单项
        menuBar.add(viewMenu);
        viewMenu.add(viewMenuStatus);

        //向菜单条添加"帮助"菜单及菜单项
        menuBar.add(helpMenu);
        helpMenu.add(helpMenuHelpTopics);
        helpMenu.addSeparator();
        helpMenu.add(helpMenuAboutNotepad);

        //向窗口添加菜单条
        this.setJMenuBar(menuBar);

        //创建文本编辑去并添加滚动条
        editArea = new JTextArea(20, 50);
        JScrollPane scrollPane = new JScrollPane(editArea);
        scrollPane.setVerticalScrollBarPolicy(JScrollPane.VERTICAL_SCROLLBAR_ALWAYS);
        //向窗口添加文本编辑区
        this.add(scrollPane, BorderLayout.CENTER);
        //设置单词在以行不足容纳时换行
        editArea.setWrapStyleWord(true);
        //设置文本编辑区自动换行默认为 true，即会“自动换行”
        editArea.setLineWrap(true);
//        //向窗口添加文本编辑区
//        this.add(editArea, BorderLayout.CENTER);
        //获取原文本编辑区的内容
        oldValue = editArea.getText();

        //编辑区注册事件监听（与撤销操作有关）
        editArea.getDocument().addUndoableEditListener(undoHandler);
        editArea.getDocument().addDocumentListener(this);

        //创建右键弹出菜单
        popupMenu = new JPopupMenu();
        popupMenuUndo = new JMenuItem("撤销(U)");
        popupMenuCut = new JMenuItem("剪切(T)");
        popupMenuCopy = new JMenuItem("复制(C)");
        popupMenuPaste = new JMenuItem("粘帖(P)");
        popupMenuDelete = new JMenuItem("删除(D)");
        popupMenuSelectAll = new JMenuItem("全选(A)");

        popupMenuUndo.setEnabled(false);

        //向右键菜单添加菜单项和分隔符
        popupMenu.add(popupMenuUndo);
        popupMenu.addSeparator();
        popupMenu.add(popupMenuCut);
        popupMenu.add(popupMenuCopy);
        popupMenu.add(popupMenuPaste);
        popupMenu.add(popupMenuDelete);
        popupMenu.addSeparator();
        popupMenu.add(popupMenuSelectAll);

        //文本编辑区注册右键菜单事件
        popupMenuUndo.addActionListener(this);
        popupMenuCut.addActionListener(this);
        popupMenuCopy.addActionListener(this);
        popupMenuPaste.addActionListener(this);
        popupMenuDelete.addActionListener(this);
        popupMenuSelectAll.addActionListener(this);

        //文本编辑区注册右键菜单事件
        editArea.addMouseListener(new MouseAdapter() {
            @Override
            public void mousePressed(MouseEvent e) {
                //返回此鼠标事件是否为该平台的弹出菜单触发事件
                if (e.isPopupTrigger()) {
                    //在组件调用者的坐标中的位置X, Y 显示弹出菜单
                    popupMenu.show(e.getComponent(), e.getX(), e.getY());
                }
                //设置剪切，复制，粘帖，删除等功能的可用性
                checkMenuItemEnabled();
                //编辑区获取焦点
                editArea.requestFocus();
            }

            @Override
            public void mouseReleased(MouseEvent e) {
                //返回此鼠标事件是否为该平台的弹出菜单触发事件
                if (e.isPopupTrigger()) {
                    //在组件调用者的坐标中的位置X, Y 显示弹出菜单
                    popupMenu.show(e.getComponent(), e.getX(), e.getY());
                }
                //设置剪切，复制，粘帖，删除等功能的可用性
                checkMenuItemEnabled();
                //编辑区获取焦点
                editArea.requestFocus();
            }
        });//文本编辑区注册右键菜单事件结束

        //创建和添加状态栏
        statusLabel = new JLabel("按 F1 获取帮助");
        //向窗口添加状态栏标签
        this.add(statusLabel, BorderLayout.SOUTH);

        //设置窗口在屏幕上的位置、大小和可见性
        this.setLocation(100, 100);
        this.setSize(650, 650);
        this.setVisible(true);
        //添加窗口监听器
        addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                exitWindowChoose();
            }
        });
        checkMenuItemEnabled();
        editArea.requestFocus();
    }//构造函数Notepad结束


    /**
     * 设置菜单项的可用性：剪切，复制，粘帖，删除功能
     */
    public void checkMenuItemEnabled() {
        String selectText = editArea.getSelectedText();
        if (selectText == null) {
            editMenuCut.setEnabled(false);
            popupMenuCut.setEnabled(false);
            editMenuCopy.setEnabled(false);
            popupMenuCopy.setEnabled(false);
            editMenuDelete.setEnabled(false);
            popupMenuDelete.setEnabled(false);
        } else {
            editMenuCut.setEnabled(true);
            popupMenuCut.setEnabled(true);
            editMenuCopy.setEnabled(true);
            popupMenuCopy.setEnabled(true);
            editMenuDelete.setEnabled(true);
            popupMenuDelete.setEnabled(true);
        }
        //粘贴功能可用性判断
        Transferable contents = clipboard.getContents(this);
        if (contents == null) {
            editMenuPaste.setEnabled(false);
            popupMenuPaste.setEnabled(false);
        } else {
            editMenuPaste.setEnabled(true);
            popupMenuPaste.setEnabled(true);
        }
    }//方法checkMenuItemEnabled()结束

    /**
     * 关闭窗口时调用
     */
    public void exitWindowChoose() {
        editArea.requestFocus();
        String currentValue = editArea.getText();
        if (currentValue.equals(oldValue)) {
            System.exit(0);
        } else {
            int exitChoose = JOptionPane.showConfirmDialog(this,
                    "您的文件尚未保存，是否保存？", "退出提示",
                    JOptionPane.YES_NO_CANCEL_OPTION);
            if (exitChoose == JOptionPane.YES_OPTION) {
                if (isNewFile) {
                    String str = null;
                    JFileChooser fileChooser = new JFileChooser();
                    fileChooser.setFileSelectionMode(JFileChooser.FILES_ONLY);
                    fileChooser.setApproveButtonText("确定");
                    fileChooser.setDialogTitle("另存为 ");

                    int result = fileChooser.showSaveDialog(this);
                    if (result == JFileChooser.CANCEL_OPTION) {
                        statusLabel.setText("您没有保存文件");
                        return;
                    }

                    File saveFileName = fileChooser.getSelectedFile();
                    if (saveFileName == null || saveFileName.getName().equals("")) {
                        JOptionPane.showMessageDialog(this,
                                "不合法的文件名", "不合法的文件名",
                                JOptionPane.ERROR_MESSAGE);
                    } else {
                        try {
                            FileWriter fw = new FileWriter(saveFileName);
                            BufferedWriter bfw = new BufferedWriter(fw);
                            bfw.write(editArea.getText(), 0, editArea.getText().length());
                            bfw.flush();
                            fw.close();

                            isNewFile = false;
                            currentFile = saveFileName;
                            oldValue = editArea.getText();

                            this.setTitle(saveFileName.getName() + "- 记事本");
                            statusLabel.setText("当前打开文件：" + saveFileName.getAbsoluteFile());
                            //isSave = true;
                        } catch (IOException e) {
                            e.printStackTrace();
                        }
                    }
                } else {
                    try {
                        FileWriter fw = new FileWriter(currentFile);
                        BufferedWriter bfw = new BufferedWriter(fw);
                        bfw.write(editArea.getText(), 0, editArea.getText().length());
                        bfw.flush();
                        fw.close();
                        //isSave = true;
                    } catch (IOException e) {
                        e.printStackTrace();
                    }
                }
                System.exit(0);
                //if(isSave)System.exit(0);
                //else return;
            } else {
                if (exitChoose == JOptionPane.NO_OPTION) {
                    System.exit(0);
                } else {
                    return;
                }
            }
        }
    }//关闭窗口时调用方法结束

    /**
     * 查找方法
     */
    public void find() {
        //false时允许其他窗口同时处于激活状态(即无模式)
        final JDialog findDialog = new JDialog(this, "查找", false);
        Container con = findDialog.getContentPane();
        con.setLayout(new FlowLayout(FlowLayout.LEFT));
        JLabel findContentLabel = new JLabel("查找内容(N)：");
        final JTextField findText = new JTextField(15);
        JButton findNextButton = new JButton("查找下一个(F)：");
        final JCheckBox matchCheckBox = new JCheckBox("区分大小写(C)");
        ButtonGroup bGroup = new ButtonGroup();
        final JRadioButton upButton = new JRadioButton("向上(U)");
        final JRadioButton downButton = new JRadioButton("向下(U)");
        downButton.setSelected(true);
        bGroup.add(upButton);
        bGroup.add(downButton);
        /*ButtonGroup此类用于为一组按钮创建一个多斥（multiple-exclusion）作用域。
		使用相同的 ButtonGroup 对象创建一组按钮意味着“开启”其中一个按钮时，将关闭组中的其他所有按钮。*/
		/*JRadioButton此类实现一个单选按钮，此按钮项可被选择或取消选择，并可为用户显示其状态。
		与 ButtonGroup 对象配合使用可创建一组按钮，一次只能选择其中的一个按钮。
		（创建一个 ButtonGroup 对象并用其 add 方法将 JRadioButton 对象包含在此组中。）*/
        JButton cancel = new JButton("取消");
        //取消按钮事件处理
        cancel.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent actionEvent) {
                findDialog.dispose();
            }
        });
        //"查找下一个"按钮监听
        findNextButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent actionEvent) {
                //"区分大小写(C)"的JCheckBox是否被选中
                int k = 0, m = 0;
                final String str1, str2, str3, str4, strA, strB;
                str1 = editArea.getText();
                str2 = findText.getText();
                str3 = str1.toUpperCase();
                str4 = str2.toUpperCase();
                //区分大小写
                if (matchCheckBox.isSelected()){
                    strA = str1;
                    strB = str2;
                } else {//不区分大小写,此时把所选内容全部化成大写(或小写)，以便于查找
                    strA = str3;
                    strB = str4;
                }
                if (upButton.isSelected()) {    //k=strA.lastIndexOf(strB,editArea.getCaretPosition()-1);
                    if (editArea.getSelectedText() == null) {
                        k = strA.lastIndexOf(strB, editArea.getCaretPosition() - 1);
                    } else {
                        k = strA.lastIndexOf(strB, editArea.getCaretPosition() - findText.getText().length() - 1);
                    }
                    if (k > -1) {    //String strData=strA.subString(k,strB.getText().length()+1);
                        editArea.setCaretPosition(k);
                        editArea.select(k, k + strB.length());
                    } else {
                        JOptionPane.showMessageDialog(null, "找不到您查找的内容！", "查找", JOptionPane.INFORMATION_MESSAGE);
                    }
                } else if (downButton.isSelected()) {
                    if (editArea.getSelectedText() == null) {
                        k = strA.indexOf(strB, editArea.getCaretPosition() + 1);
                    } else {
                        k = strA.indexOf(strB, editArea.getCaretPosition() - findText.getText().length() + 1);
                    }
                    if (k > -1) {    //String strData=strA.subString(k,strB.getText().length()+1);
                        editArea.setCaretPosition(k);
                        editArea.select(k, k + strB.length());
                    } else {
                        JOptionPane.showMessageDialog(null, "找不到您查找的内容！", "查找", JOptionPane.INFORMATION_MESSAGE);
                    }
                }
            }


        });//"查找下一个"按钮监听结束

        //创建"查找"对话框的界面
        JPanel panel1 = new JPanel();
        JPanel panel2 = new JPanel();
        JPanel panel3 = new JPanel();
        JPanel directionPanel = new JPanel();
        directionPanel.setBorder(BorderFactory.createTitledBorder("方向"));
        //设置directionPanel组件的边框;
        //BorderFactory.createTitledBorder(String title)创建一个新标题边框，使用默认边框（浮雕化）、默认文本位置（位于顶线上）、默认调整 (leading) 以及由当前外观确定的默认字体和文本颜色，并指定了标题文本。
        directionPanel.add(upButton);
        directionPanel.add(downButton);
        panel1.setLayout(new GridLayout(2, 1));
        panel1.add(findNextButton);
        panel1.add(cancel);
        panel2.add(findContentLabel);
        panel2.add(findText);
        panel2.add(panel1);
        panel3.add(matchCheckBox);
        panel3.add(directionPanel);
        con.add(panel2);
        con.add(panel3);
        findDialog.setSize(410, 180);
        //不可调整大小
        findDialog.setResizable(false);
        findDialog.setLocation(230, 280);
        findDialog.setVisible(true);
    }//查找方法结束

    /**
     * 替换方法
     */
    public void replace() {
        //false时允许其他窗口同时处于激活状态(即无模式)
        final JDialog replaceDialog = new JDialog(this, "替换", false);
        //返回此对话框的contentPane对象
        Container con = replaceDialog.getContentPane();
        con.setLayout(new FlowLayout(FlowLayout.CENTER));
        JLabel findContentLabel = new JLabel("查找内容(N)：");
        final JTextField findText = new JTextField(15);
        JButton findNextButton = new JButton("查找下一个(F):");
        JLabel replaceLabel = new JLabel("替换为(P)：");
        final JTextField replaceText = new JTextField(15);
        JButton replaceButton = new JButton("替换(R)");
        JButton replaceAllButton = new JButton("全部替换(A)");
        JButton cancel = new JButton("取消");
        cancel.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                replaceDialog.dispose();
            }
        });
        final JCheckBox matchCheckBox = new JCheckBox("区分大小写(C)");
        ButtonGroup bGroup = new ButtonGroup();
        final JRadioButton upButton = new JRadioButton("向上(U)");
        final JRadioButton downButton = new JRadioButton("向下(U)");
        downButton.setSelected(true);
        bGroup.add(upButton);
        bGroup.add(downButton);
     /*ButtonGroup此类用于为一组按钮创建一个多斥（multiple-exclusion）作用域。
     使用相同的 ButtonGroup 对象创建一组按钮意味着“开启”其中一个按钮时，将关闭组中的其他所有按钮。*/
     /*JRadioButton此类实现一个单选按钮，此按钮项可被选择或取消选择，并可为用户显示其状态。
     与 ButtonGroup 对象配合使用可创建一组按钮，一次只能选择其中的一个按钮。
     （创建一个 ButtonGroup 对象并用其 add 方法将 JRadioButton 对象包含在此组中。）*/

        //"查找下一个"按钮监听
        findNextButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                //"区分大小写(C)"的JCheckBox是否被选中
                int k = 0, m = 0;
                final String str1, str2, str3, str4, strA, strB;
                str1 = editArea.getText();
                str2 = findText.getText();
                str3 = str1.toUpperCase();
                str4 = str2.toUpperCase();
                //区分大小写
                if (matchCheckBox.isSelected()) {
                    strA = str1;
                    strB = str2;
                } else {    //不区分大小写,此时把所选内容全部化成大写(或小写)，以便于查找
                    strA = str3;
                    strB = str4;
                }
                if (upButton.isSelected()) {
                    //k=strA.lastIndexOf(strB,editArea.getCaretPosition()-1);
                    if (editArea.getSelectedText() == null) {
                        k = strA.lastIndexOf(strB, editArea.getCaretPosition() - 1);
                    } else {
                        k = strA.lastIndexOf(strB, editArea.getCaretPosition() - findText.getText().length() - 1);
                    }
                    if (k > -1) {
                        //String strData=strA.subString(k,strB.getText().length()+1);
                        editArea.setCaretPosition(k);
                        editArea.select(k, k + strB.length());
                    } else {
                        JOptionPane.showMessageDialog(null, "找不到您查找的内容！", "查找", JOptionPane.INFORMATION_MESSAGE);
                    }
                } else if (downButton.isSelected()) {
                    if (editArea.getSelectedText() == null) {
                        k = strA.indexOf(strB, editArea.getCaretPosition() + 1);
                    } else {
                        k = strA.indexOf(strB, editArea.getCaretPosition() - findText.getText().length() + 1);
                    }
                    if (k > -1) {    //String strData=strA.subString(k,strB.getText().length()+1);
                        editArea.setCaretPosition(k);
                        editArea.select(k, k + strB.length());
                    } else {
                        JOptionPane.showMessageDialog(null, "找不到您查找的内容！", "查找", JOptionPane.INFORMATION_MESSAGE);
                    }
                }
            }
        });//"查找下一个"按钮监听结束

        //"替换"按钮监听
        replaceButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                if (replaceText.getText().length() == 0 && editArea.getSelectedText() != null) {
                    editArea.replaceSelection("");
                }
                if (replaceText.getText().length() > 0 && editArea.getSelectedText() != null) {
                    editArea.replaceSelection(replaceText.getText());
                }
            }
        });//"替换"按钮监听结束

        //"全部替换"按钮监听
        replaceAllButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                editArea.setCaretPosition(0);    //将光标放到编辑区开头
                int k = 0, m = 0, replaceCount = 0;
                if (findText.getText().length() == 0) {
                    JOptionPane.showMessageDialog(replaceDialog, "请填写查找内容!", "提示", JOptionPane.WARNING_MESSAGE);
                    findText.requestFocus(true);
                    return;
                }
                while (k > -1)//当文本中有内容被选中时(k>-1被选中)进行替换，否则不进行while循环
                {    //"区分大小写(C)"的JCheckBox是否被选中
                    //int k=0,m=0;
                    final String str1, str2, str3, str4, strA, strB;
                    str1 = editArea.getText();
                    str2 = findText.getText();
                    str3 = str1.toUpperCase();
                    str4 = str2.toUpperCase();
                    if (matchCheckBox.isSelected())//区分大小写
                    {
                        strA = str1;
                        strB = str2;
                    } else//不区分大小写,此时把所选内容全部化成大写(或小写)，以便于查找
                    {
                        strA = str3;
                        strB = str4;
                    }
                    if (upButton.isSelected()) {    //k=strA.lastIndexOf(strB,editArea.getCaretPosition()-1);
                        if (editArea.getSelectedText() == null) {
                            k = strA.lastIndexOf(strB, editArea.getCaretPosition() - 1);
                        } else {
                            k = strA.lastIndexOf(strB, editArea.getCaretPosition() - findText.getText().length() - 1);
                        }
                        if (k > -1) {    //String strData=strA.subString(k,strB.getText().length()+1);
                            editArea.setCaretPosition(k);
                            editArea.select(k, k + strB.length());
                        } else {
                            if (replaceCount == 0) {
                                JOptionPane.showMessageDialog(replaceDialog, "找不到您查找的内容!", "记事本", JOptionPane.INFORMATION_MESSAGE);
                            } else {
                                JOptionPane.showMessageDialog(replaceDialog, "成功替换" + replaceCount + "个匹配内容!", "替换成功", JOptionPane.INFORMATION_MESSAGE);
                            }
                        }
                    } else if (downButton.isSelected()) {
                        if (editArea.getSelectedText() == null) {
                            k = strA.indexOf(strB, editArea.getCaretPosition() + 1);
                        } else {
                            k = strA.indexOf(strB, editArea.getCaretPosition() - findText.getText().length() + 1);
                        }
                        if (k > -1) {    //String strData=strA.subString(k,strB.getText().length()+1);
                            editArea.setCaretPosition(k);
                            editArea.select(k, k + strB.length());
                        } else {
                            if (replaceCount == 0) {
                                JOptionPane.showMessageDialog(replaceDialog, "找不到您查找的内容!", "记事本", JOptionPane.INFORMATION_MESSAGE);
                            } else {
                                JOptionPane.showMessageDialog(replaceDialog, "成功替换" + replaceCount + "个匹配内容!", "替换成功", JOptionPane.INFORMATION_MESSAGE);
                            }
                        }
                    }
                    if (replaceText.getText().length() == 0 && editArea.getSelectedText() != null) {
                        editArea.replaceSelection("");
                        replaceCount++;
                    }

                    if (replaceText.getText().length() > 0 && editArea.getSelectedText() != null) {
                        editArea.replaceSelection(replaceText.getText());
                        replaceCount++;
                    }
                }//while循环结束
            }
        });//"替换全部"方法结束

        //创建"替换"对话框的界面
        JPanel directionPanel = new JPanel();
        directionPanel.setBorder(BorderFactory.createTitledBorder("方向"));
        //设置directionPanel组件的边框;
        //BorderFactory.createTitledBorder(String title)创建一个新标题边框，使用默认边框（浮雕化）、默认文本位置（位于顶线上）、默认调整 (leading) 以及由当前外观确定的默认字体和文本颜色，并指定了标题文本。
        directionPanel.add(upButton);
        directionPanel.add(downButton);
        JPanel panel1 = new JPanel();
        JPanel panel2 = new JPanel();
        JPanel panel3 = new JPanel();
        JPanel panel4 = new JPanel();
        panel4.setLayout(new GridLayout(2, 1));
        panel1.add(findContentLabel);
        panel1.add(findText);
        panel1.add(findNextButton);
        panel4.add(replaceButton);
        panel4.add(replaceAllButton);
        panel2.add(replaceLabel);
        panel2.add(replaceText);
        panel2.add(panel4);
        panel3.add(matchCheckBox);
        panel3.add(directionPanel);
        panel3.add(cancel);
        con.add(panel1);
        con.add(panel2);
        con.add(panel3);
        replaceDialog.setSize(420, 220);
        replaceDialog.setResizable(false);//不可调整大小
        replaceDialog.setLocation(230, 280);
        replaceDialog.setVisible(true);
    }//"全部替换"按钮监听结束

    /**
     * "字体"方法
     */
    public void font() {
        final JDialog fontDialog = new JDialog(this, "字体设置", false);
        Container con = fontDialog.getContentPane();
        con.setLayout(new FlowLayout(FlowLayout.LEFT));
        JLabel fontLabel = new JLabel("字体(F)：");
        //构造一个Dimension，并将其初始化为指定宽度和高度
        fontLabel.setPreferredSize(new Dimension(100, 20));
        JLabel styleLabel = new JLabel("字形(Y)：");
        styleLabel.setPreferredSize(new Dimension(100, 20));
        JLabel sizeLabel = new JLabel("大小(S)：");
        sizeLabel.setPreferredSize(new Dimension(100, 20));
        final JLabel sample = new JLabel("秦艽的记事本-QinJiao's Notepad");
        //sample.setHorizontalAlignment(SwingConstants.CENTER);
        final JTextField fontText = new JTextField(9);
        fontText.setPreferredSize(new Dimension(200, 20));
        final JTextField styleText = new JTextField(8);
        styleText.setPreferredSize(new Dimension(200, 20));
        final int style[] = {Font.PLAIN, Font.BOLD, Font.ITALIC, Font.BOLD + Font.ITALIC};
        final JTextField sizeText = new JTextField(5);
        sizeText.setPreferredSize(new Dimension(200, 20));
        JButton okButton = new JButton("确定");
        JButton cancel = new JButton("取消");
        cancel.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                fontDialog.dispose();
            }
        });
        Font currentFont = editArea.getFont();
        fontText.setText(currentFont.getFontName());
        fontText.selectAll();
        //styleText.setText(currentFont.getStyle());
        //styleText.selectAll();
        if (currentFont.getStyle() == Font.PLAIN) {
            styleText.setText("常规");
        } else if (currentFont.getStyle() == Font.BOLD) {
            styleText.setText("粗体");
        } else if (currentFont.getStyle() == Font.ITALIC) {
            styleText.setText("斜体");
        } else if (currentFont.getStyle() == (Font.BOLD + Font.ITALIC)) {
            styleText.setText("粗斜体");
        }
        styleText.selectAll();
        String str = String.valueOf(currentFont.getSize());
        sizeText.setText(str);
        sizeText.selectAll();
        final JList fontList, styleList, sizeList;
        GraphicsEnvironment ge = GraphicsEnvironment.getLocalGraphicsEnvironment();
        final String fontName[] = ge.getAvailableFontFamilyNames();
        fontList = new JList(fontName);
        fontList.setFixedCellWidth(86);
        fontList.setFixedCellHeight(20);
        fontList.setSelectionMode(ListSelectionModel.SINGLE_SELECTION);
        final String fontStyle[] = {"常规", "粗体", "斜体", "粗斜体"};
        styleList = new JList(fontStyle);
        styleList.setFixedCellWidth(86);
        styleList.setFixedCellHeight(20);
        styleList.setSelectionMode(ListSelectionModel.SINGLE_SELECTION);
        if (currentFont.getStyle() == Font.PLAIN) {
            styleList.setSelectedIndex(0);
        } else if (currentFont.getStyle() == Font.BOLD) {
            styleList.setSelectedIndex(1);
        } else if (currentFont.getStyle() == Font.ITALIC) {
            styleList.setSelectedIndex(2);
        } else if (currentFont.getStyle() == (Font.BOLD + Font.ITALIC)) {
            styleList.setSelectedIndex(3);
        }
        final String fontSize[] = {"8", "9", "10", "11", "12", "14", "16", "18", "20", "22", "24", "26", "28", "36", "48", "72"};
        sizeList = new JList(fontSize);
        sizeList.setFixedCellWidth(43);
        sizeList.setFixedCellHeight(20);
        sizeList.setSelectionMode(ListSelectionModel.SINGLE_SELECTION);
        fontList.addListSelectionListener(new ListSelectionListener() {
            @Override
            public void valueChanged(ListSelectionEvent event) {
                fontText.setText(fontName[fontList.getSelectedIndex()]);
                fontText.selectAll();
                Font sampleFont1 = new Font(fontText.getText(), style[styleList.getSelectedIndex()], Integer.parseInt(sizeText.getText()));
                sample.setFont(sampleFont1);
            }
        });
        styleList.addListSelectionListener(new ListSelectionListener() {
            @Override
            public void valueChanged(ListSelectionEvent event) {
                int s = style[styleList.getSelectedIndex()];
                styleText.setText(fontStyle[s]);
                styleText.selectAll();
                Font sampleFont2 = new Font(fontText.getText(), style[styleList.getSelectedIndex()], Integer.parseInt(sizeText.getText()));
                sample.setFont(sampleFont2);
            }
        });
        sizeList.addListSelectionListener(new ListSelectionListener() {
            @Override
            public void valueChanged(ListSelectionEvent event) {
                sizeText.setText(fontSize[sizeList.getSelectedIndex()]);
                //sizeText.requestFocus();
                sizeText.selectAll();
                Font sampleFont3 = new Font(fontText.getText(), style[styleList.getSelectedIndex()], Integer.parseInt(sizeText.getText()));
                sample.setFont(sampleFont3);
            }
        });
        okButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                Font okFont = new Font(fontText.getText(), style[styleList.getSelectedIndex()], Integer.parseInt(sizeText.getText()));
                editArea.setFont(okFont);
                fontDialog.dispose();
            }
        });
        JPanel samplePanel = new JPanel();
        samplePanel.setBorder(BorderFactory.createTitledBorder("示例"));
        //samplePanel.setLayout(new FlowLayout(FlowLayout.CENTER));
        samplePanel.add(sample);
        JPanel panel1 = new JPanel();
        JPanel panel2 = new JPanel();
        JPanel panel3 = new JPanel();
        //JPanel panel4=new JPanel();
        //JPanel panel5=new JPanel();
        //panel1.add(fontLabel);
        //panel1.add(styleLabel);
        //panel1.add(sizeLabel);
        //panel2.add(fontText);
        //panel2.add(new JScrollPane(fontList));//JList不支持直接滚动，所以要让JList作为JScrollPane的视口视图
        //panel2.setLayout(new GridLayout(2,1));
        //panel3.add(styleText);
        //panel3.add(new JScrollPane(styleList));
        //panel3.setLayout(new GridLayout(2,1));
        //panel4.add(sizeText);
        //panel4.add(new JScrollPane(sizeText));
        //panel4.setLayout(new GridLayout(2,1));
        //panel5.add(okButton);
        //panel5.add(cancel);
        //con.add(panel1);
        //con.add(panel2);
        //con.add(panel3);
        //con.add(panel4);
        //con.add(panel5);
        panel2.add(fontText);
        panel2.add(styleText);
        panel2.add(sizeText);
        panel2.add(okButton);
        panel3.add(new JScrollPane(fontList));//JList不支持直接滚动，所以要让JList作为JScrollPane的视口视图
        panel3.add(new JScrollPane(styleList));
        panel3.add(new JScrollPane(sizeList));
        panel3.add(cancel);
        con.add(panel1);
        con.add(panel2);
        con.add(panel3);
        con.add(samplePanel);
        fontDialog.setSize(350, 340);
        fontDialog.setLocation(200, 200);
        fontDialog.setResizable(false);
        fontDialog.setVisible(true);
    }

    @Override
    public void actionPerformed(ActionEvent actionEvent) {
        //新建
        if (actionEvent.getSource() == fileMenuNew) {
            editArea.requestFocus();
            String currentValue = editArea.getText();
            boolean isTextChange = (currentValue.equals(oldValue)) ? false : true;
            if (isTextChange) {
                int saveChoose = JOptionPane.showConfirmDialog(this, "您的文件尚未保存，是否保存？", "提示", JOptionPane.YES_NO_CANCEL_OPTION);
                if (saveChoose == JOptionPane.YES_OPTION) {
                    String str = null;
                    JFileChooser fileChooser = new JFileChooser();
                    fileChooser.setFileSelectionMode(JFileChooser.FILES_ONLY);
                    //fileChooser.setApproveButtonText("确定");
                    fileChooser.setDialogTitle("另存为");
                    int result = fileChooser.showSaveDialog(this);
                    if (result == JFileChooser.CANCEL_OPTION) {
                        statusLabel.setText("您没有选择任何文件");
                        return;
                    }
                    File saveFileName = fileChooser.getSelectedFile();
                    if (saveFileName == null || saveFileName.getName().equals("")) {
                        JOptionPane.showMessageDialog(this, "不合法的文件名", "不合法的文件名", JOptionPane.ERROR_MESSAGE);
                    } else {
                        try {
                            FileWriter fw = new FileWriter(saveFileName);
                            BufferedWriter bfw = new BufferedWriter(fw);
                            bfw.write(editArea.getText(), 0, editArea.getText().length());
                            bfw.flush();//刷新该流的缓冲
                            bfw.close();
                            isNewFile = false;
                            currentFile = saveFileName;
                            oldValue = editArea.getText();
                            this.setTitle(saveFileName.getName() + " - 记事本");
                            statusLabel.setText("当前打开文件：" + saveFileName.getAbsoluteFile());
                        } catch (IOException ioException) {
                        }
                    }
                } else if (saveChoose == JOptionPane.NO_OPTION) {
                    editArea.replaceRange("", 0, editArea.getText().length());
                    statusLabel.setText(" 新建文件");
                    this.setTitle("无标题 - 记事本");
                    isNewFile = true;
                    undo.discardAllEdits();    //撤消所有的"撤消"操作
                    editMenuUndo.setEnabled(false);
                    oldValue = editArea.getText();
                } else if (saveChoose == JOptionPane.CANCEL_OPTION) {
                    return;
                }
            } else {
                editArea.replaceRange("", 0, editArea.getText().length());
                statusLabel.setText(" 新建文件");
                this.setTitle("无标题 - 记事本");
                isNewFile = true;
                undo.discardAllEdits();//撤消所有的"撤消"操作
                editMenuUndo.setEnabled(false);
                oldValue = editArea.getText();
            }
        }//新建结束
        //打开
        else if (actionEvent.getSource() == fileMenuOpen) {
            editArea.requestFocus();
            String currentValue = editArea.getText();
            boolean isTextChange = (currentValue.equals(oldValue)) ? false : true;
            if (isTextChange) {
                int saveChoose = JOptionPane.showConfirmDialog(this, "您的文件尚未保存，是否保存？", "提示", JOptionPane.YES_NO_CANCEL_OPTION);
                if (saveChoose == JOptionPane.YES_OPTION) {
                    String str = null;
                    JFileChooser fileChooser = new JFileChooser();
                    fileChooser.setFileSelectionMode(JFileChooser.FILES_ONLY);
                    //fileChooser.setApproveButtonText("确定");
                    fileChooser.setDialogTitle("另存为");
                    int result = fileChooser.showSaveDialog(this);
                    if (result == JFileChooser.CANCEL_OPTION) {
                        statusLabel.setText("您没有选择任何文件");
                        return;
                    }
                    File saveFileName = fileChooser.getSelectedFile();
                    if (saveFileName == null || saveFileName.getName().equals("")) {
                        JOptionPane.showMessageDialog(this, "不合法的文件名", "不合法的文件名", JOptionPane.ERROR_MESSAGE);
                    } else {
                        try {
                            FileWriter fw = new FileWriter(saveFileName);
                            BufferedWriter bfw = new BufferedWriter(fw);
                            bfw.write(editArea.getText(), 0, editArea.getText().length());
                            bfw.flush();//刷新该流的缓冲
                            bfw.close();
                            isNewFile = false;
                            currentFile = saveFileName;
                            oldValue = editArea.getText();
                            this.setTitle(saveFileName.getName() + " - 记事本");
                            statusLabel.setText("当前打开文件：" + saveFileName.getAbsoluteFile());
                        } catch (IOException ioException) {
                        }
                    }
                } else if (saveChoose == JOptionPane.NO_OPTION) {
                    String str = null;
                    JFileChooser fileChooser = new JFileChooser();
                    fileChooser.setFileSelectionMode(JFileChooser.FILES_ONLY);
                    //fileChooser.setApproveButtonText("确定");
                    fileChooser.setDialogTitle("打开文件");
                    int result = fileChooser.showOpenDialog(this);
                    if (result == JFileChooser.CANCEL_OPTION) {
                        statusLabel.setText("您没有选择任何文件");
                        return;
                    }
                    File fileName = fileChooser.getSelectedFile();
                    if (fileName == null || fileName.getName().equals("")) {
                        JOptionPane.showMessageDialog(this, "不合法的文件名", "不合法的文件名", JOptionPane.ERROR_MESSAGE);
                    } else {
                        try {
                            FileReader fr = new FileReader(fileName);
                            BufferedReader bfr = new BufferedReader(fr);
                            editArea.setText("");
                            while ((str = bfr.readLine()) != null) {
                                editArea.append(str);
                            }
                            this.setTitle(fileName.getName() + " - 记事本");
                            statusLabel.setText(" 当前打开文件：" + fileName.getAbsoluteFile());
                            fr.close();
                            isNewFile = false;
                            currentFile = fileName;
                            oldValue = editArea.getText();
                        } catch (IOException ioException) {
                        }
                    }
                } else {
                    return;
                }
            } else {
                String str = null;
                JFileChooser fileChooser = new JFileChooser();
                fileChooser.setFileSelectionMode(JFileChooser.FILES_ONLY);
                //fileChooser.setApproveButtonText("确定");
                fileChooser.setDialogTitle("打开文件");
                int result = fileChooser.showOpenDialog(this);
                if (result == JFileChooser.CANCEL_OPTION) {
                    statusLabel.setText(" 您没有选择任何文件 ");
                    return;
                }
                File fileName = fileChooser.getSelectedFile();
                if (fileName == null || fileName.getName().equals("")) {
                    JOptionPane.showMessageDialog(this, "不合法的文件名", "不合法的文件名", JOptionPane.ERROR_MESSAGE);
                } else {
                    try {
                        FileReader fr = new FileReader(fileName);
                        BufferedReader bfr = new BufferedReader(fr);
                        editArea.setText("");
                        while ((str = bfr.readLine()) != null) {
                            editArea.append(str);
                        }
                        this.setTitle(fileName.getName() + " - 记事本");
                        statusLabel.setText(" 当前打开文件：" + fileName.getAbsoluteFile());
                        fr.close();
                        isNewFile = false;
                        currentFile = fileName;
                        oldValue = editArea.getText();
                    } catch (IOException ioException) {
                    }
                }
            }
        }//打开结束
        //保存
        else if (actionEvent.getSource() == fileMenuSave) {
            editArea.requestFocus();
            if (isNewFile) {
                String str = null;
                JFileChooser fileChooser = new JFileChooser();
                fileChooser.setFileSelectionMode(JFileChooser.FILES_ONLY);
                //fileChooser.setApproveButtonText("确定");
                fileChooser.setDialogTitle("保存");
                int result = fileChooser.showSaveDialog(this);
                if (result == JFileChooser.CANCEL_OPTION) {
                    statusLabel.setText("您没有选择任何文件");
                    return;
                }
                File saveFileName = fileChooser.getSelectedFile();
                if (saveFileName == null || saveFileName.getName().equals("")) {
                    JOptionPane.showMessageDialog(this, "不合法的文件名", "不合法的文件名", JOptionPane.ERROR_MESSAGE);
                } else {
                    try {
                        FileWriter fw = new FileWriter(saveFileName);
                        BufferedWriter bfw = new BufferedWriter(fw);
                        bfw.write(editArea.getText(), 0, editArea.getText().length());
                        bfw.flush();//刷新该流的缓冲
                        bfw.close();
                        isNewFile = false;
                        currentFile = saveFileName;
                        oldValue = editArea.getText();
                        this.setTitle(saveFileName.getName() + " - 记事本");
                        statusLabel.setText("当前打开文件：" + saveFileName.getAbsoluteFile());
                    } catch (IOException ioException) {
                    }
                }
            } else {
                try {
                    FileWriter fw = new FileWriter(currentFile);
                    BufferedWriter bfw = new BufferedWriter(fw);
                    bfw.write(editArea.getText(), 0, editArea.getText().length());
                    bfw.flush();
                    fw.close();
                } catch (IOException ioException) {
                }
            }
        }//保存结束
        //另存为
        else if (actionEvent.getSource() == fileMenuSaveAs) {
            editArea.requestFocus();
            String str = null;
            JFileChooser fileChooser = new JFileChooser();
            fileChooser.setFileSelectionMode(JFileChooser.FILES_ONLY);
            //fileChooser.setApproveButtonText("确定");
            fileChooser.setDialogTitle("另存为");
            int result = fileChooser.showSaveDialog(this);
            if (result == JFileChooser.CANCEL_OPTION) {
                statusLabel.setText("　您没有选择任何文件");
                return;
            }
            File saveFileName = fileChooser.getSelectedFile();
            if (saveFileName == null || saveFileName.getName().equals("")) {
                JOptionPane.showMessageDialog(this, "不合法的文件名", "不合法的文件名", JOptionPane.ERROR_MESSAGE);
            } else {
                try {
                    FileWriter fw = new FileWriter(saveFileName);
                    BufferedWriter bfw = new BufferedWriter(fw);
                    bfw.write(editArea.getText(), 0, editArea.getText().length());
                    bfw.flush();
                    fw.close();
                    oldValue = editArea.getText();
                    this.setTitle(saveFileName.getName() + "  - 记事本");
                    statusLabel.setText("　当前打开文件:" + saveFileName.getAbsoluteFile());
                } catch (IOException ioException) {
                }
            }
        }//另存为结束
        //页面设置
        else if (actionEvent.getSource() == fileMenuPageSetUp) {
            editArea.requestFocus();
            JOptionPane.showMessageDialog(this, "对不起，此功能尚未实现！更多请看http://pan.muyi.so", "提示", JOptionPane.WARNING_MESSAGE);
        }//页面设置结束
        //打印
        else if (actionEvent.getSource() == fileMenuPrint) {
            editArea.requestFocus();
            JOptionPane.showMessageDialog(this, "对不起，此功能尚未实现！更多请看http://pan.muyi.so", "提示", JOptionPane.WARNING_MESSAGE);
        }//打印结束
        //退出
        else if (actionEvent.getSource() == fileMenuExit) {
            int exitChoose = JOptionPane.showConfirmDialog(this, "确定要退出吗?", "退出提示", JOptionPane.OK_CANCEL_OPTION);
            if (exitChoose == JOptionPane.OK_OPTION) {
                System.exit(0);
            } else {
                return;
            }
        }//退出结束
        //编辑
        //else if(e.getSource()==editMenu)
        //{	checkMenuItemEnabled();//设置剪切、复制、粘贴、删除等功能的可用性
        //}
        //编辑结束
        //撤销
        else if (actionEvent.getSource() == editMenuUndo || actionEvent.getSource() == popupMenuUndo) {
            editArea.requestFocus();
            if (undo.canUndo()) {
                try {
                    undo.undo();
                } catch (CannotUndoException ex) {
                    System.out.println("Unable to undo:" + ex);
                    //ex.printStackTrace();
                }
            }
            if (!undo.canUndo()) {
                editMenuUndo.setEnabled(false);
            }
        }//撤销结束
        //剪切
        else if (actionEvent.getSource() == editMenuCut || actionEvent.getSource() == popupMenuCut) {
            editArea.requestFocus();
            String text = editArea.getSelectedText();
            StringSelection selection = new StringSelection(text);
            clipboard.setContents(selection, null);
            editArea.replaceRange("", editArea.getSelectionStart(), editArea.getSelectionEnd());
            checkMenuItemEnabled();//设置剪切，复制，粘帖，删除功能的可用性
        }//剪切结束
        //复制
        else if (actionEvent.getSource() == editMenuCopy || actionEvent.getSource() == popupMenuCopy) {
            editArea.requestFocus();
            String text = editArea.getSelectedText();
            StringSelection selection = new StringSelection(text);
            clipboard.setContents(selection, null);
            checkMenuItemEnabled();//设置剪切，复制，粘帖，删除功能的可用性
        }//复制结束
        //粘帖
        else if (actionEvent.getSource() == editMenuPaste || actionEvent.getSource() == popupMenuPaste) {
            editArea.requestFocus();
            Transferable contents = clipboard.getContents(this);
            if (contents == null) {
                return;
            }
            String text = "";
            try {
                text = (String) contents.getTransferData(DataFlavor.stringFlavor);
            } catch (Exception exception) {
            }
            editArea.replaceRange(text, editArea.getSelectionStart(), editArea.getSelectionEnd());
            checkMenuItemEnabled();
        }//粘帖结束
        //删除
        else if (actionEvent.getSource() == editMenuDelete || actionEvent.getSource() == popupMenuDelete) {
            editArea.requestFocus();
            editArea.replaceRange("", editArea.getSelectionStart(), editArea.getSelectionEnd());
            checkMenuItemEnabled();    //设置剪切、复制、粘贴、删除等功能的可用性
        }//删除结束
        //查找
        else if (actionEvent.getSource() == editMenuFind) {
            editArea.requestFocus();
            find();
        }//查找结束
        //查找下一个
        else if (actionEvent.getSource() == editMenuFindNext) {
            editArea.requestFocus();
            find();
        }//查找下一个结束
        //替换
        else if (actionEvent.getSource() == editMenuReplace) {
            editArea.requestFocus();
            replace();
        }//替换结束
        //转到
        else if (actionEvent.getSource() == editMenuGoTo) {
            editArea.requestFocus();
            JOptionPane.showMessageDialog(this, "对不起，此功能尚未实现！更多请看http://pan.muyi.so", "提示", JOptionPane.WARNING_MESSAGE);
        }//转到结束
        //时间日期
        else if (actionEvent.getSource() == editMenuTimeDate) {
            editArea.requestFocus();
            //SimpleDateFormat currentDateTime=new SimpleDateFormat("HH:mmyyyy-MM-dd");
            //editArea.insert(currentDateTime.format(new Date()),editArea.getCaretPosition());
            Calendar rightNow = Calendar.getInstance();
            Date date = rightNow.getTime();
            editArea.insert(date.toString(), editArea.getCaretPosition());
        }//时间日期结束
        //全选
        else if (actionEvent.getSource() == editMenuSelectAll || actionEvent.getSource() == popupMenuSelectAll) {
            editArea.selectAll();
        }//全选结束
        //自动换行(已在前面设置)
        else if (actionEvent.getSource() == formatMenuLineWrap) {
            if (formatMenuLineWrap.getState()) {
                editArea.setLineWrap(true);
            } else {
                editArea.setLineWrap(false);
            }

        }//自动换行结束
        //字体设置
        else if (actionEvent.getSource() == formatMenuFont) {
            editArea.requestFocus();
            font();
        }//字体设置结束
        //设置状态栏可见性
        else if (actionEvent.getSource() == viewMenuStatus) {
            if (viewMenuStatus.getState()) {
                statusLabel.setVisible(true);
            } else {
                statusLabel.setVisible(false);
            }
        }//设置状态栏可见性结束
        //帮助主题
        else if (actionEvent.getSource() == helpMenuHelpTopics) {
            editArea.requestFocus();
            JOptionPane.showMessageDialog(this, "路漫漫其修远兮，吾将上下而求索。", "帮助主题", JOptionPane.INFORMATION_MESSAGE);
        }//帮助主题结束
        //关于
        else if (actionEvent.getSource() == helpMenuAboutNotepad) {
            editArea.requestFocus();
            JOptionPane.showMessageDialog(this,
                    "&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&\n" +
                            " 编写者：沐伊科技 \n" +
                            " 编写时间：2016-06-09                          \n" +
                            " 更多教程：http://pan.muyi.so (网盘资源教程应有尽有哦!)     \n" +
                            " e-mail：llqqxf@163.com                \n" +
                            " 一些地方借鉴他人，不足之处希望大家能提出意见，谢谢！  \n" +
                            "&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&\n",
                    "记事本", JOptionPane.INFORMATION_MESSAGE);
        }//关于结束
    }//方法actionPerformed()结束

    /**
     * 实现DocumentListener接口中的方法(与撤销操作有关)
     */
    @Override
    public void insertUpdate(DocumentEvent documentEvent) {
        editMenuUndo.setEnabled(true);
    }

    @Override
    public void removeUpdate(DocumentEvent documentEvent) {
        editMenuUndo.setEnabled(true);
    }

    @Override
    public void changedUpdate(DocumentEvent documentEvent) {
        editMenuUndo.setEnabled(true);
    }//DocumentListener结束

    /**
     * 实现接口UndoableEditListener的类UndoHandler(与撤销操作有关)
     */
    class UndoHandler implements UndoableEditListener {
        @Override
        public void undoableEditHappened(UndoableEditEvent uee) {
            undo.addEdit(uee.getEdit());
        }
    }


    /**
     * main函数开始
     */
    public static void main(String[] args) {
        NotePad notepad = new NotePad();
        //使用 System exit 方法退出应用程序
        notepad.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }//main函数结束


}


```

---
***参考：
[首席撩妹指导官](https://blog.csdn.net/qq_36864672/article/details/78598912)***
