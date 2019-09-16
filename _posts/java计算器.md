---
title: java实验楼

date: {{date}}
categories:
- 项目
tags:
- java
- 项目

---
# 题目
java实现计算器

# 题解

```
package calculator;

import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.math.BigDecimal;
import java.util.Vector;

/**
 * Demo class
 *
 * @author: Mr.Li
 * @date: 2019-09-13 15:51
 **/
@SuppressWarnings("AlibabaCommentsMustBeJavadocFormat")
public class Calculator {

    /**操作数1*/
    private String str1 = "0";
    /**操作数2*/
    private String str2 = "0";
    /**运算符*/
    private String signal = "+";
    /**运算结果*/
    private String result = "";


    /**开关 1 用于选择输入方向，输入 str1 还是 str2*/
    private int k1 = 1;
    /**开关 2 用于记录符号键的次数，如果 k2 > 1 说明进行的是 2+3-8+9 这样的多符号运算*/
    private int k2 = 1;
    /**开关 3 用于标识 str1 是否可以被清零，等于 1 时可以，不等于 1 时不能被清零*/
    private int k3 = 1;
    /**开关 4 用于标识 str2 是否可以被清零*/
    private int k4 = 1;
    /**开关 5 用于控制小数点可否被录入，等于 1 时可以*/
    private int k5 = 1;
    /**store 的作用类似于寄存器，用于记录是否连续按下符号键*/
    private JButton store;

    /**存储按钮，以便多符号值运算*/
    private Vector vt = new Vector(20, 10);
    /**声明框架，按钮变量并初始化*/
    JFrame frame = new JFrame("Calculator");
    JTextField resultTextField = new JTextField(result, 20);
    JButton clearButton = new JButton("clear");

    JButton button0 = new JButton("0");
    JButton button1 = new JButton("1");
    JButton button2 = new JButton("2");
    JButton button3 = new JButton("3");
    JButton button4 = new JButton("4");
    JButton button5 = new JButton("5");
    JButton button6 = new JButton("6");
    JButton button7 = new JButton("7");
    JButton button8 = new JButton("8");
    JButton button9 = new JButton("9");

    JButton buttonDian = new JButton(".");
    JButton buttonJia = new JButton("+");
    JButton buttonJian = new JButton("-");
    JButton buttonCheng = new JButton("*");
    JButton buttonChu = new JButton("/");
    JButton buttonDy = new JButton("=");


    public Calculator(){
        //为按钮设置等效键，即可以通过对应键盘按键 + Alt 来代替点击它
        button0.setMnemonic(KeyEvent.VK_NUMPAD0);
        button1.setMnemonic(KeyEvent.VK_NUMPAD1);
        button2.setMnemonic(KeyEvent.VK_NUMPAD2);
        button3.setMnemonic(KeyEvent.VK_NUMPAD3);
        button4.setMnemonic(KeyEvent.VK_NUMPAD4);
        button5.setMnemonic(KeyEvent.VK_NUMPAD5);
        button6.setMnemonic(KeyEvent.VK_NUMPAD6);
        button7.setMnemonic(KeyEvent.VK_NUMPAD7);
        button8.setMnemonic(KeyEvent.VK_NUMPAD8);
        button9.setMnemonic(KeyEvent.VK_NUMPAD9);

        buttonJia.setMnemonic(KeyEvent.VK_ADD);
        buttonJian.setMnemonic(KeyEvent.VK_SUBTRACT);
        buttonCheng.setMnemonic(KeyEvent.VK_MULTIPLY);
        buttonChu.setMnemonic(KeyEvent.VK_SEPARATER);

        buttonDian.setMnemonic(KeyEvent.VK_DECIMAL);
        buttonDy.setMnemonic(KeyEvent.VK_EQUALS);
        clearButton.setMnemonic(KeyEvent.VK_BACK_SPACE);
        //设置文本框为右对齐，使输入和结果都靠右显示
        resultTextField.setHorizontalAlignment(JTextField.RIGHT);

        //将 UI 组件添加进容器内
        //创建第一个 JPanel
        JPanel panel = new JPanel();
        panel.setLayout(new GridLayout(4, 4, 5, 5));
        panel.add(button7);
        panel.add(button8);
        panel.add(button9);
        panel.add(buttonChu);
        panel.add(button4);
        panel.add(button5);
        panel.add(button6);
        panel.add(buttonCheng);
        panel.add(button1);
        panel.add(button2);
        panel.add(button3);
        panel.add(buttonJian);
        panel.add(button0);
        panel.add(buttonDian);
        panel.add(buttonDy);
        panel.add(buttonJia);

        //设置 panel 对象变距
        panel.setBorder(BorderFactory.createEmptyBorder(5, 5, 5, 5));

        //创建第二个 JPanel
        JPanel panel2 = new JPanel();
        panel2.setLayout(new BorderLayout());
        panel2.add(resultTextField, BorderLayout.WEST);
        panel2.add(clearButton, BorderLayout.EAST);

        //设置主窗口在屏幕上的位置
        frame.setLocation(300, 200);
        //设置窗体不能调整大小
        frame.setResizable(false);
        //设置窗格内容，添加 panel 和 panel2 并设置位置
        frame.getContentPane().setLayout(new BorderLayout());
        frame.getContentPane().add(panel, BorderLayout.SOUTH);
        frame.getContentPane().add(panel2, BorderLayout.NORTH);

        //让窗格自适应大小，包住里面的内容
        frame.pack();
        //窗体可视化
        frame.setVisible(true);


        //事件处理程序

        //数字键
        class Listener implements ActionListener{
            @Override
            public void actionPerformed(ActionEvent actionEvent) {
                String ss = ((JButton) actionEvent.getSource()).getText();
                store = (JButton) actionEvent.getSource();
                vt.add(store);

                if (k1 == 1){
                    //这里存在一个字符串清空（上一步留下的）
                    if (k3 == 1){
                        str1 = "";
                        k5 = 1;
                    }
                    str1 = str1 + ss;
                    k3 = k3 + 1;
                    resultTextField.setText(str1);
                } else if (k1 == 2){
                    if (k4 == 1){
                        str2 = "";
                        k5 = 1;
                    }
                    str2 = str2 + ss;
                    k4 = k4 + 1;
                    resultTextField.setText(str2);
                }
            }
        }

        //符号键
        class ListenerSignal implements ActionListener {
            @Override
            public void actionPerformed(ActionEvent actionEvent) {
                String ss2 = ((JButton) actionEvent.getSource()).getText();
                store = (JButton) actionEvent.getSource();
                vt.add(store);

                if (k2 == 1){
                    k1 = 2;
                    k5 = 1;
                    signal = ss2;
                    k2 = k2 + 1;
                } else {
                    int a = vt.size();
                    JButton c = (JButton) vt.get(a - 2);

                    if (!(c.getText().equals("+"))
                            && !(c.getText().equals("-"))
                            && !(c.getText().equals("*"))
                            && !(c.getText().equals("/"))){
                        cal();
                        str1 = result;
                        k1 = 2;
                        k5 = 1;
                        k4 = 1;
                        signal = ss2;
                    }
                    k2 = k2 + 1;
                }
            }
        }

        //清除键
        class ListenerClear implements ActionListener {
            @Override
            public void actionPerformed(ActionEvent actionEvent) {
                store = (JButton) actionEvent.getSource();
                vt.add(store);
                k5 = 1;
                k2 = 1;
                k1 = 1;
                k3 = 1;
                k4 = 1;
                str1 = "";
                str2 = "";
                signal = "";
                result = "";
                resultTextField.setText(result);
                vt.clear();
            }
        }

        //等号键
        class ListenerDy implements ActionListener {
            @Override
            public void actionPerformed(ActionEvent actionEvent) {
                store = (JButton) actionEvent.getSource();
                vt.add(store);
                cal();

                k1 = 1;
                k2 = 1;
                k3 = 1;
                k4 = 1;

                str1 = result;
            }
        }

        //小数点键
        class ListenerPoint implements ActionListener {
            @Override
            public void actionPerformed(ActionEvent actionEvent) {
                String ss3 = ((JButton) actionEvent.getSource()).getText();
                store = (JButton) actionEvent.getSource();
                vt.add(store);
                if (k5 == 1){
                    if (k1 == 1){
                        if (k3 == 1){
                            str1 = "";
                            k5 = 1;
                        }
                        str1 = str1 + ss3;
                        k3 = k3 + 1;
                        resultTextField.setText(str1);
                    } else if (k1 == 2){
                        if (k4 == 1){
                            str2 = "";
                            k5 = 1;
                        }
                        str2 = str2 + ss3;
                        k4 = k4 + 1;
                        resultTextField.setText(str2);
                    }
                }
                k5 = k5 + 1;
            }
        }

        //声明监听器对象
        ListenerDy jtDy = new ListenerDy();
        Listener jt = new Listener();
        ListenerSignal jtSignal = new ListenerSignal();
        ListenerClear jtClear = new ListenerClear();
        ListenerPoint jtPoint = new ListenerPoint();

        //为按钮添加监听器
        button7.addActionListener(jt);
        button8.addActionListener(jt);
        button9.addActionListener(jt);
        buttonChu.addActionListener(jtSignal);
        button4.addActionListener(jt);
        button5.addActionListener(jt);
        button6.addActionListener(jt);
        buttonCheng.addActionListener(jtSignal);
        button1.addActionListener(jt);
        button2.addActionListener(jt);
        button3.addActionListener(jt);
        buttonJian.addActionListener(jtSignal);
        button0.addActionListener(jt);
        buttonDian.addActionListener(jtPoint);
        buttonDy.addActionListener(jtDy);
        buttonJia.addActionListener(jtSignal);
        clearButton.addActionListener(jtClear);

        //正常关闭窗口，等效frame.setDefaultCloseOptration(JFrame.EXIT_ON_CLOSE);
        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }

    //计算
    public void cal(){
        double a2;
        double b2;
        String c = signal;
        double result2 = 0;
        if (c.equals("")){
            resultTextField.setText("please input operator");
        } else {
            if (str1.equals(".")){
                str1 = "0.0";
            }
            if (str2.equals(".")){
                str2 = "0.0";
            }
            a2 = Double.valueOf(str1).doubleValue();
            b2 = Double.valueOf(str2).doubleValue();

            if (c.equals("+")){
                result2 = a2 + b2;
            }
            if (c.equals("-")){
                result2 = a2 - b2;
            }
            if (c.equals("*")){
                //大数字
                BigDecimal m1 = new BigDecimal(Double.toString(a2));
                BigDecimal m2 = new BigDecimal(Double.toString(b2));
                result2 = m1.multiply(m2).doubleValue();
            }
            if (c.equals("/")){
                if (b2 == 0.0){
                    result2 = 0.0;
                } else {
                    result2 = a2 / b2;
                }
            }

            result = Double.toString(result2);
            resultTextField.setText(result);
        }
    }

    public static void main(String[] args) {
        try {

            //界面风格
            UIManager.setLookAndFeel("javax.swing.plaf.metal.MetalLookAndFeel");
//            UIManager.setLookAndFeel("com.sun.java.swing.plaf.windows.WindowsLookAndFeel");
        } catch (Exception e) {
            e.printStackTrace();
        }
        Calculator calculator = new Calculator();
    }
}

```

---
***参考：
[实验楼](https://www.shiyanlou.com/courses/185)***
