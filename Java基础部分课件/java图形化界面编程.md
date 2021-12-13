# 一. 课程概述

通常情况下，java语言一般是用来开发后台程序的，所谓的后台程序就是部署在服务器端的程序，默默的工作，用户是看不到任何界面的，所以很多情况下，学习java会感觉很枯燥。

![](./images/服务器.jpg)

事实上，我们使用java语言同样可以完成图形化界面程序的开发，而学习图形化界面编程相对来说就会有趣很多，因为所见即所得，也就是说，我们写的大部分代码的执行效果，是可以通过图形化界面实实在在能够看得到的。

![](./images/图形化界面.gif)

java使用AWT和Swing相关的类可以完成图形化界面编程，其中AWT的全称是抽象窗口工具集(Abstract Window Toolkit),它是sun公司最早提供的GUI库，这个GUI库提供了一些基本功能，但这个GUI库的功能比较有限，所以后来sun公司又提供了Swing库。通过使用AWT和Swing提供的图形化界面组件库，java的图形化界面编程非常简单，程序只需要依次创建所需的图形组件，并以合适的方式将这些组件组织在一起，就可以开发出非常美观的用户界面。

本次讲解的java开发平台是jdk9，希望大家课后练习时也使用jdk9，因为不同版本的jdk提供的GUI库的效果略有不同。

# 二. AWT 编程

## 2.1 AWT简介

​     当 JDK 1.0发布时， Sun 提供了 一套基本的GUI类库，这个GUI类库希望可以在所有平台下都能运行 ， 这套基本类库被称为"抽象窗口工具集 CAbstract Window Toolkit )"，它为Java应用程序提供了基本的图形组件 。 AWT是窗口框架，它从不同平台的窗口系统中抽取出共同组件 ， 当程序运行时，将这些组件的创建和动作委托给程序所在的运行平台 。 简而言之 ，当使用 AWT 编写图形界面应用 时， 程序仅指定了界面组件的位置和行为，并未提供真正的实现，JVM调用操作系统本地的图形界面来创建和平台 一致的对等体 。

​	使用AWT创建的图形界面应用和所在的运行平台有相同的界面风格 ， 比如在 Windows 操作系统上，它就表现出 Windows 风格 ; 在 UNIX 操作系统上，它就表现出UNIX 风格 。 Sun 希望采用这种方式来实现 " Write Once, Run Anywhere " 的目标 。

## 2.2 AWT继承体系

所有和 AWT 编程相关的类都放在 java.awt 包以及它的子包中， AWT 编程中有两个基类 :Component和 MenuComponent。

- Component：代表一个能以图形化方式显示出来，并可与用户交互的对象，例如 Button 代表一个按钮，TextField 代表 一个文本框等；
- MenuComponent：则代表图形界面的菜单组件，包括 MenuBar (菜单条)、 Menultem (菜单项)等子类。

![](./images/AWT组件继承体系.png)

其中 Container 是一种特殊的 Component，它代表一种容器，可以盛装普通的 Component。

AWT中还有一个非常重要的接口叫LayoutManager ，如果一个容器中有多个组件，那么容器就需要使用LayoutManager来管理这些组件的布局方式。

![](./images/LayoutManager.png)



## 2.3 Container容器

### 2.3.1 Container继承体系

![](./images/Container继承体系.png)

- ​	Winow是可以独立存在的顶级窗口,默认使用BorderLayout管理其内部组件布局;
- ​        Panel可以容纳其他组件，但不能独立存在，它必须内嵌其他容器中使用，默认使用FlowLayout管理其内部组件布局；
- ​        ScrollPane 是 一个带滚动条的容器，它也不能独立存在，默认使用 BorderLayout 管理其内部组件布局；

### 2.3.2 常见API

Component作为基类，提供了如下常用的方法来设置组件的大小、位置、可见性等。

| 方法签名                                       | 方法功能                   |
| ---------------------------------------------- | -------------------------- |
| setLocation(int x, int y)                      | 设置组件的位置。           |
| setSize(int width, int height)                 | 设置组件的大小。           |
| setBounds(int x, int y, int width, int height) | 同时设置组件的位置、大小。 |
| setVisible(Boolean b):                         | 设置该组件的可见性。       |

Container作为容器根类，提供了如下方法来访问容器中的组件

| 方法签名                                | 方法功能                                                     |
| --------------------------------------- | ------------------------------------------------------------ |
| Component add(Component comp)           | 向容器中添加其他组件 (该组件既可以是普通组件，也可以 是容器) ， 并返回被添加的组件 。 |
| Component getComponentAt(int x, int y): | 返回指定点的组件 。                                          |
| int getComponentCount():                | 返回该容器内组件的数量 。                                    |
| Component[] getComponents():            | 返回该容器内的所有组件 。                                    |

### 2.3.3 容器演示

#### 2.3.3.1 Window

​	![](./images/FrameDemo.jpg)

```java
import java.awt.*;

public class FrameDemo {

    public static void main(String[] args) {
        //1.创建窗口对象
        Frame frame = new Frame("这是第一个窗口容器");

        //设置窗口的位置和大小

        frame.setBounds(100,100,500,300);

        //设置窗口可见
        frame.setVisible(true);
    }
}
```



#### 2.3.3.2 Panel

​	![](./images/PanelDemo.jpg))

```java
public class PanelDemo {
    public static void main(String[] args) {
        //1.创建Frame容器对象
        Frame frame = new Frame("这里在测试Panel");
        //2.创建Panel容器对象
        Panel panel = new Panel();

        //3.往Panel容器中添加组件
        panel.add(new TextField("这是一个测试文本"));
        panel.add(new Button("这是一个测试按钮"));

        //4.把Panel添加到Frame中
        frame.add(panel);

        //5.设置Frame的位置和大小
        frame.setBounds(30,30,500,300);

        //6.设置Frame可见
        frame.setVisible(true);
    }
}
```

由于IDEA默认使用utf-8进行编码，但是当前我们执行代码是是在windows系统上，而windows操作系统的默认编码是gbk，所以会乱码，如果出现了乱码，那么只需要在运行当前代码前，设置一个jvm参数  -Dfile.encoding=gbk即可。

#### 2.3.3.3 ScrollPane

​	![](./images/ScrollPaneDemo.jpg)

```java
import java.awt.*;

public class ScrollPaneDemo {

    public static void main(String[] args) {
        //1.创建Frame窗口对象
        Frame frame = new Frame("这里测试ScrollPane");

        //2.创建ScrollPane对象，并且指定默认有滚动条
        ScrollPane scrollPane = new ScrollPane(ScrollPane.SCROLLBARS_ALWAYS);

        //3.往ScrollPane中添加组件
        scrollPane.add(new TextField("这是测试文本"));
        scrollPane.add(new Button("这是测试按钮"));

        //4.把ScrollPane添加到Frame中
        frame.add(scrollPane);

        //5.设置Frame的位置及大小
        frame.setBounds(30,30,500,300);

        //6.设置Frame可见
        frame.setVisible(true);

    }
}
```

程序明明向 ScrollPane 容器中添加了 一个文本框和一个按钮，但只能看到 一个按钮，却看不到文本框 ，这是为什么 呢?这是因为ScrollPane 使用 BorderLayout 布局管理器的缘故，而 BorderLayout 导致了该容器中只有一个组件被显示出来 。 下一节将向详细介绍布局管理器的知识 。

## 2.4 LayoutManager布局管理器

之前，我们介绍了Component中有一个方法 setBounds() 可以设置当前容器的位置和大小，但是我们需要明确一件事，如果我们手动的为组件设置位置和大小的话，就会造成程序的不通用性，例如：

```java
Label label = new Label("你好，世界");
```

创建了一个lable组件，很多情况下，我们需要让lable组件的宽高和“你好，世界”这个字符串自身的宽高一致，这种大小称为**最佳大小**。由于操作系统存在差异，例如在windows上，我们要达到这样的效果，需要把该Lable组件的宽和高分别设置为100px,20px,但是在Linux操作系统上，可能需要把Lable组件的宽和高分别设置为120px，24px，才能达到同样的效果。

如果要让我么的程序在不同的操作系统下，都有相同的使用体验，那么手动设置组件的位置和大小，无疑是一种灾难，因为有太多的组件，需要分别设置不同操作系统下的大小和位置。为了解决这个问题，Java提供了LayoutManager布局管理器，可以根据运行平台来自动调整组件大小，程序员不用再手动设置组件的大小和位置了，只需要为容器选择合适的布局管理器即可。

![](./images/常用布局管理器.png)

### 2.4.1 FlowLayout

​        在 FlowLayout 布局管理器 中，组件像水流一样向某方向流动 (排列) ，遇到障碍(边界)就折回，重头开始排列 。在默认情况下， FlowLayout 布局管理器从左向右排列所有组件，遇到边界就会折回下一行重新开始。

| 构造方法                                | 方法功能                                                     |
| --------------------------------------- | ------------------------------------------------------------ |
| FlowLayout()                            | 使用默认 的对齐方式及默认的垂直间距、水平间距创建 FlowLayout 布局管理器。 |
| FlowLayout(int align)                   | 使用指定的对齐方式及默认的垂直间距、水平间距创建 FlowLayout 布局管理器。 |
| FlowLayout(int align,int hgap,int vgap) | 使用指定的对齐方式及指定的垂直问距、水平间距创建FlowLayout 布局管理器。 |

FlowLayout 中组件的排列方向(从左向右、从右向左、从中间向两边等) ， 该参数应该使用FlowLayout类的静态常量 : FlowLayout. LEFT 、 FlowLayout. CENTER 、 FlowLayout. RIGHT ，默认是左对齐。

FlowLayout 中组件中间距通过整数设置，单位是像素，默认是5个像素。

**代码演示：**

​	![](./images/FlowLayout.jpg)

```java
import java.awt.*;

public class FlowLayoutDemo {

    public static void main(String[] args) {
        //1.创建Frame对象
        Frame frame = new Frame("这里测试FlowLayout");
        //2.修改Frame容器的布局管理器为FlowLayout
        frame.setLayout(new FlowLayout(FlowLayout.LEFT,20,20));

        //3.往Frame中添加100个button
        for (int i = 0; i < 100; i++) {
            frame.add(new Button("按钮"+i));
        }

        //4.设置Frame为最佳大小
        frame.pack();
        //5.设置Frame可见
        frame.setVisible(true);
    }
}
```

### 2.4.2 BorderLayout

BorderLayout 将容器分为 EAST 、 SOUTH 、 WEST 、 NORTH 、 CENTER五个区域，普通组件可以被放置在这 5 个区域的任意一个中 。 BorderLayout布局 管理器的布局示意图如图所示 。

![](./images/BorderLayout.png)

当改变使用 BorderLayout 的容器大小时， NORTH 、 SOUTH 和 CENTER区域水平调整，而 EAST 、 WEST 和 CENTER 区域垂直调整。使用BorderLayout 有如下两个注意点:

1. 当向使用 BorderLayout 布局管理器的容器中添加组件时 ， 需要指定要添加到哪个区域中 。 如果没有指定添加到哪个区域中，则默认添加到中间区域中；
2. 如果向同一个区域中添加多个组件时 ， 后放入的组件会覆盖先放入的组件；

| 构造方法                         | 方法功能                                                     |
| -------------------------------- | ------------------------------------------------------------ |
| BorderLayout()                   | 使用默认的水平间距、垂直 间距创建 BorderLayout 布局管理器 。 |
| BorderLayout(int hgap,int vgap): | 使用指定的水平间距、垂直间距创建 BorderLayout 布局管理器。   |

**代码演示1:**

​	![](./images/BorderLayout.jpg)

```java
import java.awt.*;

public class BorderLayoutDemo1 {

    public static void main(String[] args) {
        //1.创建Frame对象
        Frame frame = new Frame("这里测试BorderLayout");
        //2.指定Frame对象的布局管理器为BorderLayout
        frame.setLayout(new BorderLayout(30,5));
        //3.往Frame指定东南西北中各添加一个按钮组件
        frame.add(new Button("东侧按钮"), BorderLayout.EAST);
        frame.add(new Button("西侧按钮"), BorderLayout.WEST);
        frame.add(new Button("南侧按钮"), BorderLayout.SOUTH);
        frame.add(new Button("北侧按钮"), BorderLayout.NORTH);
        frame.add(new Button("中间按钮"), BorderLayout.CENTER);
        //4.设置Frame为最佳大小
        frame.pack();
        //5.设置Frame可见
        frame.setVisible(true);
    }
}
```



如果不往某个区域中放入组件，那么该区域不会空白出来，而是会被其他区域占用

**代码演示2:**

​	![](./images/BorderLayoutDemo2.jpg)

```java
import java.awt.*;

public class BorderLayoutDemo2 {

    public static void main(String[] args) {
        //1.创建Frame对象
        Frame frame = new Frame("这里测试BorderLayout");
        //2.指定Frame对象的布局管理器为BorderLayout
        frame.setLayout(new BorderLayout(30,5));
        //3.往Frame指定南，北，放入一个按钮，往中间区域放入一个Panel

        frame.add(new Button("南侧按钮"), BorderLayout.SOUTH);
        frame.add(new Button("北侧按钮"), BorderLayout.NORTH);

        Panel panel = new Panel();
        panel.add(new TextField("测试文本"));
        panel.add(new Button("中间按钮"));

        frame.add(panel, BorderLayout.CENTER);
	
        //4.设置Frame为最佳大小
        frame.pack();
        //5.设置Frame可见
        frame.setVisible(true);
    }
}
```



### 2.4.3 GridLayout

​        GridLayout 布局管理器将容器分割成纵横线分隔的网格 ， 每个网格所占的区域大小相同。当向使用 GridLayout 布局管理器的容器中添加组件时， 默认从左向右、 从上向下依次添加到每个网格中 。 与 FlowLayout不同的是，放置在 GridLayout 布局管理器中的各组件的大小由组件所处的区域决定(每 个组件将自动占满整个区域) 。    

| 构造方法                                        | 方法功能                                                     |
| ----------------------------------------------- | ------------------------------------------------------------ |
| GridLayout(int rows,in t cols)                  | 采用指定的行数、列数，以及默认的横向间距、纵向间距将容器 分割成多个网格 |
| GridLayout(int rows,int cols,int hgap,int vgap) | 采用指定 的行数、列 数 ，以及指定的横向间距 、 纵向间距将容器分割成多个网格。 |

**案例：**

​	使用Frame+Panel，配合FlowLayout和GridLayout完成一个计算器效果。

​	![](./images/计算器.jpg)



**代码：**

```java
import java.awt.*;

public class GridLayoutDemo{

    public static void main(String[] args) {

        //1.创建Frame对象，并且标题设置为计算器
        Frame frame = new Frame("计算器");

        //2.创建一个Panel对象，并且往Panel中放置一个TextField组件
        Panel p1 = new Panel();
        p1.add(new TextField(30));

        //3.把上述的Panel放入到Frame的北侧区域
        frame.add(p1,BorderLayout.NORTH);

        //4.创建一个Panel对象，并且设置其布局管理器为GridLayout
        Panel p2 = new Panel();
        p2.setLayout(new GridLayout(3,5,4,4));

        //5.往上述Panel中，放置15个按钮，内容依次是：0,1,2,3,4,5,6，7,8,9，+，-，*，/,.
        for (int i = 0; i < 10; i++) {
            p2.add(new Button(i+""));
        }
        p2.add(new Button("+"));
        p2.add(new Button("-"));
        p2.add(new Button("*"));
        p2.add(new Button("/"));
        p2.add(new Button("."));

        //6.把上述Panel添加到Frame的中间区域中国
        frame.add(p2);
        //7.设置Frame为最佳大小
        frame.pack();

        //8.设置Frame可见
        frame.setVisible(true);

    }
}
```

### 2.4.4 GridBagLayout

GridBagLayout 布局管理器的功能最强大 ， 但也最复杂，与 GridLayout 布局管理器不同的是， 在GridBagLayout 布局管理器中，一个组件可以跨越一个或多个网格 ， 并可以设置各网格的大小互不相同，从而增加了布局的灵活性 。 当窗口的大小发生变化时 ， GridBagLayout 布局管理器也可以准确地控制窗口各部分的拉伸 。

![](./images/GridBagLayout.png)

由于在GridBagLayout 布局中，每个组件可以占用多个网格，此时，我们往容器中添加组件的时候，就需要具体的控制每个组件占用多少个网格，java提供的GridBagConstaints类，与特定的组件绑定，可以完成具体大小和跨越性的设置。

**GridBagConstraints API:**

| 成员变量   | 含义                                                         |
| ---------- | ------------------------------------------------------------ |
| gridx      | 设置受该对象控制的GUI组件左上角所在网格的横向索引            |
| gridy      | 设置受该对象控制的GUI组件左上角所在网格的纵向索引            |
| gridwidth  | 设置受该对象控制的 GUI 组件横向跨越多少个网格,如果属性值为 GridBagContraints.REMAIND,则表明当前组件是横向最后一个组件，如果属性值为GridBagConstraints.RELATIVE,表明当前组件是横向倒数第二个组件。 |
| gridheight | 设置受该对象控制的 GUI 组件纵向跨越多少个网格，如果属性值为 GridBagContraints.REMAIND,则表明当前组件是纵向最后一个组件，如果属性值为GridBagConstraints.RELATIVE,表明当前组件是纵向倒数第二个组件。 |
| fill       | 当"显示区域"大于"组件"的时候,如何调整组件 ：<br/> GridBagConstraints.NONE : GUI 组件不扩大<br/> GridBagConstraints.HORIZONTAL: GUI 组件水平扩大 以 占据空白区域<br/> GridBagConstraints.VERTICAL: GUI 组件垂直扩大以占据空白区域<br/> GridBagConstraints.BOTH: GUI 组件水平 、 垂直同时扩大以占据空白区域. |
| ipadx      | 设置受该对象控制的 GUI 组件横向内部填充的大小，即 在该组件最小尺寸的基础上还需要增大多少. |
| ipady      | 设置受该对象控制的 GUI 组件纵向内部填充的大小，即 在该组件最小尺寸的基础上还需要增大多少. |
| insets     | 设置受该对象控制 的 GUI 组件的 外部填充的大小 ， 即该组件边界和显示区 域边界之间的 距离 . |
| weightx    | 设置受该对象控制 的 GUI 组件占据多余空间的水平比例， 假设某个容器 的水平线上包括三个 GUI 组件， 它们的水平增加比例分别是 1 、 2 、 3 ， 但容器宽度增加 60 像素 时，则第一个组件宽度增加 10 像素 ， 第二个组件宽度增加 20 像素，第三个组件宽度增加 30 像 素。 如 果其增 加比例为 0 ， 则 表示不会增加 。 |
| weighty    | 设置受该对象控制 的 GUI 组件占据多余空间的垂直比例           |
| anchor     | 设置受该对象控制 的 GUI 组件在其显示区域中的定位方式:<br/>GridBagConstraints .CENTER (中 间 )<br/>GridBagConstraints.NORTH (上中 ) <br/>GridBagConstraints.NORTHWEST (左上角)<br/>GridBagConstraints.NORTHEAST (右上角)<br/>GridBagConstraints.SOUTH (下中) <br/>GridBagConstraints.SOUTHEAST (右下角)<br/>GridBagConstraints.SOUTHWEST (左下角)<br/>GridBagConstraints.EAST (右中) <br/>GridBagConstraints.WEST (左中) |



**GridBagLayout使用步骤：**

```
1.创建GridBagLaout布局管理器对象，并给容器设置该布局管理器对象；

2.创建GridBagConstraints对象，并设置该对象的控制属性：

	gridx: 用于指定组件在网格中所处的横向索引；

	gridy: 用于执行组件在网格中所处的纵向索引；

	gridwidth: 用于指定组件横向跨越多少个网格；

	gridheight: 用于指定组件纵向跨越多少个网格；

3.调用GridBagLayout对象的setConstraints(Component c,GridBagConstraints gbc )方法，把即将要添加到容器中的组件c和GridBagConstraints对象关联起来；

4. 把组件添加到容器中；
```

**案例：**

​	使用Frame容器，设置GridBagLayout布局管理器，实现下图中的效果：

​	![](./images/GridBagLayout.jpg)

**演示代码：**

```java
import java.awt.*;

public class GridBagLayoutDemo {

    public static void main(String[] args) {
        //1.创建Frame对象
        Frame frame = new Frame("这里是GridBagLayout测试");

        //2.创建GridBagLayout对象
        GridBagLayout gbl = new GridBagLayout();

        //3.把Frame对象的布局管理器设置为GridBagLayout
        frame.setLayout(gbl);

        //4.创建GridBagConstraints对象
        GridBagConstraints gbc = new GridBagConstraints();

        //5.创建容量为10的Button数组
        Button[] bs = new Button[10];

        //6.遍历数组，初始化每一个Button
        for (int i = 0; i < bs.length; i++) {
            bs[i] = new Button("按钮"+(i+1));
        }

        //7.设置所有的GridBagConstraints对象的fill属性为GridBagConstraints.BOTH,当有空白区域时，组件自动扩大占满空白区域
        gbc.fill=GridBagConstraints.BOTH;

        //8.设置GridBagConstraints对象的weightx设置为1,表示横向扩展比例为1
        gbc.weightx=1;

        //9.往frame中添加数组中的前3个Button
        addComponent(frame,bs[0],gbl,gbc);
        addComponent(frame,bs[1],gbl,gbc);
        addComponent(frame,bs[2],gbl,gbc);

        //10.把GridBagConstraints的gridwidth设置为GridBagConstraints.REMAINDER,则表明当前组件是横向最后一个组件
        gbc.gridwidth=GridBagConstraints.REMAINDER;

        //11.把button数组中第四个按钮添加到frame中
        addComponent(frame,bs[3],gbl,gbc);


        //12.把GridBagConstraints的weighty设置为1，表示纵向扩展比例为1
        gbc.weighty=1;

        //13.把button数组中第5个按钮添加到frame中
        addComponent(frame,bs[4],gbl,gbc);

        //14.把GridBagConstaints的gridheight和gridwidth设置为2，表示纵向和横向会占用两个网格
        gbc.gridheight=2;
        gbc.gridwidth=2;

        //15.把button数组中第6个按钮添加到frame中
        addComponent(frame,bs[5],gbl,gbc);

        //16.把GridBagConstaints的gridheight和gridwidth设置为1，表示纵向会占用1个网格
        gbc.gridwidth=1;
        gbc.gridheight=1;
        //17.把button数组中第7个按钮添加到frame中
        addComponent(frame,bs[6],gbl,gbc);

        //18.把GridBagConstraints的gridwidth设置为GridBagConstraints.REMAINDER,则表明当前组件是横向最后一个组件
        gbc.gridwidth=GridBagConstraints.REMAINDER;

        //19.把button数组中第8个按钮添加到frame中
        addComponent(frame,bs[7],gbl,gbc);

        //20.把GridBagConstaints的gridwidth设置为1，表示纵向会占用1个网格
        gbc.gridwidth=1;

        //21.把button数组中第9、10个按钮添加到frame中
        addComponent(frame,bs[8],gbl,gbc);
        addComponent(frame,bs[9],gbl,gbc);

        //22.设置frame为最佳大小
        frame.pack();

        //23.设置frame可见
        frame.setVisible(true);
    }

    public static void addComponent(Container container,Component c,GridBagLayout gridBagLayout,GridBagConstraints gridBagConstraints){
        gridBagLayout.setConstraints(c,gridBagConstraints);
        container.add(c);
    }
}
```



### 2.4.5 CardLayout

CardLayout 布局管理器以时间而非空间来管理它里面的组件，它将加入容器的所有组件看成一叠卡片（每个卡片其实就是一个组件），每次只有最上面的那个 Component 才可见。就好像一副扑克牌，它们叠在一起，每次只有最上面的一张扑克牌才可见.

| 方法名称                          | 方法功能                                                     |
| --------------------------------- | ------------------------------------------------------------ |
| CardLayout()                      | 创建默认的 CardLayout 布局管理器。                           |
| CardLayout(int hgap,int vgap)     | 通过指定卡片与容器左右边界的间距 C hgap) 、上下边界 Cvgap) 的间距来创建 CardLayout 布局管理器. |
| first(Container target)           | 显示target 容器中的第一张卡片.                               |
| last(Container target)            | 显示target 容器中的最后一张卡片.                             |
| previous(Container target)        | 显示target 容器中的前一张卡片.                               |
| next(Container target)            | 显示target 容器中的后一张卡片.                               |
| show(Container taget,String name) | 显 示 target 容器中指定名字的卡片.                           |

**案例：**

​	使用Frame和Panel以及CardLayout完成下图中的效果，点击底部的按钮，切换卡片

​	![](./images/CardLayout.jpg)

​	

**演示代码：**

```java
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class CardLayoutDemo {

    public static void main(String[] args) {
        //1.创建Frame对象
        Frame frame = new Frame("这里测试CardLayout");

        //2.创建一个String数组，存储不同卡片的名字
        String[] names = {"第一张","第二张","第三张","第四张","第五张"};

        //3.创建一个Panel容器p1，并设置其布局管理器为CardLayout,用来存放多张卡片
        CardLayout cardLayout = new CardLayout();
        Panel p1 = new Panel();
        p1.setLayout(cardLayout);

        //4.往p1中存储5个Button按钮，名字从String数组中取
        for (int i = 0; i < 5; i++) {
            p1.add(names[i],new Button(names[i]));
        }

        //5.创建一个Panel容器p2,用来存储5个按钮，完成卡片的切换
        Panel p2 = new Panel();

        //6.创建5个按钮，并给按钮设置监听器
        ActionListener listener = new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String command = e.getActionCommand();
                switch (command){
                    case "上一张":
                        cardLayout.previous(p1);
                        break;
                    case "下一张":
                        cardLayout.next(p1);
                        break;
                    case "第一张":
                        cardLayout.first(p1);
                        break;
                    case "最后一张":
                        cardLayout.last(p1);
                        break;
                    case "第三张":
                        cardLayout.show(p1,"第三张");
                        break;
                }
            }
        };

        Button b1 = new Button("上一张");
        Button b2 = new Button("下一张");
        Button b3 = new Button("第一张");
        Button b4 = new Button("最后一张");
        Button b5 = new Button("第三张");
        b1.addActionListener(listener);
        b2.addActionListener(listener);
        b3.addActionListener(listener);
        b4.addActionListener(listener);
        b5.addActionListener(listener);

        //7.把5个按钮添加到p2中
        p2.add(b1);
        p2.add(b2);
        p2.add(b3);
        p2.add(b4);
        p2.add(b5);


        //8.把p1添加到frame的中间区域
        frame.add(p1);


        //9.把p2添加到frame的底部区域
        frame.add(p2,BorderLayout.SOUTH);

        //10设置frame最佳大小并可见
        frame.pack();
        frame.setVisible(true);
    }
}

```

### 2.4.6 BoxLayout

为了简化开发，Swing 引入了 一个新的布局管理器 : BoxLayout 。 BoxLayout 可以在垂直和 水平两个方向上摆放 GUI 组件， BoxLayout 提供了如下一个简单的构造器:

| 方法名称                              | 方法功能                                                     |
| ------------------------------------- | ------------------------------------------------------------ |
| BoxLayout(Container target, int axis) | 指定创建基于 target 容器的 BoxLayout 布局管理器，该布局管理器里的组件按 axis 方向排列。其中 axis 有 BoxLayout.X_AXIS( 横向)和 BoxLayout.Y _AXIS (纵向〉两个方向。 |

**案例1：**

​	使用Frame和BoxLayout完成下图效果：

![](./images/BoxLayout1.jpg)

**演示代码1：**

```java
import javax.swing.*;
import java.awt.*;

public class BoxLayoutDemo1 {

    public static void main(String[] args) {

        //1.创建Frame对象
        Frame frame = new Frame("这里测试BoxLayout");
        //2.创建BoxLayout布局管理器，并指定容器为上面的frame对象，指定组件排列方向为纵向
        BoxLayout boxLayout = new BoxLayout(frame, BoxLayout.Y_AXIS);
        frame.setLayout(boxLayout);

        //3.往frame对象中添加两个按钮
        frame.add(new Button("按钮1"));
        frame.add(new Button("按钮2"));


        //4.设置frame最佳大小，并可见
        frame.pack();
        frame.setVisible(true);
    }
}
```



在java.swing包中，提供了一个新的容器Box，该容器的默认布局管理器就是BoxLayout,大多数情况下，使用Box容器去容纳多个GUI组件，然后再把Box容器作为一个组件，添加到其他的容器中，从而形成整体窗口布局。

| 方法名称                         | 方法功能                           |
| -------------------------------- | ---------------------------------- |
| static Box createHorizontalBox() | 创建一个水平排列组件的 Box 容器 。 |
| static Box createVerticalBox()   | 创建一个垂直排列组件的 Box 容器 。 |

**案例2：**

​	使用Frame和Box，完成下图效果：

​	![](./images/boxlayoutdemo2.jpg)

**演示代码2：**

```java
import javax.swing.*;
import java.awt.*;

public class BoxLayoutDemo2 {

    public static void main(String[] args) {

        //1.创建Frame对象
        Frame frame = new Frame("这里测试BoxLayout");

        //2.创建一个横向的Box,并添加两个按钮
        Box hBox = Box.createHorizontalBox();
        hBox.add(new Button("水平按钮一"));
        hBox.add(new Button("水平按钮二"));

        //3.创建一个纵向的Box，并添加两个按钮
        Box vBox = Box.createVerticalBox();
        vBox.add(new Button("垂直按钮一"));
        vBox.add(new Button("垂直按钮二"));

        //4.把box容器添加到frame容器中
        frame.add(hBox,BorderLayout.NORTH);
        frame.add(vBox);


        //5.设置frame最佳大小并可见

        frame.pack();
        frame.setVisible(true);

    }
}
```

通过之前的两个BoxLayout演示，我们会发现，被它管理的容器中的组件之间是没有间隔的，不是特别的美观，但之前学习的几种布局，组件之间都会有一些间距，那使用BoxLayout如何给组件设置间距呢？

其实很简单，我们只需要在原有的组件需要间隔的地方，添加间隔即可，而每个间隔可以是一个组件，只不过该组件没有内容，仅仅起到一种分隔的作用。

![](./images/BoxLayout3.png)

Box类中，提供了5个方便的静态方法来生成这些间隔组件：

| 方法名称                                          | 方法功能                                                     |
| ------------------------------------------------- | ------------------------------------------------------------ |
| static Component createHorizontalGlue()           | 创建一条水平 Glue (可在两个方向上同时拉伸的间距)             |
| static Component createVerticalGlue()             | 创建一条垂直 Glue (可在两个方向上同时拉伸的间距）            |
| static Component createHorizontalStrut(int width) | 创建一条指定宽度(宽度固定了，不能拉伸)的水平Strut (可在垂直方向上拉伸的间距) |
| static Component createVerticalStrut(int height)  | 创建一条指定高度(高度固定了，不能拉伸)的垂直Strut (可在水平方向上拉伸的间距) |

**案例3：**

使用Frame和Box，完成下图效果：

![](./images/BoxLayout4.jpg)

**演示代码3：**

```java
import javax.swing.*;
import java.awt.*;

public class BoxLayoutDemo3 {

    public static void main(String[] args) {
        //1.创建Frame对象
        Frame frame = new Frame("这里测试BoxLayout");

        //2.创建一个横向的Box,并添加两个按钮
        Box hBox = Box.createHorizontalBox();
        hBox.add(new Button("水平按钮一"));
        hBox.add(Box.createHorizontalGlue());//两个方向都可以拉伸的间隔
        hBox.add(new Button("水平按钮二"));
        hBox.add(Box.createHorizontalStrut(10));//水平间隔固定，垂直间方向可以拉伸
        hBox.add(new Button("水平按钮3"));



        //3.创建一个纵向的Box，并添加两个按钮
        Box vBox = Box.createVerticalBox();
        vBox.add(new Button("垂直按钮一"));
        vBox.add(Box.createVerticalGlue());//两个方向都可以拉伸的间隔
        vBox.add(new Button("垂直按钮二"));
        vBox.add(Box.createVerticalStrut(10));//垂直间隔固定，水平方向可以拉伸
        vBox.add(new Button("垂直按钮三"));


        //4.把box容器添加到frame容器中
        frame.add(hBox, BorderLayout.NORTH);
        frame.add(vBox);


        //5.设置frame最佳大小并可见

        frame.pack();
        frame.setVisible(true);
    }
}
```

## 2.5 AWT中常用组件

### 2.5.1 基本组件

| 组件名        | 功能                                                         |
| ------------- | ------------------------------------------------------------ |
| Button        | Button                                                       |
| Canvas        | 用于绘图的画布                                               |
| Checkbox      | 复选框组件（也可当做单选框组件使用）                         |
| CheckboxGroup | 用于将多个Checkbox 组件组合成一组， 一组 Checkbox 组件将只有一个可以 被选中 ， 即全部变成单选框组件 |
| Choice        | 下拉选择框                                                   |
| Frame         | 窗口 ， 在 GUI 程序里通过该类创建窗口                        |
| Label         | 标签类，用于放置提示性文本                                   |
| List          | JU表框组件，可以添加多项条目                                 |
| Panel         | 不能单独存在基本容器类，必须放到其他容器中                   |
| Scrollbar     | 滑动条组件。如果需要用户输入位于某个范围的值 ， 就可以使用滑动条组件 ，比如调 色板中设置 RGB 的三个值所用的滑动条。当创建一个滑动条时，必须指定它的方向、初始值、 滑块的大小、最小值和最大值。 |
| ScrollPane    | 带水平及垂直滚动条的容器组件                                 |
| TextArea      | 多行文本域                                                   |
| TextField     | 单行文本框                                                   |

这些 AWT 组件的用法比较简单，可以查阅 API 文档来获取它们各自的构方法、成员方法等详细信息。

**案例：** 

​	实现下图效果：

​	![](./images/BasicComponent.jpg)

**演示代码：**

```java
import javax.swing.*;
import java.awt.*;

public class BasicComponentDemo {
    Frame frame = new Frame("这里测试基本组件");

    //定义一个按钮
    Button ok = new Button("确认");

    //定义一个复选框组
    CheckboxGroup cbg = new CheckboxGroup();
    //定义一个单选框，初始处于被选中状态,并添加到cbg组中
    Checkbox male = new Checkbox("男", cbg, true);

    //定义一个单选框，初始处于未被选中状态,并添加到cbg组中
    Checkbox female = new Checkbox("女", cbg, false);

    //定义一个复选框，初始处于未被选中状态
    Checkbox married = new Checkbox("是否已婚？", false);

    //定义一个下拉选择框
    Choice colorChooser = new Choice();

    //定义一个列表选择框
    List colorList = new List(6, true);

    //定义一个5行，20列的多行文本域
    TextArea ta = new TextArea(5, 20);

    //定义一个50列的单行文本域
    TextField tf = new TextField(50);

    public void init() {
        //往下拉选择框中添加内容
        colorChooser.add("红色");
        colorChooser.add("绿色");
        colorChooser.add("蓝色");

        //往列表选择框中添加内容
        colorList.add("红色");
        colorList.add("绿色");
        colorList.add("蓝色");

        //创建一个装载按钮和文本框的Panel容器
        Panel bottom = new Panel();
        bottom.add(tf);
        bottom.add(ok);

        //把bottom添加到Frame的底部
        frame.add(bottom,BorderLayout.SOUTH);

        //创建一个Panel容器，装载下拉选择框，单选框和复选框
        Panel checkPanel = new Panel();
        checkPanel.add(colorChooser);
        checkPanel.add(male);
        checkPanel.add(female);
        checkPanel.add(married);

        //创建一个垂直排列的Box容器，装载 多行文本域和checkPanel
        Box topLeft = Box.createVerticalBox();
        topLeft.add(ta);
        topLeft.add(checkPanel);

        //创建一个水平排列的Box容器，装载topLeft和列表选择框
        Box top = Box.createHorizontalBox();
        top.add(topLeft);
        top.add(colorList);

        //将top添加到frame的中间区域
        frame.add(top);


        //设置frame最佳大小并可见
        frame.pack();
        frame.setVisible(true);
    }

    public static void main(String[] args) {

        new BasicComponentDemo().init();

    }
}

```

### 2.5.2 对话框Dialog

#### 2.5.2.1 Dialog

Dialog 是 Window 类的子类，是 一个容器类，属于特殊组件 。 对话框是可以独立存在的顶级窗口， 因此用法与普通窗口的用法几乎完全一样，但是使用对话框需要注意下面两点：

- 对话框通常依赖于其他窗口，就是通常需要有一个父窗口；
- 对话框有非模式(non-modal)和模式(modal)两种，当某个模式对话框被打开后，该模式对话框总是位于它的父窗口之上，在模式对话框被关闭之前，父窗口无法获得焦点。

| 方法名称                                         | 方法功能                                                     |
| ------------------------------------------------ | ------------------------------------------------------------ |
| Dialog(Frame owner, String title, boolean modal) | 创建一个对话框对象：<br/>owner:当前对话框的父窗口<br/>title:当前对话框的标题<br/>modal：当前对话框是否是模式对话框，true/false |

**案例1：**

​	通过Frame、Button、Dialog实现下图效果:

​	![](./images/DialogDemo1.jpg)



**演示代码1：**

```java
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class DialogDemo1 {

    public static void main(String[] args) {

        Frame frame = new Frame("这里测试Dialog");

        Dialog d1 = new Dialog(frame, "模式对话框", true);
        Dialog d2 = new Dialog(frame, "非模式对话框", false);

        Button b1 = new Button("打开模式对话框");
        Button b2 = new Button("打开非模式对话框");

        //设置对话框的大小和位置
        d1.setBounds(20,30,300,400);
        d2.setBounds(20,30,300,400);

        //给b1和b2绑定监听事件
        b1.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                d1.setVisible(true);
            }
        });
        b2.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                d2.setVisible(true);
            }
        });

        //把按钮添加到frame中
        frame.add(b1);
        frame.add(b2,BorderLayout.SOUTH);

        //设置frame最佳大小并可见
        frame.pack();
        frame.setVisible(true);

    }
}
```

在Dialog对话框中，可以根据需求，自定义内容

**案例：**

​	点击按钮，弹出一个模式对话框，其内容如下:

​	![](./images/DialogDemo2.jpg)

**演示代码：**

```java
public class DialogDemo2 {

    public static void main(String[] args) {

        Frame frame = new Frame("这里测试Dialog");

        Dialog d1 = new Dialog(frame, "模式对话框", true);

        //往对话框中添加内容
        Box vBox = Box.createVerticalBox();

        vBox.add(new TextField(15));
        vBox.add(new JButton("确认"));
        d1.add(vBox);

        Button b1 = new Button("打开模式对话框");

        //设置对话框的大小和位置
        d1.setBounds(20,30,200,100);


        //给b1绑定监听事件
        b1.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                d1.setVisible(true);
            }
        });


        //把按钮添加到frame中
        frame.add(b1);

        //设置frame最佳大小并可见
        frame.pack();
        frame.setVisible(true);

    }
}
```



#### 2.5.2.1 FileDialog

Dialog 类还有 一个子类 : FileDialog ，它代表一个文件对话框，用于打开或者保存 文件,需要注意的是FileDialog无法指定模态或者非模态，这是因为 FileDialog 依赖于运行平台的实现，如果运行平台的文件对话框是模态的，那么 FileDialog 也是模态的;否则就是非模态的 。

| 方法名称                                         | 方法功能                                                     |
| ------------------------------------------------ | ------------------------------------------------------------ |
| FileDialog(Frame parent, String title, int mode) | 创建一个文件对话框：<br/>parent:指定父窗口<br/>title:对话框标题<br/>mode:文件对话框类型，如果指定为FileDialog.load，用于打开文件，如果指定为FileDialog.SAVE,用于保存文件 |
| String getDirectory()                            | 获取被打开或保存文件的绝对路径                               |
| String getFile()                                 | 获取被打开或保存文件的文件名                                 |

**案例2：**

​	使用 Frame、Button和FileDialog完成下图效果：

​	![](./images/FileDialog.jpg)



**演示代码2：**

```java
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class FileDialogTest {

    public static void main(String[] args) {

        Frame frame = new Frame("这里测试FileDialog");

        FileDialog d1 = new FileDialog(frame, "选择需要加载的文件", FileDialog.LOAD);
        FileDialog d2 = new FileDialog(frame, "选择需要保存的文件", FileDialog.SAVE);

        Button b1 = new Button("打开文件");
        Button b2 = new Button("保存文件");

        //给按钮添加事件
        b1.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                d1.setVisible(true);
                //打印用户选择的文件路径和名称
                System.out.println("用户选择的文件路径:"+d1.getDirectory());
                System.out.println("用户选择的文件名称:"+d1.getFile());
            }
        });

        System.out.println("-------------------------------");
        b2.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                d2.setVisible(true);
                //打印用户选择的文件路径和名称
                System.out.println("用户选择的文件路径:"+d2.getDirectory());
                System.out.println("用户选择的文件名称:"+d2.getFile());
            }
        });

        //添加按钮到frame中

        frame.add(b1);
        frame.add(b2,BorderLayout.SOUTH);

        //设置frame最佳大小并可见
        frame.pack();
        frame.setVisible(true);
    }
}
```

## 2.6 事件处理

前面介绍了如何放置各种组件，从而得到了丰富多彩的图形界面，但这些界面还不能响应用户的任何操作。比如单击前面所有窗口右上角的“X”按钮，但窗口依然不会关闭。因为在 AWT 编程中 ，所有用户的操作，都必须都需要经过一套事件处理机制来完成，而 Frame 和组件本身并没有事件处理能力 。

### 2.6.1 GUI事件处理机制

**定义：**

​	当在某个组件上发生某些操作的时候，会自动的触发一段代码的执行。

在GUI事件处理机制中涉及到4个重要的概念需要理解：

**事件源(Event Source)**：操作发生的场所，通常指某个组件，例如按钮、窗口等；
**事件（Event）**：在事件源上发生的操作可以叫做事件，GUI会把事件都封装到一个Event对象中，如果需要知道该事件的详细信息，就可以通过Event对象来获取。
**事件监听器(Event Listener)**:当在某个事件源上发生了某个事件，事件监听器就可以对这个事件进行处理。

**注册监听**：把某个事件监听器(A)通过某个事件(B)绑定到某个事件源(C)上，当在事件源C上发生了事件B之后，那么事件监听器A的代码就会自动执行。

![](./images/事件处理机制.png)

**使用步骤：**

1.创建事件源组件对象；

2.自定义类，实现XxxListener接口，重写方法；

3.创建事件监听器对象(自定义类对象)

4.调用事件源组件对象的addXxxListener方法完成注册监听

**案例：**

​	完成下图效果，点击确定按钮，在单行文本域内显示 hello world:

​	![](./images/EventDemo1.jpg)

​	

**演示代码：**

```java
public class EventDemo1 {
    Frame  frame = new Frame("这里测试事件处理");

    //事件源
    Button button = new Button("确定");

    TextField tf = new TextField(30);
    public void init(){
        //注册监听
        button.addActionListener(new MyActionListener());

        //添加组件到frame中
        frame.add(tf);
        frame.add(button,BorderLayout.SOUTH);

        //设置frame最佳大小并可见
        frame.pack();
        frame.setVisible(true);
    }

    //自定义事件监听器类
    private  class MyActionListener implements ActionListener{

        @Override
        public void actionPerformed(ActionEvent e) {

            System.out.println("用户点击了确定按钮");
            tf.setText("hello world");
        }
    }
    
    public static void main(String[] args) {
        new EventDemo1().init();
    }
}
```

### 2.6.2 GUI中常见事件和事件监听器

事件监听器必须实现事件监听器接口， AWT 提供了大量的事件监听器接口用于实现不同类型的事件监听器，用于监听不同类型的事件 。 AWT 中提供了丰富的事件类，用于封装不同组件上所发生的特定操作， AWT 的事件类都是 AWTEvent 类的子类 ， AWTEvent是 EventObject 的子类。

#### 2.6.2.1 事件

AWT把事件分为了两大类：

​	1.低级事件：这类事件是基于某个特定动作的事件。比如进入、点击、拖放等动作的鼠标事件，再比如得到焦点和失去焦点等焦点事件。

| 事件           | 触发时机                                                     |
| -------------- | ------------------------------------------------------------ |
| ComponentEvent | 组件事件 ， 当 组件尺寸发生变化、位置发生移动、显示/隐藏状态发生改变时触发该事件。 |
| ContainerEvent | 容器事件 ， 当容器里发生添加组件、删除组件时触发该事件 。    |
| WindowEvent    | 窗口事件， 当窗 口状态发生改变 ( 如打开、关闭、最大化、最 小化)时触发该事件 。 |
| FocusEvent     | 焦点事件 ， 当组件得到焦点或失去焦点 时触发该事件 。         |
| KeyEvent       | 键盘事件 ， 当按键被按下、松开、单击时触发该事件。           |
| MouseEvent     | 鼠标事件，当进行单击、按下、松开、移动鼠标等动作 时触发该事件。 |
| PaintEvent     | 组件绘制事件 ， 该事件是一个特殊的事件类型 ， 当 GUI 组件调 用 update/paint 方法 来呈现自身时触发该事件，该事件并非专用于事件处理模型 。 |

​	2.高级事件：这类事件并不会基于某个特定动作，而是根据功能含义定义的事件。

| 事件           | 触发时机                                                     |
| -------------- | ------------------------------------------------------------ |
| ActionEvent    | 动作事件 ，当按钮、菜单项被单击，在 TextField 中按 Enter 键时触发 |
| AjustmentEvent | 调节事件，在滑动条上移动滑块以调节数值时触发该事件。         |
| ltemEvent      | 选项事件，当用户选中某项， 或取消选中某项时触发该事件 。     |
| TextEvent      | 文本事件， 当文本框、文本域里的文本发生改变时触发该事件。    |

#### 2.6.2 事件监听器

不同的事件需要使用不同的监听器监听，不同的监听器需要实现不同的监听器接口， 当指定事件发生后 ， 事件监听器就会调用所包含的事件处理器(实例方法)来处理事件 。

| 事件类别        | 描述信息                 | 监听器接口名        |
| --------------- | ------------------------ | ------------------- |
| ActionEvent     | 激活组件                 | ActionListener      |
| ItemEvent       | 选择了某些项目           | ItemListener        |
| MouseEvent      | 鼠标移动                 | MouseMotionListener |
| MouseEvent      | 鼠标点击等               | MouseListener       |
| KeyEvent        | 键盘输入                 | KeyListener         |
| FocusEvent      | 组件收到或失去焦点       | FocusListener       |
| AdjustmentEvent | 移动了滚动条等组件       | AdjustmentListener  |
| ComponentEvent  | 对象移动缩放显示隐藏等   | ComponentListener   |
| WindowEvent     | 窗口收到窗口级事件       | WindowListener      |
| ContainerEvent  | 容器中增加删除了组件     | ContainerListener   |
| TextEvent       | 文本字段或文本区发生改变 | TextListener        |

### 2.6.3 案例

**案例一：**

​	通过ContainerListener监听Frame容器添加组件；

​	通过TextListener监听TextFiled内容变化；

​	通过ItemListener监听Choice条目选中状态变化；

​	![](./images/ListenerDemo1.jpg)

**演示代码一:**

```java
import java.awt.*;
import java.awt.event.ContainerAdapter;
import java.awt.event.ContainerEvent;
import java.awt.event.TextEvent;
import java.awt.event.TextListener;

public class ListenerDemo1 {

    public static void main(String[] args) {
        Frame frame = new Frame("这里测试监听器");

        //创建一个单行文本域
        TextField tf = new TextField(30);

        //给文本域添加TextListener，监听内容的变化
        tf.addTextListener(new TextListener() {
            @Override
            public void textValueChanged(TextEvent e) {
                System.out.println("当前内容："+tf.getText());;
            }
        });


        //给frame注册ContainerListener监听器，监听容器中组件的添加
        frame.addContainerListener(new ContainerAdapter() {
            @Override
            public void componentAdded(ContainerEvent e) {
                Component child = e.getChild();
                System.out.println("容器中添加了新组件："+child);
            }
        });


        //添加tf到frame
        frame.add(tf);

        //设置frame最佳大小并可见
        frame.pack();
        frame.setVisible(true);
    }
}
```



**案例2：**

​	给Frame设置WindowListner，监听用户点击 X 的动作，如果用户点击X，则关闭当前窗口



**演示代码2：**

```java
import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;

public class ListenerDemo2 {

    public static void main(String[] args) {

        Frame frame = new Frame("这里测试WindowListener");



        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });

        frame.setBounds(200,200,500,300);

        frame.setVisible(true);
    }
}
```

## 2.7 菜单组件

​	前面讲解了如果构建GUI界面，其实就是把一些GUI的组件，按照一定的布局放入到容器中展示就可以了。在实际开发中，除了主界面，还有一类比较重要的内容就是菜单相关组件，可以通过菜单相关组件很方便的使用特定的功能，在AWT中，菜单相关组件的使用和之前学习的组件是一模一样的，只需要把菜单条、菜单、菜单项组合到一起，按照一定的布局，放入到容器中即可。

![](./images/菜单1.png)



**下表中给出常见的菜单相关组件：**

| 菜单组件名称     | 功能                                                         |
| ---------------- | ------------------------------------------------------------ |
| MenuBar          | 菜单条 ， 菜单的容器 。                                      |
| Menu             | 菜单组件 ， 菜单项的容器 。 它也是Menultem的子类 ，所以可作为菜单项使用 |
| PopupMenu        | 上下文菜单组件(右键菜单组件)                                 |
| Menultem         | 菜单项组件 。                                                |
| CheckboxMenuItem | 复选框菜单项组件                                             |

**下图是常见菜单相关组件集成体系图：**

​	![](./images/菜单项组件继承体系.png)

**菜单相关组件使用：**

1.准备菜单项组件，这些组件可以是MenuItem及其子类对象

2.准备菜单组件Menu或者PopupMenu(右击弹出子菜单)，把第一步中准备好的菜单项组件添加进来；

3.准备菜单条组件MenuBar，把第二步中准备好的菜单组件Menu添加进来；

4.把第三步中准备好的菜单条组件添加到窗口对象中显示。



**小技巧：**

1.如果要在某个菜单的菜单项之间添加分割线，那么只需要调用Menu的add（new MenuItem(-)）即可。

2.如果要给某个菜单项关联快捷键功能，那么只需要在创建菜单项对象时设置即可，例如给菜单项关联 ctrl+shif+/ 快捷键，只需要：new MenuItem("菜单项名字",new MenuShortcut(KeyEvent.VK_Q,true);

**案例1：**

​	使用awt中常用菜单组件，完成下图效果

​	![](./images/菜单1.png)



**演示代码1：**

```java
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class SimpleMenu {
    //创建窗口
    private Frame frame = new Frame("这里测试菜单相关组件");
    //创建菜单条组件
    private MenuBar menuBar = new MenuBar();
    //创建文件菜单组件
    private Menu fileMenu = new Menu("文件");
    //创建编辑菜单组件
    private Menu editMenu = new Menu("编辑");
    //创建新建菜单项
    private MenuItem newItem = new MenuItem("新建");
    //创建保存菜单项
    private MenuItem saveItem = new MenuItem("保存");
    //创建退出菜单项
    private MenuItem exitItem = new MenuItem("退出");

    //创建自动换行选择框菜单项
    private CheckboxMenuItem autoWrap = new CheckboxMenuItem("自动换行");

    //创建复制菜单项
    private MenuItem copyItem = new MenuItem("复制");

    //创建粘贴菜单项
    private MenuItem pasteItem = new MenuItem("粘贴");

    //创建格式菜单
    private Menu formatMenu = new Menu("格式");

    //创建注释菜单项
    private MenuItem commentItem = new MenuItem("注释");
    //创建取消注释菜单项
    private MenuItem cancelItem = new MenuItem("取消注释");

    //创建一个文本域
    private TextArea ta = new TextArea(6, 40);

    public void init(){


        //定义菜单事件监听器
        ActionListener listener = new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String command = e.getActionCommand();
                ta.append("单击“"+command+"”菜单\n");
                if (command.equals("退出")){
                    System.exit(0);
                }
            }
        };

        //为注释菜单项和退出菜单项注册监听器
        commentItem.addActionListener(listener);
        exitItem.addActionListener(listener);

        //为文件菜单fileMenu添加菜单项
        fileMenu.add(newItem);
        fileMenu.add(saveItem);
        fileMenu.add(exitItem);

        //为编辑菜单editMenu添加菜单项
        editMenu.add(autoWrap);
        editMenu.add(copyItem);
        editMenu.add(pasteItem);

        //为格式化菜单formatMenu添加菜单项
        formatMenu.add(commentItem);
        formatMenu.add(cancelItem);

        //将格式化菜单添加到编辑菜单中，作为二级菜单
        editMenu.add(new MenuItem("-"));
        editMenu.add(formatMenu);


        //将文件菜单和编辑菜单添加到菜单条中
        menuBar.add(fileMenu);
        menuBar.add(editMenu);


        //把菜单条设置到frame窗口上
        frame.setMenuBar(menuBar);

        //把文本域添加到frame中
        frame.add(ta);

        //设置frame最佳大小并可见
        frame.pack();
        frame.setVisible(true);
    }


    public static void main(String[] args) {
        new SimpleMenu().init();
    }
}

```

**案例2：**

​	通过PopupMenu实现下图效果：

​	![](./images/菜单2.png)

**实现思路：**

1.创建PopubMenu菜单组件；

2.创建多个MenuItem菜单项，并添加到PopupMenu中；

3.将PopupMenu添加到目标组件中；

4.为需要右击出现PopubMenu菜单的组件，注册鼠标监听事件，当监听到用户释放右键时，弹出菜单。



**演示代码2：**

```java
import java.awt.*;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;

public class PopupMenuTest {

    private Frame frame = new Frame("这里测试PopupMenu");

    //创建PopubMenu菜单
    private PopupMenu popupMenu = new PopupMenu();

    //创建菜单条

    private MenuItem commentItem = new MenuItem("注释");
    private MenuItem cancelItem = new MenuItem("取消注释");
    private MenuItem copyItem = new MenuItem("复制");
    private MenuItem pasteItem = new MenuItem("保存");


    //创建一个文本域
    private TextArea ta = new TextArea("我爱中华！！！", 6, 40);

    //创建一个Panel
    private  Panel panel = new Panel();

    public void init(){

        //把菜单项添加到PopupMenu中
        popupMenu.add(commentItem);
        popupMenu.add(cancelItem);
        popupMenu.add(copyItem);
        popupMenu.add(pasteItem);

        //设置panel大小
        panel.setPreferredSize(new Dimension(300,100));

        //把PopupMenu添加到panel中
        panel.add(popupMenu);

        //为panel注册鼠标事件
        panel.addMouseListener(new MouseAdapter() {
            @Override
            public void mouseReleased(MouseEvent e) {
                boolean flag = e.isPopupTrigger();
                //判断当前鼠标操作是不是触发PopupMenu的操作
                if (flag){
                    //让PopupMenu显示在panel上，并且跟随鼠标事件发生的地方显示
                    popupMenu.show(panel,e.getX(),e.getY());
                }
            }
        });

        //把ta添加到frame中间区域中

        frame.add(ta);

        //把panel添加到frame底部
        frame.add(panel,BorderLayout.SOUTH);

        //设置frame最佳大小，并可视；
        frame.pack();
        frame.setVisible(true);

    }

    public static void main(String[] args) {
        new PopupMenuTest().init();
    }

}
```



## 2.8 绘图

​	很多程序如各种小游戏都需要在窗口中绘制各种图形，除此之外，即使在开发JavaEE项目时， 有 时候也必须"动态"地向客户 端生成各种图形、图表，比如 图形验证码、统计图等，这都需要利用AWT的绘图功能。

### 2.8.1 组件绘图原理

​	之前我们已经学习过很多组件，例如Button、Frame、Checkbox等等，不同的组件，展示出来的图形都不一样，其实这些组件展示出来的图形，其本质就是用AWT的绘图来完成的。

​	在AWT中，真正提供绘图功能的是Graphics对象，那么Component组件和Graphics对象存在什么关系，才能让Component绘制自身图形呢？在Component类中，提供了下列三个方法来完成组件图形的绘制与刷新：

​	paint(Graphics g):绘制组件的外观；

​	update(Graphics g):内部调用paint方法，刷新组件外观；

​	repaint():调用update方法，刷新组件外观；

​	![](./images/组件绘制图形流程.png)

​	一般情况下，update和paint方法是由AWT系统负责调用，如果程序要希望系统重新绘制组件，可以调用repaint方法完成。

### 2.8.2 Graphics类的使用

​	实际生活中如果需要画图，首先我们得准备一张纸，然后在拿一支画笔，配和一些颜色，就可以在纸上画出来各种各样的图形，例如圆圈、矩形等等。

​	![](./images/画图示意.jpg)

程序中绘图也一样，也需要画布，画笔，颜料等等。AWT中提供了Canvas类充当画布，提供了Graphics类来充当画笔，通过调用Graphics对象的setColor()方法可以给画笔设置颜色。

**画图的步骤：**

1.自定义类，继承Canvas类，重写paint(Graphics g)方法完成画图；

2.在paint方法内部，真正开始画图之前调用Graphics对象的setColor()、setFont()等方法设置画笔的颜色、字体等属性；

3.调用Graphics画笔的drawXxx()方法开始画图。



其实画图的核心就在于使用Graphics画笔在Canvas画布上画出什么颜色、什么样式的图形，所以核心在画笔上，下表中列出了Graphics类中常用的一些方法：

| 方法名称           | 方法功能               |
| ------------------ | ---------------------- |
| setColor(Color c)  | 设置颜色               |
| setFont(Font font) | 设置字体               |
| drawLine()         | 绘制直线               |
| drawRect()         | 绘制矩形               |
| drawRoundRect()    | 绘制圆角矩形           |
| drawOval()         | 绘制椭圆形             |
| drawPolygon()      | 绘制多边形             |
| drawArc()          | 绘制圆弧               |
| drawPolyline()     | 绘制折线               |
| fillRect()         | 填充矩形区域           |
| fillRoundRect()    | 填充圆角矩形区域       |
| fillOval()         | 填充椭圆区域           |
| fillPolygon()      | 填充多边形区域         |
| fillArc()          | 填充圆弧对应的扇形区域 |
| drawImage()        | 绘制位图               |

**案例：**

​	使用AWT绘图API，完成下图效果

​	![](./images/画图演示1.jpg)

**演示代码：**

```java
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.Random;

public class SimpleDraw {

    private final String RECT_SHAPE="rect";
    private final String OVAL_SHAPE="oval";

    private Frame frame = new Frame("这里测试绘图");

    private Button drawRectBtn = new Button("绘制矩形");
    private Button drawOvalBtn = new Button("绘制椭圆");

    //用来保存当前用户需要绘制什么样的图形
    private String shape="";

    private MyCanvas drawArea = new MyCanvas();




    public void init(){

        //为按钮添加点击事件
        drawRectBtn.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                shape = RECT_SHAPE;
                drawArea.repaint();
            }
        });

        drawOvalBtn.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                shape = OVAL_SHAPE;
                drawArea.repaint();
            }
        });

        //定义一个Panel，装载两个按钮
        Panel p = new Panel();
        p.add(drawRectBtn);
        p.add(drawOvalBtn);

        //把panel添加到frame底部
        frame.add(p,BorderLayout.SOUTH);
        
        //设置画布的大小
        drawArea.setPreferredSize(new Dimension(300,200));
        //把画布添加到frame中

        frame.add(drawArea);

        frame.pack();
        frame.setVisible(true);


    }

    public static void main(String[] args) {
        new SimpleDraw().init();
    }


    //1.自定义类，继承Canvas类，重写paint方法

    private class MyCanvas extends Canvas{
        @Override
        public void paint(Graphics g) {
            Random r = new Random();

            if (shape.equals(RECT_SHAPE)){
                //绘制矩形
                g.setColor(Color.BLACK);
                g.drawRect(r.nextInt(200),r.nextInt(100),40,60);
            }

            if(shape.equals(OVAL_SHAPE)){
                //绘制椭圆
                g.setColor(Color.RED);
                g.drawOval(r.nextInt(200),r.nextInt(100),60,40);
            }

        }
    }
}

```

​	

​	Java也可用于开发一些动画。所谓动画，就是间隔一定的时间(通常小于0 . 1秒 )重新绘制新的图像，两次绘制的图像之间差异较小，肉眼看起来就成了所谓的动画 。

​	为了实现间隔一定的时间就重新调用组件的 repaint()方法，可以借助于 Swing 提供的Timer类，Timer类是一个定时器， 它有如下一个构造器 ：
Timer(int delay, ActionListener listener): 每间隔 delay 毫秒，系统自动触发 ActionListener 监听器里的事件处理器方法，在方法内部我们就可以调用组件的repaint方法，完成组件重绘。



**案例2：**

​	使用AWT画图技术及Timer定时器，完成下图中弹球小游戏。

​	![](./images/小球运行.png) ![](./images/小球结束.png)

**演示代码2：**

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class PinBall {

    //桌面宽度
    private final int TABLE_WIDTH = 300;
    //桌面高度
    private final int TABLE_HEIGHT = 400;


    //球拍的高度和宽度
    private final int RACKET_WIDTH = 60;
    private final int RACKET_HEIGHT = 20;

    //小球的大小
    private final int BALL_SIZE = 16;

    //定义小球纵向运行速度
    private int ySpeed = 10;
    //小球横向运行速度
    private int xSpeed = 5;

    //定义小球的初始坐标
    private int ballX = 120;
    private int ballY = 20;

    //定义球拍的初始坐标，x坐标会发生变化，y坐标不会发生变化
    private int rackeX = 120;
    private final int RACKET_Y = 340;

    //声明定时器
    private Timer timer;

    //定义游戏结束的标记
    private boolean isLose = false;

    //声明一个桌面
    private MyCanvas tableArea = new MyCanvas();

    //创建窗口对象
    private Frame frame = new Frame("弹球游戏");

    public void init(){
        //设置桌面区域的最佳大小
        tableArea.setPreferredSize(new Dimension(TABLE_WIDTH,TABLE_HEIGHT));
        //把桌面添加到frame中
        frame.add(tableArea);

        //定义键盘监听器
        KeyListener keyListener = new KeyAdapter(){

            //监听键盘 ←  → 按下操作，当指定的键按下时，球拍的水平坐标分别会增加或者减少
            @Override
            public void keyPressed(KeyEvent e) {
                int keyCode = e.getKeyCode();
                if (keyCode==KeyEvent.VK_LEFT){//←
                    //没有到左边界，可以继续向左移动
                    if (rackeX>0){
                        rackeX-=10;
                    }
                }

                if (keyCode==KeyEvent.VK_RIGHT){//→
                    //没有到右边界，可以继续向右移动
                    if (rackeX<TABLE_WIDTH-RACKET_WIDTH){
                        rackeX+=10;
                    }
                }
            }
        };

        //为窗口和tableArea分别添加键盘事件
        frame.addKeyListener(keyListener);
        tableArea.addKeyListener(keyListener);

        //定义ActionListener，用来监听小球的变化情况
        ActionListener timerTask = new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                //小球碰到左右边框
                if (ballX<=0 || ballX>=TABLE_WIDTH-BALL_SIZE){
                    xSpeed=-xSpeed;
                }
                //小球的高度超出了球拍的位置，且横向不在球拍范围内，则游戏结束
                if (ballY > RACKET_Y && (ballX<rackeX || ballX>rackeX+RACKET_WIDTH)){
                    //结束定时器
                    timer.stop();
                    //把游戏结束的标记设置为true
                    isLose = true;
                    //重绘界面
                    tableArea.repaint();

                }
                //如果小球横向在球拍范围内，且到达球拍位置或者到达顶端位置，则小球反弹
                if (ballY<=0 || (ballY>=RACKET_Y-BALL_SIZE && ballX>=rackeX && ballX<=rackeX+RACKET_WIDTH)){
                    ySpeed=-ySpeed;
                }

                //更新小球的坐标
                ballX+=xSpeed;
                ballY+=ySpeed;

                //重绘桌面
                tableArea.repaint();
            }
        };

        //设置定时器，定时任务就是timerTask
        timer = new Timer(100,timerTask);
        timer.start();

        //设置frame最佳大小，并可视

        frame.pack();
        frame.setVisible(true);


    }

    public static void main(String[] args) {
        new PinBall().init();
    }

    private class MyCanvas extends Canvas{

        //重写paint方法，实现绘图
        @Override
        public void paint(Graphics g) {
            //判断游戏是否结束
            if (isLose){//结束
                g.setColor(Color.BLUE);
                g.setFont(new Font("Times",Font.BOLD,30));
                g.drawString("游戏结束！",50,200);
            }else{//没有结束

                //设置颜色并绘制小球
                g.setColor(Color.RED);
                g.fillOval(ballX,ballY,BALL_SIZE,BALL_SIZE);

                //设置颜色并绘制球拍
                g.setColor(Color.PINK);
                g.fillRect(rackeX,RACKET_Y,RACKET_WIDTH,RACKET_HEIGHT);
            }

        }
    }
}
```

### 2.8.3 处理位图

​	如果仅仅绘制一些简单的几何图形，程序的图形效果依然比较单调 。 AWT 也允许在组件上绘制位图， Graphics 提供了 drawlmage() 方法用于绘制位图，该方法需要一个Image参数一一代表位图，通过该方法就可 以绘制出指定的位图 。

**位图使用步骤：**

1.创建Image的子类对象BufferedImage(int width,int height,int ImageType),创建时需要指定位图的宽高及类型属性；此时相当于在内存中生成了一张图片；

2.调用BufferedImage对象的getGraphics()方法获取画笔，此时就可以往内存中的这张图片上绘图了，绘图的方法和之前学习的一模一样；

3.调用组件的drawImage()方法，一次性的内存中的图片BufferedImage绘制到特定的组件上。

**使用位图绘制组件的好处：**

使用位图来绘制组件，相当于实现了图的缓冲区，此时绘图时没有直接把图形绘制到组件上，而是先绘制到内存中的BufferedImage上，等全部绘制完毕，再一次性的图像显示到组件上即可，这样用户的体验会好一些。

**案例：**

​	通过BufferedImage实现一个简单的手绘程序：通过鼠标可以在窗口中画图。

​	![](./images/手绘程序2.png)

**演示代码：**

```java
import java.awt.*;
import java.awt.event.*;
import java.awt.image.BufferedImage;

public class HandDraw {

    //定义画图区的宽高
    private final int AREA_WIDTH = 500;
    private final int AREA_HEIGHT = 400;

    //定义变量，保存上一次鼠标拖动时，鼠标的坐标
    private int preX = -1;
    private int preY = -1;

    //定义一个右键菜单，用于设置画笔的颜色
    private PopupMenu colorMenu = new PopupMenu();
    private MenuItem redItem = new MenuItem("红色");
    private MenuItem greenItem = new MenuItem("绿色");
    private MenuItem blueItem = new MenuItem("蓝色");

    //定义一个BufferedImage对象
    private BufferedImage image = new BufferedImage(AREA_WIDTH,AREA_HEIGHT,BufferedImage.TYPE_INT_RGB);
    //获取BufferedImage对象关联的画笔
    private Graphics g = image.getGraphics();

    //定义窗口对象
    private Frame frame = new Frame("简单手绘程序");

    //定义画布对象
    private Canvas drawArea =  new Canvas(){
        @Override
        public void paint(Graphics g) {
            //把位图image绘制到0,0坐标点
            g.drawImage(image,0,0,null);
        }
    };

    //定义一个Color对象，用来保存用户设置的画笔颜色,默认为黑色
    private Color forceColor = Color.BLACK;

    public void init(){
        //定义颜色菜单项单击监听器
        ActionListener menuListener = new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String command = e.getActionCommand();
                switch (command){
                    case "红色":
                        forceColor=Color.RED;
                        break;
                    case "绿色":
                        forceColor = Color.GREEN;
                        break;
                    case "蓝色":
                        forceColor = Color.BLUE;
                        break;
                }
            }
        };

        //为三个菜单项添加点击事件
        redItem.addActionListener(menuListener);
        greenItem.addActionListener(menuListener);
        blueItem.addActionListener(menuListener);

        //把菜单项添加到右键菜单中
        colorMenu.add(redItem);
        colorMenu.add(greenItem);
        colorMenu.add(blueItem);

        //把右键菜单添加到绘图区域drawArea
        drawArea.add(colorMenu);

        //将iamge图片背景设置为白色
        g.fillRect(0,0,AREA_WIDTH,AREA_HEIGHT);

        //设置绘图区域drawArea的大小
        drawArea.setPreferredSize(new Dimension(AREA_WIDTH,AREA_HEIGHT));

        //绘图区域drawArea设置鼠标移动监听器
        drawArea.addMouseMotionListener(new MouseMotionAdapter() {
            //用于绘制图像
            @Override
            public void mouseDragged(MouseEvent e) {//按下鼠标键并拖动会触发
                //如果上次鼠标的坐标在绘图区域，才开始绘图
                if (preX>0 && preY>0){
                    //设置当前选中的画笔颜色
                    g.setColor(forceColor);
                    //绘制线条，需要有两组坐标，一组是上一次鼠标拖动鼠标时的坐标，一组是现在鼠标的坐标
                    g.drawLine(preX,preY,e.getX(),e.getY());
                }

                //更新preX和preY
                preX = e.getX();
                preY = e.getY();

                //重新绘制drawArea组件
                drawArea.repaint();

            }
        });

        drawArea.addMouseListener(new MouseAdapter() {

            //用于弹出右键菜单
            @Override
            public void mouseReleased(MouseEvent e) {//松开鼠标键会触发
                boolean popupTrigger = e.isPopupTrigger();
                if (popupTrigger){
                    //把colorMenu显示到drawArea画图区域，并跟随鼠标显示
                    colorMenu.show(drawArea,e.getX(),e.getY());
                }

                //当鼠标松开时，把preX和preY重置为-1
                preX = -1;
                preY = -1;

            }
        });

        //把drawArea添加到frame中
        frame.add(drawArea);

        //设置frame最佳大小并可见
        frame.pack();
        frame.setVisible(true);
    }
    public static void main(String[] args) {
        new HandDraw().init();
    }
}
```

### 2.8.4  ImageIO的使用

在实际生活中，很多软件都支持打开本地磁盘已经存在的图片，然后进行编辑，编辑完毕后，再重新保存到本地磁盘。如果使用AWT要完成这样的功能，那么需要使用到ImageIO这个类，可以操作本地磁盘的图片文件。

| 方法名称                                                     | 方法功能                 |
| ------------------------------------------------------------ | ------------------------ |
| static BufferedImage read(File input)                        | 读取本地磁盘图片文件     |
| static BufferedImage read(InputStream input)                 | 读取本地磁盘图片文件     |
| static boolean write(RenderedImage im, String formatName, File output) | 往本地磁盘中输出图片文件 |

**案例：**

​	编写图片查看程序,支持另存操作

​	![](./images/ImageIODemo.jpg)

**演示代码：**

```java
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;

public class ReadAndSaveImage {

    private Frame frame = new Frame("图片查看器");

    private BufferedImage image;

    private class MyCanvas  extends Canvas{

        @Override
        public void paint(Graphics g) {
            if (image!=null){
                g.drawImage(image,0,0,image.getWidth(),image.getHeight(),null);
            }
        }
    }

    private MyCanvas imageComponent = new MyCanvas();

    public void init() throws Exception{

        //设置菜单项
        MenuBar mb = new MenuBar();
        Menu menu = new Menu("文件");
        MenuItem openItem = new MenuItem("打开");
        MenuItem saveItem = new MenuItem("另存为");

        openItem.addActionListener(e -> {
            //弹出对话框，选择本地图片
            FileDialog oDialog = new FileDialog(frame);
            oDialog.setVisible(true);
            //读取用户选择的图片
            String dir = oDialog.getDirectory();
            String file = oDialog.getFile();
            try {
                image = ImageIO.read(new File(dir,file));

                imageComponent.repaint();

            } catch (IOException e1) {
                e1.printStackTrace();
            }

        });


        saveItem.addActionListener(e -> {
            //弹出对话框，另存为
            FileDialog sDialog = new FileDialog(frame,"保存图片",FileDialog.SAVE);
            sDialog.setVisible(true);
            String dir = sDialog.getDirectory();
            String file = sDialog.getFile();

            try {
                ImageIO.write(image,"JPEG",new File(dir,file));
            } catch (IOException e1) {
                e1.printStackTrace();
            }
        });

        mb.add(menu);
        menu.add(openItem);
        menu.add(saveItem);

        frame.setMenuBar(mb);
        frame.add(imageComponent);

        frame.setBounds(200,200,800,600);

        frame.setVisible(true);

        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });
    }



    public static void main(String[] args) throws Exception {
        new ReadAndSaveImage().init();
    }
}
```

### 2.8.5 五子棋

接下来，我们使用之前学习的绘图技术，做一个五子棋的游戏。

​	![](./images/五子棋.jpg)

**演示代码：**

```java
import javax.imageio.ImageIO;
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.awt.image.BufferedImage;
import java.io.File;

public class Gobang {

    //定义三个BufferedImage，分别代表棋盘图、黑子图、白子图
    private BufferedImage table;
    private BufferedImage black;
    private BufferedImage white;

    //定义一个BufferedImage，代表当鼠标移动时将要下子的选择框
    private BufferedImage selected;

    //定义棋盘的宽高，这里的定义尺寸和给定的board.jpg图片的尺寸一致因为棋盘背景是通过图片加载的
    private final int TABLE_WIDTH = 535;
    private final int TABLE_HEIGHT = 536;

    //定义棋盘中，每行和每列可下子的数目，这个数目跟给定的board.jpg中的数目是一致的，都为15
    private final int  BOARD_SIZE = 15;

    //定义每个棋子所占棋盘总宽度的大小比率；每个棋子所占宽度 535/15=35
    private final int RATE = TABLE_WIDTH/BOARD_SIZE;

    //定义棋盘有效区域与背景图坐标之间的偏移值，x坐标右移5个像素，y坐标下移6个像素
    private final int X_OFFSET = 5;
    private final int Y_OFFSET = 6;


    /*

        定义一个二维数组充当棋盘上每个位置处的棋子；
        该数组的索引与该棋子在棋盘上的坐标需要有一个对应关系：
            例如： 索引[2][3]处的棋子，对一个的真实绘制坐标应该是：

                xpos = 2*RATE+X_OFFSET=75;
                ypos = 3*RATE+Y_OFFSET=111;

     */
    private int[][] board = new int[BOARD_SIZE][BOARD_SIZE];//如果存储0，代表没有棋子，如果存储1，代表黑棋，如果存储2，代表白棋

    //定义五子棋游戏窗口
    private JFrame f = new JFrame("五子棋游戏");

    //定义五子棋游戏棋盘对应的Canvas组件
    private class ChessBoard extends JPanel{
        //重写paint方法，实现绘画
        @Override
        public void paint(Graphics g) {
            //绘制五子棋棋盘
            g.drawImage(table,0,0,null);
            //绘制选中点的红框
            if (selectX>0 && selectY>0){
                g.drawImage(selected,selectX*RATE+X_OFFSET,selectY*RATE+Y_OFFSET,null);
            }

            //遍历数组，绘制棋子
            for (int i = 0; i < BOARD_SIZE; i++) {
                for (int j = 0; j < BOARD_SIZE; j++) {
                    //绘制黑棋

                    if (board[i][j]==1){
                        g.drawImage(black,i*RATE+X_OFFSET,j*RATE+Y_OFFSET,null);
                    }

                    //绘制白棋
                    if (board[i][j]==2){
                        g.drawImage(white,i*RATE+X_OFFSET,j*RATE+Y_OFFSET,null);
                    }
                }
            }
        }
    }

    private ChessBoard chessBoard = new ChessBoard();

    //定义变量，记录当前选中的坐标点对应的boad数组中对应的棋子索引；
    private int selectX = -1;
    private int selectY = -1;

    //定义一个变量，记录当前用户选择下的是白棋还是黑棋还是清除，清除：0，黑棋：1，白棋：2；
    private int chessCategory = 1;

    //定义Panel,放置点击按钮
    Panel p = new Panel();
    private Button whiteBtn = new Button("白棋");
    private Button blackBtn = new Button("黑棋");
    private Button clearBtn = new Button("删除");

    public void updateBtnColor(Color whiteBtnColor,Color blackBtnColor,Color clearBtnColor){
        whiteBtn.setBackground(whiteBtnColor);
        blackBtn.setBackground(blackBtnColor);
        clearBtn.setBackground(clearBtnColor);
    }

    public void init() throws Exception{

        //初始化按钮的颜色
        updateBtnColor(Color.LIGHT_GRAY,Color.GREEN,Color.LIGHT_GRAY);
        whiteBtn.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                chessCategory = 2;
                updateBtnColor(Color.GREEN,Color.LIGHT_GRAY,Color.LIGHT_GRAY);
            }
        });
        blackBtn.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                chessCategory=1;
                updateBtnColor(Color.LIGHT_GRAY,Color.GREEN,Color.LIGHT_GRAY);
            }
        });
        clearBtn.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                chessCategory=0;
                updateBtnColor(Color.LIGHT_GRAY,Color.LIGHT_GRAY,Color.GREEN);
            }
        });

        p.add(whiteBtn);
        p.add(blackBtn);
        p.add(clearBtn);
        //把Panel放入到frame底部
        f.add(p,BorderLayout.SOUTH);



        //初始化黑棋，白棋，棋盘,选中框
        table = ImageIO.read(new File("awt_demo\\board.jpg"));
        black = ImageIO.read(new File("awt_demo\\black.gif"));
        white = ImageIO.read(new File("awt_demo\\white.gif"));
        selected = ImageIO.read(new File("awt_demo\\selected.gif"));
        //初始化board数组，默认情况下，所有位置处都没有棋子
        for (int i = 0; i < BOARD_SIZE; i++) {
            for (int j = 0; j < BOARD_SIZE; j++) {
                board[i][j]=0;
            }
        }

        //设置chessBoard的最佳大小
        chessBoard.setPreferredSize(new Dimension(TABLE_WIDTH,TABLE_HEIGHT));

        //给chessBoard注册鼠标监听器
        chessBoard.addMouseListener(new MouseAdapter() {
            //鼠标单击会触发
            @Override
            public void mouseClicked(MouseEvent e) {
                //将用户鼠标的坐标，转换成棋子的坐标
                int xPos = (e.getX()-X_OFFSET)/RATE;
                int yPos = (e.getY()-Y_OFFSET)/RATE;

                board[xPos][yPos] = chessCategory;

                //重绘chessBoard
                chessBoard.repaint();
            }

            //当鼠标退出棋盘区域后，复位选中坐标,重绘chessBoard，要保证红色选中框显示正确
            @Override
            public void mouseExited(MouseEvent e) {
                selectX=-1;
                selectY=-1;
                chessBoard.repaint();
            }
        });

        //给chessBoard注册鼠标移动监听器
        chessBoard.addMouseMotionListener(new MouseMotionAdapter() {
            //当鼠标移动时，修正selectX和selectY，重绘chessBoard，要保证红色选中框显示正确
            @Override
            public void mouseMoved(MouseEvent e) {
                //将鼠标的坐标，转换成棋子的索引
                selectX = (e.getX()-X_OFFSET)/RATE;
                selectY = (e.getY()-Y_OFFSET)/RATE;
                chessBoard.repaint();
            }
        });

        //把chessBoard添加到Frame中
        f.add(chessBoard);



        //设置frame最佳大小并可见
        f.pack();
        f.setVisible(true);

    }

    public static void main(String[] args) throws Exception{
        new Gobang().init();
    }

}
```





# 三. Swing 编程

## 3.1 Swing概述

​	前一章己经介绍过AWT和Swing 的关系 ， 因此不难知道 : 实际使用 Java 开发图形界面程序时 ，很少使用 AWT 组件，绝大部分时候都是用 Swing 组件开发的 。 Swing是由100%纯 Java实现的，不再依赖于本地平台的 GUI， 因此可以在所有平台上都保持相同的界面外观。独立于本地平台的Swing组件被称为**轻量级组件**;而依赖于本地平台的 AWT 组件被称为**重量级组件**。
	由于 Swing 的所有组件完全采用 Java 实现，不再调用本地平台的 GUI，所以导致 Swing 图形界面的显示速度要比 AWT 图形界面的显示速度慢一些，但相对于快速发展的硬件设施而言，这种微小的速度差别无妨大碍。

**使用Swing的优势:**
	1. Swing 组件不再依赖于本地平台的 GUI，无须采用各种平台的 GUI 交集 ，因此 Swing 提供了大量图形界面组件 ， 远远超出了 AWT 所提供的图形界面组件集。
	2. Swing 组件不再依赖于本地平台 GUI ，因此不会产生与平台 相关的 bug 。

​	3. Swing 组件在各种平台上运行时可以保证具有相同的图形界面外观。

​	Swing 提供的这些优势，让 Java 图形界面程序真正实现了 " Write Once, Run Anywhere" 的 目标。



**Swing的特征：**
 	1. Swing 组件采用 MVC(Model-View-Controller， 即模型一视图一控制器)设计模式：

			模型(Model): 用于维护组件的各种状态；

		视图(View): 是组件的可视化表现；
		
		控制器(Controller):用于控制对于各种事件、组件做出响应 。
		
		当模型发生改变时，它会通知所有依赖它的视图，视图会根据模型数据来更新自己。Swing使用UI代理来包装视图和控制器， 还有一个模型对象来维护该组件的状态。例如，按钮JButton有一个维护其状态信息的模型ButtonModel对象 。 Swing组件的模型是自动设置的，因此一般都使用JButton，而无须关心ButtonModel对象。

	2. Swing在不同的平台上表现一致，并且有能力提供本地平台不支持的显示外观 。由于 Swing采用 MVC 模式来维护各组件，所以 当组件的外观被改变时，对组件的状态信息(由模型维护)没有任何影响 。因 此，Swing可以使用插拔式外观感觉 (Pluggable Look And Feel, PLAF)来控制组件外观，使得 Swing图形界面在同一个平台上运行时能拥有不同的外观，用户可以选择自己喜欢的外观 。相比之下，在 AWT 图形界面中，由于控制组件外观的对等类与具体平台相关 ，因此 AWT 组件总是具有与本地平台相同的外观 。    



## 3.2 Swing基本组件的用法

### 3.2.1 Swing组件层次

**Swing组件继承体系图：**

![](./images/Swing组件继承体系.png)

​	大部分Swing 组件都是 JComponent抽象类的直接或间接子类(并不是全部的 Swing 组件)，JComponent 类定义了所有子类组件的通用方法 ，JComponent 类是 AWT 里 java.awt. Container 类的子类 ，这也是 AWT 和 Swing 的联系之一。 绝大部分 Swing 组件类继承了 Container类，所以Swing 组件都可作为 容器使用 ( JFrame继承了Frame 类)。

**Swing组件和AWT组件的对应关系：**

​	大部分情况下，只需要在AWT组件的名称前面加个J，就可以得到其对应的Swing组件名称，但有几个例外：

​		1. JComboBox: 对应于 AWT 里的 Choice 组件，但比 Choice 组件功能更丰富 。
		2. JFileChooser: 对应于 AWT 里的 FileDialog 组件 。
		3. JScrollBar: 对应于 AWT 里的 Scrollbar 组件，注意两个组件类名中 b 字母的大小写差别。
		4. JCheckBox : 对应于 AWT 里的 Checkbox 组件， 注意两个组件类名中 b 字母的大小 写差别 。
		5. JCheckBoxMenultem: 对应于 AWT 里的 CheckboxMenuItem 组件，注意两个组件类名中 b字母的大小写差别。



**Swing组件按照功能来分类：**

​	1. 顶层容器: JFrame、JApplet、JDialog 和 JWindow 。
	2. 中间容器: JPanel 、 JScrollPane 、 JSplitPane 、 JToolBar 等 。
	3. 特殊容器:在用户界面上具有特殊作用的中间容器，如 JIntemalFrame 、 JRootPane 、 JLayeredPane和 JDestopPane 等 。
	4. 基本组件 : 实现人机交互的组件，如 JButton、 JComboBox 、 JList、 JMenu、 JSlider 等 。
	5. 不可编辑信息的显示组件:向用户显示不可编辑信息的组件，如JLabel 、 JProgressBar 和 JToolTip等。
	6. 可编辑信息的显示组件:向用户显示能被编辑的格式化信息的组件，如 JTable 、 JTextArea 和JTextField 等 。
	7. 特殊对话框组件:可以直接产生特殊对话框的组件 ， 如 JColorChooser 和 JFileChooser 等。

### 3.2.2 AWT组件的Swing实现

​	Swing 为除 Canvas 之外的所有 AWT 组件提供了相应的实现，Swing 组件比 AWT 组件的功能更加强大。相对于 AWT 组件， Swing 组件具有如下 4 个额外的功能 :

1. 可以为 Swing 组件设置提示信息。使用 setToolTipText()方法，为组件设置对用户有帮助的提示信息 。

2. 很多 Swing 组件如按钮、标签、菜单项等，除使用文字外，还可以使用图标修饰自己。为了允许在 Swing 组件中使用图标， Swing为Icon 接口提供了 一个实现类: Imagelcon ，该实现类代表一个图像图标。

3. 支持插拔式的外观风格。每个 JComponent 对象都有一个相应的 ComponentUI 对象，为它完成所有的绘画、事件处理、决定尺寸大小等工作。 ComponentUI 对象依赖当前使用的 PLAF ， 使用 UIManager.setLookAndFeel()方法可以改变图形界面的外观风格 。
4. 支持设置边框。Swing 组件可以设置一个或多个边框。 Swing 中提供了各式各样的边框供用户边 用，也能建立组合边框或自己设计边框。 一种空白边框可以用于增大组件，同时协助布局管理器对容器中的组件进行合理的布局。    



​	每个 Swing 组件都有一个对应的UI 类，例如 JButton组件就有一个对应的 ButtonUI 类来作为UI代理 。每个 Swing组件的UI代理的类名总是将该 Swing 组件类名的 J 去掉，然后在后面添加 UI 后缀 。 UI代理类通常是一个抽象基类 ， 不同的 PLAF 会有不同的UI代理实现类 。 Swing 类库中包含了几套UI代理,分别放在不同的包下， 每套UI代理都几乎包含了所有 Swing组件的 ComponentUI实现，每套这样的实现都被称为一种PLAF 实现 。以 JButton 为例，其 UI 代理的继承层次下图：

​	  ![](./images/ComponentUI.png)

​	如果需要改变程序的外观风格， 则可以使用如下代码：

```java
//容器：
JFrame jf = new JFrame();

try {

    //设置外观风格
    UIManager.setLookAndFeel("com.sun.java.swing.plaf.windows.WindowsLookAndFeel");

    //刷新jf容器及其内部组件的外观
    SwingUtilities.updateComponentTreeUI(jf);
} catch (Exception e) {
    e.printStackTrace();
}
```



**案例：**

​	使用Swing组件，实现下图中的界面效果：

​	![](./images/swing_c_1.jpg)

​	![](./images/swing_c_2.jpg)

**演示代码：**

```java
import cn.itcast.swing.util.ImagePathUtil;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.InputEvent;

public class SwingComponentDemo {


    JFrame f = new JFrame("测试swing基本组件");

    //定义一个按钮，并为其指定图标
    Icon okIcon = new ImageIcon(ImagePathUtil.getRealPath("2\\ok.png"));
    JButton ok = new JButton("确定",okIcon);

    //定义一个单选按钮，初始处于选中的状态
    JRadioButton male = new JRadioButton("男",true);
    //定义一个单选按钮，初始处于选中状态
    JRadioButton female = new JRadioButton("女",false);

    //定义一个ButtonGroup，把male和female组合起来，实现单选
    ButtonGroup bg  = new ButtonGroup();

    //定义一个复选框，初始处于没有选中状态
    JCheckBox married = new JCheckBox("是否已婚？",false);

    //定义一个数组存储颜色
    String[] colors = { "红色", "绿色 " , "蓝色 " };

    //定义一个下拉选择框，展示颜色
    JComboBox<String> colorChooser = new JComboBox<String>(colors);

    //定一个列表框，展示颜色
    JList<String> colorList = new JList<String>(colors);

    //定义一个8行20列的多行文本域
    JTextArea ta = new JTextArea(8,20);

    //定义一个40列的单行文本域
    JTextField name = new JTextField(40);

    //定义菜单条
    JMenuBar mb = new JMenuBar();

    //定义菜单
    JMenu file = new JMenu("文件");
    JMenu edit = new JMenu("编辑");

    //创建菜单项，并指定图标
    JMenuItem newItem = new JMenuItem("新建",new ImageIcon(ImagePathUtil.getRealPath("2\\new.png")));
    JMenuItem saveItem = new JMenuItem("保存",new ImageIcon(ImagePathUtil.getRealPath("2\\save.png")));
    JMenuItem exitItem = new JMenuItem("退出",new ImageIcon(ImagePathUtil.getRealPath("2\\exit.png")));

    JCheckBoxMenuItem autoWrap = new JCheckBoxMenuItem("自动换行");
    JMenuItem copyItem = new JMenuItem("复制",new ImageIcon(ImagePathUtil.getRealPath("2\\copy.png")));
    JMenuItem pasteItem = new JMenuItem("粘贴",new ImageIcon(ImagePathUtil.getRealPath("2\\paste.png")));

    //定义二级菜单，将来会添加到编辑中
    JMenu format = new JMenu("格式");
    JMenuItem commentItem = new JMenuItem("注释");
    JMenuItem cancelItem = new JMenuItem("取消注释");

    //定义一个右键菜单，用于设置程序的外观风格
    JPopupMenu pop = new JPopupMenu();

    //定义一个ButtongGroup对象，用于组合风格按钮，形成单选
    ButtonGroup flavorGroup = new ButtonGroup();

    //定义五个单选按钮菜单项，用于设置程序风格
    JRadioButtonMenuItem metalItem = new JRadioButtonMenuItem("Metal 风格",true);
    JRadioButtonMenuItem nimbusItem = new JRadioButtonMenuItem("Nimbus 风格",true);
    JRadioButtonMenuItem windowsItem = new JRadioButtonMenuItem("Windows 风格",true);
    JRadioButtonMenuItem classicItem = new JRadioButtonMenuItem("Windows 经典风格",true);
    JRadioButtonMenuItem motifItem = new JRadioButtonMenuItem("Motif 风格",true);



    //初始化界面
    public void init(){

        //------------------------组合主区域------------------------
        //创建一个装载文本框和按钮的JPanel
        JPanel bottom = new JPanel();
        bottom.add(name);
        bottom.add(ok);

        f.add(bottom, BorderLayout.SOUTH);

        //创建一个装载下拉选择框、三个JChekBox的JPanel
        JPanel checkPanel = new JPanel();
        checkPanel.add(colorChooser);
        bg.add(male);
        bg.add(female);

        checkPanel.add(male);
        checkPanel.add(female);
        checkPanel.add(married);

        //创建一个垂直排列的Box，装载checkPanel和多行文本域
        Box topLeft = Box.createVerticalBox();

        //使用JScrollPane作为普通组件的JViewPort
        JScrollPane taJsp = new JScrollPane(ta);
        topLeft.add(taJsp);
        topLeft.add(checkPanel);

        //创建一个水平排列的Box，装载topLeft和colorList
        Box top = Box.createHorizontalBox();
        top.add(topLeft);
        top.add(colorList);

        //将top Box 添加到窗口的中间
        f.add(top);

        //---------------------------组合菜单条----------------------------------------------
        //为newItem添加快捷键 ctrl+N
        newItem.setAccelerator(KeyStroke.getKeyStroke('N', InputEvent.CTRL_MASK));
        newItem.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                ta.append("用户点击了“新建”菜单\n");
            }
        });


        //为file添加菜单项
        file.add(newItem);
        file.add(saveItem);
        file.add(exitItem);

        //为edit添加菜单项
        edit.add(autoWrap);
        edit.addSeparator();
        edit.add(copyItem);
        edit.add(pasteItem);
        //为commentItem添加提示信息
        commentItem.setToolTipText("将程序代码注释起来");

        //为format菜单添加菜单项
        format.add(commentItem);
        format.add(cancelItem);

        //给edit添加一个分隔符
        edit.addSeparator();

        //把format添加到edit中形成二级菜单
        edit.add(format);

        //把edit file 添加到菜单条中
        mb.add(file);
        mb.add(edit);

        //把菜单条设置给窗口
        f.setJMenuBar(mb);

        //------------------------组合右键菜单-----------------------------

        flavorGroup.add(metalItem);
        flavorGroup.add(nimbusItem);
        flavorGroup.add(windowsItem);
        flavorGroup.add(classicItem);
        flavorGroup.add(motifItem);

        //给5个风格菜单创建事件监听器
        ActionListener flavorLister = new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String command = e.getActionCommand();
                try {
                    changeFlavor(command);
                } catch (Exception e1) {
                    e1.printStackTrace();
                }
            }
        };

        //为5个风格菜单项注册监听器
        metalItem.addActionListener(flavorLister);
        nimbusItem.addActionListener(flavorLister);
        windowsItem.addActionListener(flavorLister);
        classicItem.addActionListener(flavorLister);
        motifItem.addActionListener(flavorLister);

        pop.add(metalItem);
        pop.add(nimbusItem);
        pop.add(windowsItem);
        pop.add(classicItem);
        pop.add(motifItem);

        //调用ta组件的setComponentPopupMenu即可设置右键菜单，无需使用事件
        ta.setComponentPopupMenu(pop);

        // 设置关闭窗口时推出程序
        f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        //设置jFrame最佳大小并可见
        f.pack();
        f.setVisible(true);


    }

    //定义一个方法，用于改变界面风格
    private void changeFlavor(String command) throws Exception{
        switch (command){
            case "Metal 风格":
                UIManager.setLookAndFeel("javax.swing.plaf.metal.MetalLookAndFeel");
                break;
            case "Nimbus 风格":
                UIManager.setLookAndFeel("javax.swing.plaf.nimbus.NimbusLookAndFeel");
                break;
            case "Windows 风格":
                UIManager.setLookAndFeel("com.sun.java.swing.plaf.windows.WindowsLookAndFeel");
                break;
            case "Windows 经典风格":
                UIManager.setLookAndFeel("com.sun.java.swing.plaf.windows.WindowsClassicLookAndFeel");
                break;
            case "Motif 风格":
                UIManager.setLookAndFeel("com.sun.java.swing.plaf.motif.MotifLookAndFeel");
                break;
        }

        //更新f窗口内顶级容器以及所有组件的UI
        SwingUtilities.updateComponentTreeUI(f.getContentPane());
        //更新mb菜单条及每部所有组件UI
        SwingUtilities.updateComponentTreeUI(mb);
        //更新右键菜单及内部所有菜单项的UI
        SwingUtilities.updateComponentTreeUI(pop);
    }


    public static void main(String[] args) {
        new SwingComponentDemo().init();
    }

}

```

**注意细节：**

1.Swing菜单项指定快捷键时必须通过`组件名.setAccelerator(keyStroke.getKeyStroke("大写字母",InputEvent.CTRL_MASK))`方法来设置，其中KeyStroke代表一次击键动作，可以直接通过按键对应字母来指定该击键动作 。

2.更新JFrame的风格时，调用了` SwingUtilities.updateComponentTreeUI(f.getContentPane());`这是因为如果直接更新 JFrame 本身 ，将会导致 JFrame 也被更新， JFrame 是一个特殊的容器 ， JFrame 依然部分依赖于本地平台的图形组件 。如果强制 JFrame 更新，则有可能导致该窗口失去标题栏和边框 。 

3.给组件设置右键菜单，不需要使用监听器，只需要调用setComponentPopupMenu()方法即可，更简单。

4.关闭JFrame窗口，也无需监听器，只需要调用setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE)方法即可，更简单。

5.如果需要让某个组件支持滚动条，只需要把该组件放入到JScrollPane中，然后使用JScrollPane即可。



### 3.2.3 为组件设置边框

​	很多情况下，我们常常喜欢给不同的组件设置边框，从而让界面的层次感更明显，swing中提供了Border对象来代表一个边框，下图是Border的继承体系图：

​	![](./images/Border继承体系.png)

**特殊的Border：**

 	1. TitledBorder:它的作用并不是直接为其他组件添加边框，而是为其他边框设置标题，创建该类的对象时，需要传入一个其他的Border对象；
		2. ComoundBorder:用来组合其他两个边框，创建该类的对象时，需要传入其他两个Border对象，一个作为内边框，一个座位外边框

**给组件设置边框步骤：**

 	1. 使用BorderFactory或者XxxBorder创建Border的实例对象；
		2. 调用Swing组件的setBorder（Border b）方法为组件设置边框；

**案例：**

​	请使用Border实现下图效果：

​	![](./images/border.jpg)

**演示代码：**

```java
import javax.swing.*;
import javax.swing.border.*;
import java.awt.*;

public class BorderTest {

    JFrame jf  = new JFrame("测试边框");

    public void init(){
        //设置Jframe为网格布局
        jf.setLayout(new GridLayout(2,4));

        //创建凸起的斜边框，分别设置四条边的颜色
        Border bb = BorderFactory.createBevelBorder(BevelBorder.RAISED,Color.RED,Color.GREEN,Color.BLUE,Color.GRAY);
        jf.add(getPanelWithBorder(bb,"BevelBorder"));


        //创建LineBorder
        Border lb = BorderFactory.createLineBorder(Color.ORANGE, 10);
        jf.add(getPanelWithBorder(lb,"LineBorder"));

        //创建EmptyBorder，会在组件的四周留白
        Border eb = BorderFactory.createEmptyBorder(20, 5, 10, 30);
        jf.add(getPanelWithBorder(eb,"EmptyBorder"));

        //创建EtchedBorder，
        Border etb = BorderFactory.createEtchedBorder(EtchedBorder.RAISED, Color.RED, Color.GREEN);
        jf.add(getPanelWithBorder(etb,"EtchedBorder"));

        //创建TitledBorder,为原有的Border添加标题
        TitledBorder tb = new TitledBorder(lb,"测试标题",TitledBorder.LEFT,TitledBorder.BOTTOM,new Font("StSong",Font.BOLD,18),Color.BLUE);
        jf.add(getPanelWithBorder(tb,"TitledBorder"));

        //直接创建MatteBorder，它是EmptyBorder的子类，EmptyBorder是留白，而MatteBorder可以给留空的区域填充颜色
        MatteBorder mb = new MatteBorder(20,5,10,30,Color.GREEN);
        jf.add(getPanelWithBorder(mb,"MatteBorder"));

        //直接创创建CompoundBorder，将两个边框组合成新边框
        CompoundBorder cb = new CompoundBorder(new LineBorder(Color.RED,8),tb);
        jf.add(getPanelWithBorder(cb,"CompoundBorder"));

        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.pack();
        jf.setVisible(true);

    }
    public JPanel getPanelWithBorder(Border border,String borderName){
        JPanel jPanel = new JPanel();

        jPanel.add(new JLabel(borderName));

        //为panel设置边框
        jPanel.setBorder(border);

        return jPanel;
    }
    public static void main(String[] args) {
        new BorderTest().init();
    }
}
```

### 3.2.4 使用JToolBar创建工具条

Swing 提供了JToolBar类来创建工具条，并且可以往JToolBar中添加多个工具按钮。

**JToolBar  API:**

| 方法名称                                 | 方法功能                                                     |
| ---------------------------------------- | ------------------------------------------------------------ |
| JToolBar( String name , int orientation) | 创建一个名字为name，方向为orientation的工具条对象，其orientation的是取值可以是SwingConstants.HORIZONTAL或SwingConstants.VERTICAL |
| JButton add(Action a)                    | 通过Action对象为JToolBar工具条添加对应的工具按钮             |
| addSeparator( Dimension size )           | 向工具条中添加指定大小的分隔符                               |
| setFloatable( boolean b )                | 设定工具条是否可以被拖动                                     |
| setMargin(Insets m)                      | 设置工具条与工具按钮的边距                                   |
| setOrientation( int o )                  | 设置工具条的方向                                             |
| setRollover(boolean rollover)            | 设置此工具条的rollover状态                                   |

**add(Action a)方法：**

​	上述API中add(Action a)这个方法比较难理解，为什么呢，之前说过，Action接口是ActionListener的一个子接口，那么它就代表一个事件监听器，而这里add方法是在给工具条添加一个工具按钮，为什么传递的是一个事件监听器呢？

​	首先要明确的是不管是菜单条中的菜单项还是工具条中的工具按钮，最终肯定是需要点击来完成一些操作，所以JToolBar以及JMenu都提供了更加便捷的添加子组件的方法add(Action a),在这个方法的内部会做如下几件事：

   	1. 创建一个适用于该容器的组件(例如，在工具栏中创建一个工具按钮)；
   	2. 从 Action 对象中获得对应的属性来设置该组件(例如，通过 name 来设置文本，通过 lcon 来设置图标) ；
   	3. 把Action监听器注册到刚才创建的组件上；

**案例：**

​	使用JToolBar组件完成下图效果：

​	![](./images/JTooBarTest.jpg)

**演示代码：**

```java
import cn.itcast.swing.util.ImagePathUtil;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;

public class JToolBarTest {

    JFrame jf = new JFrame("测试工具条");

    JTextArea jta = new JTextArea(6,35);
    //创建工具条
    JToolBar jtb = new JToolBar();

    //创建"上一曲"Action,该Action用于创建工具按钮
    Action pre = new AbstractAction("上一曲",new ImageIcon(ImagePathUtil.getRealPath("2\\pre.png"))) {
        @Override
        public void actionPerformed(ActionEvent e) {
            jta.append("上一曲.\n");
        }
    };

    //创建"暂停" Action
    Action pause = new AbstractAction("暂停",new ImageIcon(ImagePathUtil.getRealPath("2\\pause.png"))) {
        @Override
        public void actionPerformed(ActionEvent e) {
           jta.append("暂停播放.\n");
        }
    };

    // 创建"下一曲" Action
    Action next = new AbstractAction("下一曲",new ImageIcon(ImagePathUtil.getRealPath("2\\next.png"))) {
        @Override
        public void actionPerformed(ActionEvent e) {
            jta.append("下一曲.\n");
        }
    };

    public void init(){

        //给JTextArea添加滚动条
        jf.add(new JScrollPane(jta));

        //以Action的形式创建按钮，并将按钮添加到Panel中
        JButton preBtn = new JButton(pre);
        JButton pauseBtn = new JButton(pause);
        JButton nextBtn = new JButton(next);


        //往工具条中添加Action对象，该对象会转换成工具按钮
        jtb.add(preBtn);
        jtb.addSeparator();
        jtb.add(pauseBtn);
        jtb.addSeparator();
        jtb.add(nextBtn);

        //向窗口中添加工具条
        jf.add(jtb,BorderLayout.NORTH);

        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        jf.pack();
        jf.setVisible(true);
    }

    public static void main(String[] args) {
        new JToolBarTest().init();
    }
}
```

### 3.2.5 JColorChooser 和JFileChooser

Swing提供了JColorChooser和JFileChooser这两种对话框，可以很方便的完成颜色的选择和本地文件的选择。

#### 3.2.5.1 JColorChooser

JColorChooser 用于创建颜色选择器对话框 ， 该类的用法非常简单，只需要调用它的静态方法就可以快速生成一个颜色选择对话框：

```java
public static Color showDialog(Component component, String title,Color initialColor)
    
/*
	参数：
		componet:指定当前对话框的父组件
		title：当前对话框的名称
		initialColor：指定默认选中的颜色
		
	返回值：
		返回用户选中的颜色
*/
```

**案例：**

​	使用颜色选择器，完成下图功能：

​		点击按钮，改变文本域的背景色

​	![](./images/JColorChooser.jpg)

**演示代码：**

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;

public class JColorChooserDemo {

    JFrame jFrame = new JFrame("测试颜色选择器");

    JTextArea jta = new JTextArea("我爱中华",6,30);

    JButton button = new JButton(new AbstractAction("改变文本框的本景色"){

        @Override
        public void actionPerformed(ActionEvent e) {

            //弹出颜色选择器
            Color result = JColorChooser.showDialog(jFrame, "颜色选择器", Color.WHITE);
            jta.setBackground(result);
        }
    });

    public void init(){
        jFrame.add(jta);

        jFrame.add(button,BorderLayout.SOUTH);

        jFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jFrame.pack();
        jFrame.setVisible(true);
    }

    public static void main(String[] args) {
        new JColorChooserDemo().init();
    }

}

```

#### 3.2.5.2 JFileChooser

​	JFileChooser 的功能与AWT中的 FileDialog 基本相似，也是用于生成"打开文件"、"保存文件 "对话框。与 FileDialog 不同的是 ， JFileChooser 无须依赖于本地平台的 GUI ， 它由 100%纯 Java 实现 ， 在所有平台 上具有完全相同的行为，并可以在所有平台上具有相同的外观风格。

JFileChooser使用步骤：

1. 创建JFileChooser对象：

```java
JFileChooser chooser = new JFileChooser("D:\\a");//指定默认打开的本地磁盘路径
```

2. 调用JFileChooser的一系列可选方法，进行初始化

```java
setSelectedFile(File file)/setSelectedFiles(File[] selectedFiles):设定默认选中的文件
setMultiSelectionEnabled(boolean b)：设置是否允许多选，默认是单选
setFileSelectionMode(int mode)：设置可以选择内容，例如文件、文件夹等，默认只能选择文件
```

3. 打开文件对话框

```java
showOpenDialog(Component parent):打开文件加载对话框，并指定父组件
showSaveDialog(Component parent):打开文件保存对话框，并指定父组件
```

4. 获取用户选择的结果

```java
File getSelectedFile():获取用户选择的一个文件
File[] getSelectedFiles():获取用户选择的多个文件
```

**案例：**

​	使用JFileChooser完成下图效果：

​	![](./images/ImageIODemo.jpg)



**演示代码：**

```java
import javax.imageio.ImageIO;
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

public class JFileChooserDemo {

    //创建窗口对象
    JFrame jf = new JFrame("测试JFileChooser");

    //创建打开文件对话框
    JFileChooser chooser = new JFileChooser(".");

    //创建菜单条
    JMenuBar jmb = new JMenuBar();
    //创建菜单
    JMenu jMenu = new JMenu("文件");
    //创建菜单项
    JMenuItem open = new JMenuItem(new AbstractAction("打开"){

        @Override
        public void actionPerformed(ActionEvent e) {
            chooser.showOpenDialog(jf);
            File imageFile = chooser.getSelectedFile();
            try {
                image = ImageIO.read(imageFile);
                drawArea.repaint();
            } catch (IOException e1) {
                e1.printStackTrace();
            }
        }
    });

    JMenuItem save = new JMenuItem(new AbstractAction("另存为"){

        @Override
        public void actionPerformed(ActionEvent e) {
            chooser.setFileSelectionMode(JFileChooser.DIRECTORIES_ONLY);
            chooser.showSaveDialog(jf);
            File dir = chooser.getSelectedFile();
            try {
                ImageIO.write(image,"jpeg",new File(dir,"a.jpg"));
            } catch (Exception e1) {
                e1.printStackTrace();
            }
        }
    });

    //用来记录用户选择的图片
    BufferedImage image;

    //显示图片
    class MyCanvas extends JPanel{
        @Override
        public void paint(Graphics g) {
            if (image!=null){
                g.drawImage(image,0,0,null);
            }
        }
    }

    JPanel drawArea = new MyCanvas();

    public void init(){
        //设置图片显示区域大小
        drawArea.setPreferredSize(new Dimension(500,300));
        jf.add(drawArea);

        //组装并设置菜单条
        jMenu.add(open);
        jMenu.add(save);
        jmb.add(jMenu);
        jf.setJMenuBar(jmb);

        //显示jf
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.pack();
        jf.setVisible(true);
    }

    public static void main(String[] args) {
        new JFileChooserDemo().init();
    }    
      
}
```

### 3.2.7 使用JOptionPane

#### 3.2.7.1 基本概述

通过 JOptionPane 可以非常方便地创建一些简单的对话框， Swing 已经为这些对话框添加了相应的组件，无须程序员手动添加组件 。 JOptionPane 提供了如下 4 个方法来创建对话框 。

| 方法名称                                    | 方法功能                                                     |
| ------------------------------------------- | ------------------------------------------------------------ |
| showMessageDialog/showInternalMessageDialog | 消息对话框 ，告知用户某事己发生 ， 用户只能单击"确定"按钮 ， 类似于 JavaScript 的 alert 函数 。 |
| showConfirmDialog/showInternalConfirmDialog | 确认对话框，向用户确认某个问题，用户可以选择 yes 、 no ~ cancel 等选项 。 类似于 JavaScript 的 comfirm 函数 。该方法返回用户单击了 哪个按钮 |
| showInputDialog/showInternalInputDialog     | 输入对话框，提示要求输入某些信息，类似于 JavaScript的 prompt 函数。该方法返回用户输入的字符串 。 |
| showOptionDialog/showInternalOptionDialog   | 自定义选项对话框 ，允许使用自 定义选项 ，可以取代showConfirmDialog 所产生的对话框，只是用起来更复杂 。 |

上述方法都有都有很多重载形式，选择其中一种最全的形式，参数解释如下：

```java
showXxxDialog(Component parentComponent,
		Object message, 
		String title, 
		int optionType, 
		int messageType,
        	Icon icon,
		Object[] options, 
		Object initialValue)
--参数解释：
parentComponent：当前对话框的父组件
message：对话框上显示的信息，信息可以是字符串、组件、图片等
title：当前对话框的标题
optionType：当前对话框上显示的按钮类型：DEFAULT_OPTION、YES_NO_OPTION、YES_NO_CANCEL_OPTION、OK_CANCEL_OPTION
messageType:当前对话框的类型:ERROR_MESSAGE、INFORMATION_MESSAGE、WARNING_MESSAGE、QUESTION_MESSAGE、PLAIN_MESSAGE
icon:当前对话框左上角的图标
options:自定义下拉列表的选项
initialValue:自定义选项中的默认选中项
```



**当用户与对话框交互结束后，不同类型对话框的返回值如下：**

- showMessageDialog: 无返回值 。
- showlnputDialog: 返回用户输入或选择的字符串 。
- showConfirmDialog: 返回 一个整数代表用户选择的选项 。
- showOptionDialog : 返回 一个整数代表用户选择的选项，如果用户选择第一项，则返回 0; 如果选择第二项，则返回1……依此类推 。

**对 showConfirmDialog 所产生的对话框，有如下几个返回值：**

- YES OPTION: 用户 单击了 "是"按钮后返回 。
- NO OPTION: 用 户单击了"否"按钮后返回 。
- CANCEL OPTION: 用户单击了"取消"按钮后返回 。
- OK OPTION : 用户单击了"确定"按钮后返回 。
- CLOSED OPTION: 用户 单击了对话框右上角的 " x" 按钮后返回。

#### 3.2.7.2 四种对话框演示

**消息对话框：**

​	![](./images/消息提示框.jpg)

```java
import cn.itcast.swing.util.ImagePathUtil;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;

public class MessageDialogTest {


    JFrame jf = new JFrame("测试消息对话框");

    JTextArea jta = new JTextArea(6, 30);

    JButton btn = new JButton(new AbstractAction("弹出消息对话框") {

        @Override
        public void actionPerformed(ActionEvent e) {
            //JOptionPane.showMessageDialog(jf, jta.getText(), "消息对话框", JOptionPane.ERROR_MESSAGE);
            //JOptionPane.showMessageDialog(jf, jta.getText(), "消息对话框", JOptionPane.INFORMATION_MESSAGE);
            //JOptionPane.showMessageDialog(jf, jta.getText(), "消息对话框", JOptionPane.WARNING_MESSAGE);
            //JOptionPane.showMessageDialog(jf, jta.getText(), "消息对话框", JOptionPane.QUESTION_MESSAGE);
            //JOptionPane.showMessageDialog(jf, jta.getText(), "消息对话框", JOptionPane.PLAIN_MESSAGE);
            JOptionPane.showMessageDialog(jf, jta.getText(), "消息对话框", JOptionPane.WARNING_MESSAGE, new ImageIcon(ImagePathUtil.getRealPath("2\\female.png")));

        }
    });


    public void init(){
        jf.add(jta);
        jf.add(btn, BorderLayout.SOUTH);

        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.pack();
        jf.setVisible(true);
    }

    public static void main(String[] args) {
        new MessageDialogTest().init();
    }

}

```



**确认对话框：**

​	![](./images/确认对话框.jpg)

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;

public class ConfirmDialogTest {


    JFrame jf = new JFrame("测试确认对话框");

    JTextArea jta = new JTextArea(6, 30);

    JButton btn = new JButton(new AbstractAction("弹出确认对话框") {

        @Override
        public void actionPerformed(ActionEvent e) {

            int result = JOptionPane.showConfirmDialog(jf, jta.getText(), "确认对话框",JOptionPane.YES_NO_OPTION, JOptionPane.QUESTION_MESSAGE);
            if (result == JOptionPane.YES_OPTION){
                jta.append("\n用户点击了确定按钮");
            }

            if (result==JOptionPane.NO_OPTION){
                jta.append("\n用户点击了取消按钮");
            }

        }
    });


    public void init(){
        jf.add(jta);
        jf.add(btn, BorderLayout.SOUTH);

        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.pack();
        jf.setVisible(true);
    }

    public static void main(String[] args) {
        new ConfirmDialogTest().init();
    }

}
```

​	

**输入对话框：**

​	![](./images/输入对话框1.jpg)

​	![](./images/输入对话框2.jpg)

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;

public class InputDialogTest {


    JFrame jf = new JFrame("测试输入对话框");

    JTextArea jta = new JTextArea(6, 30);

    JButton btn = new JButton(new AbstractAction("弹出输入对话框") {

        @Override
        public void actionPerformed(ActionEvent e) {


           /* String result = JOptionPane.showInputDialog(jf, "请填写您的银行账号：", "输入对话框", JOptionPane.INFORMATION_MESSAGE);
            if(result!=null){
                jta.append(result.toString());
            }
            */

            Object result = JOptionPane.showInputDialog(jf, "", "输入对话框", JOptionPane.DEFAULT_OPTION, null, new String[]{"柳岩", "舒淇", "龚玥菲"}, "舒淇");
            if (result!=null){
                jta.append(result.toString());
            }
        }
    });


    public void init(){
        jf.add(jta);
        jf.add(btn, BorderLayout.SOUTH);

        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.pack();
        jf.setVisible(true);
    }

    public static void main(String[] args) {
        new InputDialogTest().init();
    }

}

```



**选项对话框：**

​	![](./images/选项对话框.jpg)



```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;

public class OptionDialogTest {


    JFrame jf = new JFrame("测试选项对话框");

    JTextArea jta = new JTextArea(6, 30);

    JButton btn = new JButton(new AbstractAction("弹出选项对话框") {

        @Override
        public void actionPerformed(ActionEvent e) {




            int result = JOptionPane.showOptionDialog(jf, "请选择尿不湿号码", "选项对话框",JOptionPane.DEFAULT_OPTION,JOptionPane.INFORMATION_MESSAGE,
                    null,new String[]{"大号","中号","小号"},"中号");

            switch (result){
                case 0:
                    jta.setText("用户选择了大号");
                    break;
                case 1:
                    jta.setText("用户选择了中号");
                    break;
                case 2:
                    jta.setText("用户选择了小号");
                    break;
            }
        }
    });


    public void init(){
        jf.add(jta);
        jf.add(btn, BorderLayout.SOUTH);

        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.pack();
        jf.setVisible(true);
    }

    public static void main(String[] args) {
        new OptionDialogTest().init();
    }

}

```



## 3.3 Swing中的特殊容器

Swing提供了一些具有特殊功能的容器 ， 这些特殊容器可以用于创建一些更复杂的用户界面。

### 3.3.1 使用JSplitPane

JSplitPane 用于创建一个分割面板,它可以将 一个组件(通常是一个容器)分割成两个部分，并提供一个分割条 ， 用户可以拖动该分割条来调整两个部分的大小。

![](./images/JSplitPaneDemo.jpg)



**JSplitPane使用步骤：**

1. 创建JSplitPane对象

```java
通过如下构造方法可以创建JSplitPane对象
JSplitPane(int newOrientation, Component newLeftComponent,Component newRightComponent)
    newOrientation：指定JSplitPane容器的分割方向：
    	如果值为JSplitPane.VERTICAL_SPLIT,为纵向分割；
    	如果值为JSplitPane.HORIZONTAL_SPLIT，为横向分割；
    	
    newLeftComponent：左侧或者上侧的组件；
    newRightComponent：右侧或者下侧的组件；
```

2. 设置是否开启连续布局的支持(可选)

```java
setContinuousLayout(boolean newContinuousLayout):
	默认是关闭的，如果设置为true，则打开连续布局的支持，但由于连续布局支持需要不断的重绘组件，所以效率会低一些
```

3. 设置是否支持"一触即展"的支持(可选)

```java
setOneTouchExpandable(boolean newValue):
	默认是关闭的，如果设置为true，则打开"一触即展"的支持
```

4. 其他设置

```java
setDividerLocation(double proportionalLocation):设置分隔条的位置为JSplitPane的某个百分比
setDividerLocation(int location)：通过像素值设置分隔条的位置
setDividerSize(int newSize)：通过像素值设置分隔条的大小
setLeftComponent(Component comp)/setTopComponent(Component comp)/setRightComponent(Component comp)/setBottomComponent(Component comp):设置指定位置的组件
```

**案例：**

​	使用JSplitPane实现下图效果：

​		点击右侧的图书名称，在左上方显示该图书的图片，左下方显示该图书的描述

​	![](./images/JSplitPane.jpg)

**演示代码：**

```java
public class Book {

    private String name;

    private Icon icon;

    private String desc;

    public Book(String name, Icon icon, String desc) {
        this.name = name;
        this.icon = icon;
        this.desc = desc;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Icon getIcon() {
        return icon;
    }

    public void setIcon(Icon icon) {
        this.icon = icon;
    }

    public String getDesc() {
        return desc;
    }

    public void setDesc(String desc) {
        this.desc = desc;
    }

    @Override
    public String toString() {
        return name;
    }
}

import cn.itcast.swing.util.ImagePathUtil;

import javax.swing.*;
import javax.swing.event.ListSelectionEvent;
import javax.swing.event.ListSelectionListener;
import java.awt.*;

public class SplitPaneTest {

    Book[] books = {new Book("java自学宝典", new ImageIcon(ImagePathUtil.getRealPath("3\\java.png")), "国内关于 Java 编程最全面的图书 \n 看得懂 ， 学得会"),

            new Book("轻量级的JAVAEE企业应用实战", new ImageIcon(ImagePathUtil.getRealPath("3\\ee.png")), "SSM整合开发的经典图书，值的拥有"),

            new Book("Android基础教程", new ImageIcon(ImagePathUtil.getRealPath("3\\android.png")), "全面介绍Android平台应用程序\n 开发的各方面知识")

    };

    JFrame jf = new JFrame("测试JSplitPane");

    //列表展示图书
    JList<Book> bookList = new JList<>(books);

    JLabel bookCover = new JLabel();

    JTextArea bookDesc = new JTextArea();

    public void init(){

        //为三个组件设置最佳大小
        bookList.setPreferredSize(new Dimension(150,400));
        bookCover.setPreferredSize(new Dimension(220,330));
        bookDesc.setPreferredSize(new Dimension(220,70));

        //为列表添加事件监听器
        bookList.addListSelectionListener(new ListSelectionListener() {
            @Override
            public void valueChanged(ListSelectionEvent e) {
                Book book = bookList.getSelectedValue();
                bookCover.setIcon(book.getIcon());
                bookDesc.setText(book.getDesc());
            }
        });

        //创建一个垂直的分割面板
        JSplitPane left = new JSplitPane(JSplitPane.VERTICAL_SPLIT,bookCover,new JScrollPane(bookDesc));

        //打开"一触即展"特性
        left.setOneTouchExpandable(true);

        //设置分隔条的大小

        left.setDividerSize(10);
        //设置分割面板根据组件的大小调整最佳布局
        left.resetToPreferredSizes();
        
        //创建一个水平分隔面板
        JSplitPane content = new JSplitPane(JSplitPane.HORIZONTAL_SPLIT, left, bookList);
        //设置支持连续布局
        content.setContinuousLayout(true);

        jf.add(content);

        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.pack();
        jf.setVisible(true);


    }

    public static void main(String[] args) {
        new SplitPaneTest().init();
    }

}
```



### 3.3.2 使用JTabledPane

JTabbedPane可以很方便地在窗口上放置多个标签页，每个标签页相当于获得了一个与外部容器具有相同大小的组件摆放区域。通过这种方式， 就可以在一个容器里放置更多的组件 ， 例如右击桌面上的" 我的电脑 "图标，在弹出的快捷菜单里单击"属性 " 菜单工页 ， 就可以看 到 一个"系统属性 " 对话框 ，这个对话框里包含了 若干个标签页。

![](./images/properties.jpg)

如果需要使用JTabbedPane在窗口上创建标签页 ，则可以按如下步骤进行:

1. 创建JTabbedPane对象

```java
 JTabbedPane(int tabPlacement, int tabLayoutPolicy):
	tabPlacement:
		指定标签标题的放置位置，可以选择 SwingConstants中的四个常量：TOP、LEFT、BOTTOM、RIGHT
	tabLaoutPolicy:
		指定当窗口不能容纳标签页标题时的布局策略，可以选择JTabbedPane.WRAP_TAB_LAYOUT和JTabbedPane.SCROLL_TAB_LAYOUT
```

2. 通过JTabbedPane对象堆标签进行增删改查

```java
addTab(String title, Icon icon, Component component, String tip):添加标签
	title:标签的名称
	icon:标签的图标
	component:标签对应的组件
	tip:光标放到标签上的提示
	
insertTab(String title, Icon icon, Component component, String tip, int index):插入标签页
	title:标签的名称
	icon:标签的图标
	component:标签对应的组件
	tip:光标放到标签上的提示
	index:在哪个索引处插入标签页
setComponentAt(int index, Component component):修改标签页对应的组件
	index:修改哪个索引处的标签
	component:标签对应的组件
removeTabAt(int index):
	index:删除哪个索引处的标签
```

3. 设置当前显示的标签页

```java
setSelectedIndex(int index):设置哪个索引处的标签被选中
```

4. 设置JTabbedPane的其他属性

```java
setDisabledIconAt(int index, Icon disabledIcon): 将指定位置的禁用图标设置为 icon，该图标也可以是null表示不使用禁用图标。
setEnabledAt(int index, boolean enabled): 设置指定位置的标签页是否启用。
setTitleAt(int index, String title): 设置指定位置标签页的标题为 title，该title可以是null,这表明设置该标签页的标题为空。
setToolTipTextAt(int index, String toolTipText): 设置指定位置标签页的提示文本 。
```

5. 为JTabbedPane设置监听器

```java
addChangeListener(ChangeListener l)
```

**案例：**

​	请使用JTabbedPane完成下图功能：

​	![](./images/JTabbedPane.jpg)

**演示代码：**

```java
import javax.swing.*;
import javax.swing.event.ChangeEvent;
import javax.swing.event.ChangeListener;

public class JTabbedPaneTest {
    JFrame jf = new JFrame("测试JTabbedPane");



    JTabbedPane tabbedPane = new JTabbedPane(SwingConstants.TOP,JTabbedPane.WRAP_TAB_LAYOUT);

    public void init(){


        //设置jf大小
        jf.setBounds(400,400,400,400);
        //设置jf大小不能变化
        jf.setResizable(false);


        ImageIcon icon = new ImageIcon(ImagePathUtil.getRealPath("3\\open.gif"));
        //添加标签
        tabbedPane.addTab("用户管理",icon,new JList<String>(new String[]{"用户一","用户二","用户三"}));
        tabbedPane.addTab("商品管理",new JList<String>(new String[]{"商品一","商品二","商品三"}));
        tabbedPane.addTab("订单管理",icon,new JList<String>(new String[]{"订单一","订单二","订单三"}));

        //设置第二个标签默认选中
        tabbedPane.setSelectedIndex(1);
        //设置第一个标签不能用
        tabbedPane.setEnabledAt(0,false);

        tabbedPane.addChangeListener(new ChangeListener() {
            @Override
            public void stateChanged(ChangeEvent e) {
                int selectedIndex = tabbedPane.getSelectedIndex();
                JOptionPane.showMessageDialog(jf,"选中了第"+(selectedIndex+1)+"个标签");
            }
        });


        jf.add(tabbedPane);
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.setVisible(true);

    }


    public static void main(String[] args) {
        new JTabbedPaneTest().init();
    }
}

```



### 3.3.3 使用JLayeredPane、JDesktopPane、JInternalFrame

#### 3.3.3.1 JLayeredPane

JLayeredPane是 一个代表有层 次深度的容器 ， 它允许组件在需要 时 互相重叠。当向JLayeredPane容器中添加组件时， 需要为该组件指定一个深度索引 ， 其中层次索引较高 的层里的组件位于其他层的组件之上。

![](./images/JLayeredPane1.gif)

JLayeredPane 还将容器的层次深度分成几个默认层 ，程序只是将组件放入相应 的层 ，从而可以更容易地确保组件的正确重叠 ， 无须为组件指定具体的深度索引。JLayeredPane 提供了如下几个默认层：

1. DEFAULT_LAYER:大多数组件位于标准层，这是最底层；
2. PALETTE_LAYER : 调色板层位于默认层之上 。该层对于浮动工具栏和调色板很有用，因此可以位于其他组件之上 。
3. MODAL_LAYER: 该层用于显示模式对话框。它们将出现在容器中所有工具栏 、调色板或标准组件的上面 。
4. POPUP_LAYER : 该层用于显示右键菜单 ， 与对话框 、工具提示和普通组件关联的弹出式窗口将出现在对应的对话框、工具提示和普通组件之上。
5. DRAG_LAYER: 该层用于放置拖放过程中的组件(关于拖放操作请看下一节内 容) ，拖放操作中的组件位于所有组件之上 。 一旦拖放操作结束后 ， 该组件将重新分配到其所属的正常层。

**JLayeredPane 方法：**

1. moveToBack(Component c)：把当前组件c移动到所在层的所有组件的最后一个位置；
2. moveToFront(Component c)：把当前组件c移动到所在层的所有组件的第一个位置；
3. setLayer(Component c, int layer)：更改组件c所处的层；

需要注意的是，往JLayeredPane中添加组件，如果要显示，则必须手动设置该组件在容器中显示的位置以及大小。



**案例：**

​	使用JLayeredPane完成下图效果：

​	![](./images/JLayeredPane2.jpg)

**演示代码：**

```java
import cn.itcast.swing.util.ImagePathUtil;

import javax.swing.*;
import java.awt.*;

public class JLayeredPaneTest {
    JFrame jf = new JFrame("测试JLayeredPane");
    JLayeredPane layeredPane = new JLayeredPane();

    //自定义组件，继承JPanel
    private class ContentPanel extends JPanel{

        public ContentPanel(int xPos,int yPos,String title,String ico){
            //设置边框
            setBorder(BorderFactory.createTitledBorder(BorderFactory.createEtchedBorder(),title));
            JLabel label = new JLabel(new ImageIcon(ImagePathUtil.getRealPath("3\\"+ico)));
            add(label);
            setBounds(xPos,yPos,160,220);

        }

    }

    public void init(){
        //向LayeredPane中添加三个组件，往JLayeredPane中添加组件，都必须手动的设置组件显示的位置和大小，才能显示出来

        layeredPane.add(new ContentPanel(10,20,"java自学宝典","java.png"),JLayeredPane.MODAL_LAYER);
        layeredPane.add(new ContentPanel(100,60,"Android基础教程","android.png"),JLayeredPane.DEFAULT_LAYER);
        layeredPane.add(new ContentPanel(80,100,"轻量级javaEE企业应用","ee.png"),JLayeredPane.DRAG_LAYER);

        layeredPane.setPreferredSize(new Dimension(300,400));


        jf.add(layeredPane);
        jf.pack();
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.setVisible(true);


    }

    public static void main(String[] args) {
        new JLayeredPaneTest().init();
    }
}
```

#### 3.3.3.2 JDesktopPane和JInternalFrame

JDesktopPane是JLayeredPane的子类，这种容器在开发中会更常用很多应用程序都需要启动多个内部窗口来显示信息（典型的比如IDEA、NotePad++），这些内部窗口都属于同一个外部窗口，当外部窗 口 最小化时， 这些内部窗口都被隐藏起来。在 Windows 环境中，这
种用户界面被称为多文档界面 C Multiple Document Interface, MDI) 。

使用 Swing 可以非常简单地创建出这种 MDI 界面 ， 通常，内部窗口有自己的标题栏、标题、图标、三个窗口按钮，并允许拖动改变内部窗口 的大小和位置，但内部窗口不能拖出外部窗口。

​	![](./images/内部窗口1.jpg)

JDesktopPane 需要和 JIntemalFrame 结合使用，其中JDesktopPane 代表一 个虚拟桌面 ，而JIntemalFrame则用于创建内部窗口。使用 JDesktopPane 和 JIntemalFrame 创建内部窗口按如下步骤进行即可:

1. 创建 一 个 JDesktopPane 对象,代表虚拟桌面

```java
JDesktopPane()
```

2. 使用 JIntemalFrame 创建一个内部窗口

```java
JInternalFrame(String title, boolean resizable, boolean closable, boolean maximizable, boolean iconifiable):
	title: 内部窗口标题
	resizable:是否可改变大小
	closeble: 是否可关闭
	maximizable: 是否可最大化
	iconifiable:是否可最小化
```

3. 一旦获得了内部窗口之后，该窗口的用法和普通窗口的用法基本相似， 一样可以指定该窗口的布局管理器， 一样可以向窗口内添加组件、改变窗口图标等。
4. 将该内部窗口以合适大小、在合适位置显示出来 。与普通窗口类似的是， 该窗口默认大小是 0x0像素，位于0，0 位置(虚拟桌面的左上角处)，并且默认处于隐藏状态，程序可以通过如下代码将内部窗口显示出来:

```java
reshape(int x, int y, int width, int height):设置内部窗口的大小以及在外部窗口中的位置；
show():设置内部窗口可见
```

5. 将内部窗口添加到 JDesktopPane 容器中，再将 JDesktopPane 容器添加到其他容器中。

**案例：**

​	请使用JDesktopPane和JInternalFrame完成下图效果：

​	![](./images/JInternalFrame.jpg)

**演示代码：**

```java
import cn.itcast.swing.util.ImagePathUtil;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;

public class JInternalFrameTest {
    final int DESKTOP_WIDTH = 480;
    final int DESKTOP_HEIGHT = 360;
    final int FRAME_DISTANCE = 20;

    //创建外部窗口
    JFrame jf = new JFrame("测试JInternalFrame");

    //创建虚拟桌面
    JDesktopPane desktop = new JDesktopPane();

    //定义内部窗口为的大小
    private int width = 230;
    private int height = DESKTOP_HEIGHT;

    //定义下一个内部窗口的横轴坐标
    private int nextFrameX = 0;

    //为外部窗口定义两个菜单
    JMenu fileMenu = new JMenu("文件");


    //定义Action，用于快捷创建菜单项和工具按钮
    Action newAction = new AbstractAction("新建",new ImageIcon(ImagePathUtil.getRealPath("3\\new.png"))) {
        @Override
        public void actionPerformed(ActionEvent e) {
            //创建内部窗口
            JInternalFrame iframe = new JInternalFrame("新文档",true,true,true,true);
            //往内部窗口中添加一个8行40列的文本框
            iframe.add(new JScrollPane(new JTextArea(8,40)));
            //将内部窗口添加到虚拟桌面中
            desktop.add(iframe);
            //设置内部窗口的原始位置
            iframe.reshape(nextFrameX,0,width,height);
            //使该窗口可见
            iframe.show();

            //计算下一个内部窗口的位置
            nextFrameX+=FRAME_DISTANCE;


            if (nextFrameX>DESKTOP_WIDTH-width){
                nextFrameX=0;
            }
        }
    };

    Action exitAction = new AbstractAction("退出",new ImageIcon(ImagePathUtil.getRealPath("3\\exit.png"))) {
        @Override
        public void actionPerformed(ActionEvent e) {
            //结束当前程序
            System.exit(0);
        }
    };


    public void init(){

        //为窗口安装菜单条
        JMenuBar menuBar = new JMenuBar();

        jf.setJMenuBar(menuBar);
        menuBar.add(fileMenu);
        fileMenu.add(newAction);
        fileMenu.add(exitAction);



        //设置虚拟桌面的最佳大小
        desktop.setPreferredSize(new Dimension(DESKTOP_WIDTH,DESKTOP_HEIGHT));

        //将虚拟桌面添加到外部窗口中
        jf.add(desktop);

        jf.pack();
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.setVisible(true);

    }


    public static void main(String[] args) {
        new JInternalFrameTest().init();
    }

}
```

## 3.4 JProcessBar、ProcessMonitor、BoundedRangeModel实现进度条

进度条是图形界面中广泛使用的GUI 组件，当复制一个较大的文件时，操作系统会显示一个进度条，用于标识复制操作完成的比例 : 当启动 Eclipse 等程序时， 因为需要加载较多的资源 ， 故而启动速度较慢 ， 程序也会在启动过程中显示一个进度条 ， 用以表示该软件启动完成的比例 ……

### 3.4.1 创建进度条

使用JProgressBar创建进度条的步骤：

1. 创建JProgressBar对象

```java
public JProgressBar(int orient, int min, int max):
	orint:方向
	min:最小值
	max:最大值
```

2. 设置属性

```java
setBorderPainted(boolean b):设置进度条是否有边框
setIndeterminate(boolean newValue):设置当前进度条是不是进度不确定的进度条，如果是，则将看到一个滑块在进度条中左右移动
setStringPainted(boolean b)：设置进度条是否显示当前完成的百分比
```

3. 获取和设置当前进度条的进度状态

```java
setValue(int n):设置当前进度值
double getPercentComplete():获取进度条的完成百分比
String  getStrin():返回进度字符串的当前值
```

**案例：**

​	请使用JProgressBar完成下图效果：

​	![](./images/JProgressBar.jpg)

**演示代码：**

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class JProgressTest {

    JFrame jf = new JFrame("测试进度条");
    //创建一个垂直进度条
    JProgressBar bar = new JProgressBar(JProgressBar.HORIZONTAL);

    JCheckBox indeterminate = new JCheckBox("不确定进度");
    JCheckBox noBorder = new JCheckBox("不绘制边框");

    public void init(){

        Box box = new Box(BoxLayout.Y_AXIS);
        box.add(indeterminate);
        box.add(noBorder);

        jf.setLayout(new FlowLayout());
        jf.add(box);

        //把进度条添加到jf窗口中
        jf.add(bar);

        //设置进度条的最大值和最小值
        bar.setMinimum(0);
        bar.setMaximum(100);

        //设置进度条中绘制完成百分比
        bar.setStringPainted(true);

        //根据选择决定是否绘制进度条边框
        noBorder.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                boolean flag = noBorder.isSelected();
                bar.setBorderPainted(!flag);
            }
        });

        //根据选择决定是否是不确定进度条
        indeterminate.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                boolean flag = indeterminate.isSelected();
                bar.setIndeterminate(flag);
                //不绘制百分比，因为之前设置了绘制百分比
                bar.setStringPainted(!flag);
            }
        });

        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.pack();
        jf.setVisible(true);


        //通过循环不断改变进度条的完成进度
        for (int i = 0; i <= 100; i++) {
            //改变进度条的完成进度
            bar.setValue(i);

            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

    }

    public static void main(String[] args) {
        new JProgressTest().init();
    }
}

```

在刚才的程序中，通过for循环来不断的更新进度条的进度，这仅仅是为了演示而已，实际开发中这样的操作是没有意义的。通常情况下是不断的检测一个耗时任务的完成情况，然后才去更新进度条的进度。下面的代码通过Timer定时器和Runnable接口，对上述代码进行改进，其运行结果没有变化，知识修改到了进度条进度更新的逻辑。

```java
import javax.swing.*;
import javax.swing.event.ChangeEvent;
import javax.swing.event.ChangeListener;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class JProgressTest2 {

    JFrame jf = new JFrame("测试进度条");
    //创建一个垂直进度条
    JProgressBar bar = new JProgressBar(JProgressBar.HORIZONTAL);

    JCheckBox indeterminate = new JCheckBox("不确定进度");
    JCheckBox noBorder = new JCheckBox("不绘制边框");

    public void init(){

        Box box = new Box(BoxLayout.Y_AXIS);
        box.add(indeterminate);
        box.add(noBorder);

        jf.setLayout(new FlowLayout());
        jf.add(box);

        //把进度条添加到jf窗口中
        jf.add(bar);

        //开启耗时任务
        SimulatedActivity simulatedActivity = new SimulatedActivity(100);
        new Thread(simulatedActivity).start();


        //设置进度条的最大值和最小值
        bar.setMinimum(0);
        bar.setMaximum(simulatedActivity.getAmount());

        //设置进度条中绘制完成百分比
        bar.setStringPainted(true);

        //根据选择决定是否绘制进度条边框
        noBorder.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                boolean flag = noBorder.isSelected();
                bar.setBorderPainted(!flag);
            }
        });

        //根据选择决定是否是不确定进度条
        indeterminate.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                boolean flag = indeterminate.isSelected();
                bar.setIndeterminate(flag);
                //不绘制百分比，因为之前设置了绘制百分比
                bar.setStringPainted(!flag);
            }
        });

        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.pack();
        jf.setVisible(true);




        //通过定时器，不断的读取simulatedActivity中的current值，更新进度条的进度
        Timer timer = new Timer(300, new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                bar.setValue(simulatedActivity.getCurrent());
            }
        });
        timer.start();
        //监听进度条的变化，如果进度完成为100%，那么停止定时器
        bar.addChangeListener(new ChangeListener() {
            @Override
            public void stateChanged(ChangeEvent e) {
                if (   bar.getValue()==bar.getMaximum()){
                    timer.stop();
                }
            }
        });


    }

    public static void main(String[] args) {
        new JProgressTest2().init();
    }

    //定义一个线程任务，模拟耗时操作
    private class SimulatedActivity implements Runnable{
        //内存可见
        private volatile int current = 0;
        private int amount;

        public SimulatedActivity(int amount) {
            this.amount = amount;
        }

        public int getCurrent() {
            return current;
        }

        public void setCurrent(int current) {
            this.current = current;
        }


        public int getAmount() {
            return amount;
        }

        public void setAmount(int amount) {
            this.amount = amount;
        }

        @Override
        public void run() {
            //通过循环，不断的修改current的值，模拟任务完成量
            while(current<amount){
                try {
                    Thread.sleep(50);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                current++;
            }
        }
    }
}

```

之前我们学习过，其实Swing中很多组件的界面与数据都采用了MVC的设计思想：

​	![](./images/mvc.png)

Swing 组件大都将外观显示和 内部数据分离 ， JProgressBar 也不例外， JProgressBar 组件有一个内置的用于保存其状态数据的Model对象 ， 这个对象由BoundedRangeModel对象表示，程序调用JProgressBar对象的方法完成进度百分比的设置，监听进度条的数据变化，其实都是通过它内置的BoundedRangeModel对象完成的。下面的代码是对之前代码的改进，通过BoundedRangeModel完成数据的设置，获取与监听。

```java
import javax.swing.*;
import javax.swing.event.ChangeEvent;
import javax.swing.event.ChangeListener;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class JProgressTest3 {

    JFrame jf = new JFrame("测试进度条");
    //创建一个垂直进度条
    JProgressBar bar = new JProgressBar(JProgressBar.HORIZONTAL);

    JCheckBox indeterminate = new JCheckBox("不确定进度");
    JCheckBox noBorder = new JCheckBox("不绘制边框");

    public void init(){

        Box box = new Box(BoxLayout.Y_AXIS);
        box.add(indeterminate);
        box.add(noBorder);

        jf.setLayout(new FlowLayout());
        jf.add(box);

        //把进度条添加到jf窗口中
        jf.add(bar);

        //开启耗时任务
        SimulatedActivity simulatedActivity = new SimulatedActivity(100);
        new Thread(simulatedActivity).start();


        //设置进度条的最大值和最小值
        bar.getModel().setMinimum(0);
        bar.getModel().setMaximum(simulatedActivity.getAmount());

        //设置进度条中绘制完成百分比
        bar.setStringPainted(true);

        //根据选择决定是否绘制进度条边框
        noBorder.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                boolean flag = noBorder.isSelected();
                bar.setBorderPainted(!flag);
            }
        });

        //根据选择决定是否是不确定进度条
        indeterminate.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                boolean flag = indeterminate.isSelected();
                bar.setIndeterminate(flag);
                //不绘制百分比，因为之前设置了绘制百分比
                bar.setStringPainted(!flag);
            }
        });

        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.pack();
        jf.setVisible(true);




        //通过定时器，不断的读取simulatedActivity中的current值，更新进度条的进度
        Timer timer = new Timer(300, new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                bar.getModel().setValue(simulatedActivity.getCurrent());
            }
        });
        timer.start();
        //监听进度条的变化，如果进度完成为100%，那么停止定时器
        bar.getModel().addChangeListener(new ChangeListener() {
            @Override
            public void stateChanged(ChangeEvent e) {
                if (   bar.getModel().getValue()==bar.getModel().getMaximum()){
                    timer.stop();
                }
            }
        });


    }

    public static void main(String[] args) {
        new JProgressTest3().init();
    }

    //定义一个线程任务，模拟耗时操作
    private class SimulatedActivity implements Runnable{
        //内存可见
        private volatile int current = 0;
        private int amount;

        public SimulatedActivity(int amount) {
            this.amount = amount;
        }

        public int getCurrent() {
            return current;
        }

        public void setCurrent(int current) {
            this.current = current;
        }


        public int getAmount() {
            return amount;
        }

        public void setAmount(int amount) {
            this.amount = amount;
        }

        @Override
        public void run() {
            //通过循环，不断的修改current的值，模拟任务完成量
            while(current<amount){
                try {
                    Thread.sleep(50);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                current++;
            }
        }
    }
}
```

### 3.4.2 创建进度对话框

ProgressMonitor的用法与JProgressBa 的用法基本相似，只是ProgressMonitor可以直接创 建一个进度对话框，它提供了下面的构造器完成对话框的创建：

```java
 public ProgressMonitor(Component parentComponent,Object message,String note, int min,int max):
	parentComponent:对话框的父组件
	message:对话框的描述信息
	note:对话框的提示信息
	min:进度条的最小值
	max:进度条的最大值
```

使用 ProgressMonitor 创建的对话框里包含的进度条是非常固定的，程序甚至不能设置该进度条是否包含边框(总是包含边框) ， 不能设置进度不确定，不能改变进度条的方向(总是水平方向) 。

**案例：**

​	使用ProgressMonitor完成下图效果：

​	![](./images/ProgressMonitor.jpg)



**演示代码：**

```java
import javax.swing.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class ProgressMonitorTest {

    Timer timer;
    public void init(){
        final SimulatedActivity simulatedActivity = new SimulatedActivity(100);
        final Thread targetThread= new Thread(simulatedActivity);
        targetThread.start();


        ProgressMonitor dialog = new ProgressMonitor(null, "等待任务完成", "已完成：", 0, simulatedActivity.getAmount());

        timer = new Timer(300, new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                dialog.setProgress(simulatedActivity.getCurrent());
                if (dialog.isCanceled()){
                    timer.stop();
                    targetThread.interrupt();
                    System.exit(0);
                }
            }
        });
        timer.start();


        System.out.println("aaa");
    }

    public static void main(String[] args) {
        new ProgressMonitorTest().init();
    }

    //定义一个线程任务，模拟耗时操作
    private class SimulatedActivity implements Runnable{
        //内存可见
        private volatile int current = 0;
        private int amount;

        public SimulatedActivity(int amount) {
            this.amount = amount;
        }

        public int getCurrent() {
            return current;
        }

        public void setCurrent(int current) {
            this.current = current;
        }


        public int getAmount() {
            return amount;
        }

        public void setAmount(int amount) {
            this.amount = amount;
        }

        @Override
        public void run() {
            //通过循环，不断的修改current的值，模拟任务完成量
            while(current<amount){
                try {
                    Thread.sleep(50);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                current++;
            }
        }
    }

}
```

## 3.5 JList、JComboBox实现列表框

无论从哪个角度来看， JList 和 JComboBox 都是极其相似的，它们都有一个列表框，只是 JComboBox的列表框需要 以下拉方式显示出来; JList 和 JComboBox 都可以通过调用 setRendererO方法来改变列表项的表现形式 。甚至维护这两个组件的 Model 都是相似的， JList 使用 ListModel, JComboBox 使用ComboBoxModel ，而 ComboBoxModel 是 ListModel 的子类 。

### 3.5.1 简单列表框

使用JList或JComboBox实现简单列表框的步骤：

1. 创建JList或JComboBox对象

```java
JList(final E[] listData):创建JList对象，把listData数组中的每项内容转换成一个列表项展示
JList(final Vector<? extends E> listData):创建JList对象，把listData数组中的每项内容转换成一个列表项展示
JComboBox(E[] items):
JComboBox(Vector<E> items):
```

2. 设置JList或JComboBox的外观行为

```java
---------------------------JList----------------------------------------------
addSelectionInterval(int anchor, int lead):在已经选中列表项的基础上，增加选中从anchor到lead索引范围内的所有列表项
setFixedCellHeight(int height)/setFixedCellWidth(int width):设置列表项的高度和宽度
setLayoutOrientation(int layoutOrientation)：设置列表框的布局方向
setSelectedIndex(int index)：设置默认选中项
setSelectedIndices(int[] indices)：设置默认选中的多个列表项
setSelectedValue(Object anObject,boolean shouldScroll)：设置默认选中项，并滚动到该项显示
setSelectionBackground(Color selectionBackground)：设置选中项的背景颜色
setSelectionForeground(Color selectionForeground)：设置选中项的前景色
setSelectionInterval(int anchor, int lead):设置从anchor到lead范围内的所有列表项被选中
setSelectionMode(int selectionMode)：设置选中模式，默认没有限制，也可以设置为单选或者区域选中
setVisibleRowCount(int visibleRowCount)：设置列表框的可是高度足以显示多少行列表项
---------------------------JComboBox---------------------------------------------- 
setEditable(boolean aFlag)：设置是否可以直接修改列表文本框的值，默认为不可以
setMaximumRowCount(int count)：设置列表框的可是高度足以显示多少行列表项
setSelectedIndex(int anIndex)：设置默认选中项
setSelectedItem(Object anObject)：根据列表项的值，设置默认选中项
```

3. 设置监听器，监听列表项的变化，JList通过addListSelectionListener完成，JComboBox通过addItemListener完成

**案例：**

​	使用JList和JComboBox完成下图效果：

​	![](./images/JList_JComboBox.jpg)

**演示代码：**

```java
import javax.swing.*;
import javax.swing.border.EtchedBorder;
import javax.swing.border.TitledBorder;
import javax.swing.event.ListSelectionEvent;
import javax.swing.event.ListSelectionListener;
import java.awt.*;
import java.awt.event.ItemEvent;
import java.awt.event.ItemListener;
import java.util.List;
import java.util.Vector;

public class ListTest {
    JFrame mainWin = new JFrame("列表框测试");
    String[] books = {"java自学宝典","轻量级javaEE企业应用实战","Android基础教程","jQuery实战教程","SpringBoot企业级开发"};

    //用一个字符串数组来创建一个JList对象
    JList<String> bookList = new JList<>(books);
    JComboBox<String> bookSelector;

    //定义 布局选择按钮 所在的面板
    JPanel layoutPanel = new JPanel();
    ButtonGroup layoutGroup = new ButtonGroup();

    //定义 选择模式按钮 所在面板
    JPanel selectModePanel = new JPanel();
    ButtonGroup selectModeGroup = new ButtonGroup();

    JTextArea favorite = new JTextArea(4,40);

    public void init(){
        //设置JList的可视高度可以同时展示3个列表项
        bookList.setVisibleRowCount(3);

        //设置Jlist默认选中第三项到第五项
        bookList.setSelectionInterval(2,4);
        addLayoutButton("纵向滚动",JList.VERTICAL);
        addLayoutButton("纵向换行",JList.VERTICAL_WRAP);
        addLayoutButton("横向换行",JList.HORIZONTAL_WRAP);

        addSelectModeButton("无限制", ListSelectionModel.MULTIPLE_INTERVAL_SELECTION);
        addSelectModeButton("单选", ListSelectionModel.SINGLE_SELECTION);
        addSelectModeButton("单范围", ListSelectionModel.SINGLE_INTERVAL_SELECTION);

        Box listBox = Box.createVerticalBox();
        //将JList组件放置到JScrollPane中，并将JScrollPane放置到box中
        listBox.add(new JScrollPane(bookList));
        listBox.add(layoutPanel);
        listBox.add(selectModePanel);

        //为JList添加事件监听器
        bookList.addListSelectionListener(new ListSelectionListener() {
            @Override
            public void valueChanged(ListSelectionEvent e) {
                List<String> selectedValuesList = bookList.getSelectedValuesList();
                favorite.setText("");
                for (String s : selectedValuesList) {
                    favorite.append(s+"\n");
                }
            }
        });


        //定义一个Vector对象
        Vector<String> bookCollection = new Vector<>();
        List<String> books = List.of("java自学宝典","轻量级javaEE企业应用实战","Android基础教程","jQuery实战教程","SpringBoot企业级开发");
        bookCollection.addAll(books);

        //创建JComboBox对象
        bookSelector = new JComboBox<>(bookCollection);

        //为JComboBox添加事件监听器
        bookSelector.addItemListener(new ItemListener() {
            @Override
            public void itemStateChanged(ItemEvent e) {
                Object selectedItem = bookSelector.getSelectedItem();
                favorite.setText(selectedItem.toString());
            }
        });

        //设置JComboBox的列表项可编辑
        bookSelector.setEditable(true);

        //设置下拉列表的可视高度最多显示4个列表项
        bookSelector.setMaximumRowCount(4);

        JPanel panel = new JPanel();
        panel.add(bookSelector);
        Box box = Box.createHorizontalBox();
        box.add(listBox);
        box.add(panel);

        JPanel favoritePanel = new JPanel();
        favoritePanel.setLayout(new BorderLayout());
        favoritePanel.add(new JScrollPane(favorite));
        favoritePanel.add(new JLabel("您最喜欢的图书："),BorderLayout.NORTH);

        mainWin.add(box);
        mainWin.add(favoritePanel,BorderLayout.SOUTH);
        mainWin.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        mainWin.pack();
        mainWin.setVisible(true);

    }



    public void addLayoutButton(String label,int orientation){
        layoutPanel.setBorder(new TitledBorder(new EtchedBorder(),"确定选项布局"));

        JRadioButton button = new JRadioButton(label);

        layoutPanel.add(button);
        //默认选中第一个按钮
        if (layoutGroup.getButtonCount()==0){
            button.setSelected(true);
        }
        layoutGroup.add(button);
        button.addActionListener(e->{
            //改变列表框里列表项的布局方向
            bookList.setLayoutOrientation(orientation);
        });

    }

    public void addSelectModeButton(String label,int selectMode){
        selectModePanel.setBorder(new TitledBorder(new EtchedBorder(),"确定选择模式"));
        JRadioButton button = new JRadioButton(label);
        selectModePanel.add(button);
        if (selectModeGroup.getButtonCount()==0){
            button.setSelected(true);
        }
        selectModeGroup.add(button);
        button.addActionListener(e->{
            bookList.setSelectionMode(selectMode);
        });


    }

    public static void main(String[] args) {
        new ListTest().init();
    }
}
```

### 3.5.2 不强制存储列表项的ListModel和ComboBoxModel

与JProgressBar一样，JList和JComboBox也采用了MVC的设计模式，JList和JComboBox只负责外观的显示，而组件底层的状态数据则由对应的Model来维护。JList对应的Model是ListModel接口，JComboBox对应的Model是ComboBox接口，其代码如下：

```java
public interface ListModel<E>{

  int getSize();

  E getElementAt(int index);

  void addListDataListener(ListDataListener l);

  void removeListDataListener(ListDataListener l);
}

public interface ComboBoxModel<E> extends ListModel<E> {

  void setSelectedItem(Object anItem);

  Object getSelectedItem();
}
```

从上面接口来看，这个 ListMode l 不管 JList 里的所有列表项的存储形式，它甚至不强制存储所有的列表项，只要 ListModel的实现类提供了getSize()和 getElementAt()两个方法 ， JList 就可以根据该ListModel 对象来生成列表框 。ComboBoxModel 继承了 ListModel ，它添加了"选择项"的概念，选择项代表 JComboBox 显示区域内可见的列表项 。 

在使用JList和JComboBox时，除了可以使用jdk提供的Model实现类，程序员自己也可以根据需求，自己定义Model的实现类，实现对应的方法使用。

**案例：**

​	自定义NumberListModel和NumberComboBoxModel实现类，允许使用数值范围来创建JList和JComboBox

​	![](./images/ListModelTest.jpg)

**演示代码：**

```java
import javax.swing.*;
import java.math.BigDecimal;
import java.math.RoundingMode;

public class NumberListModel extends AbstractListModel<BigDecimal> {

    protected BigDecimal start;
    protected BigDecimal end;
    protected BigDecimal step;


    public NumberListModel(double start,double end,double step) {
        this.start = new BigDecimal(start);
        this.end = new BigDecimal(end);
        this.step = new BigDecimal(step);
    }

    @Override
    public int getSize() {
        int floor = (int) Math.floor(end.subtract(start).divide(step,2, RoundingMode.HALF_DOWN).doubleValue());
        return floor+1;
    }

    @Override
    public BigDecimal getElementAt(int index) {
        return BigDecimal.valueOf(index).multiply(step).add(start).setScale(1,RoundingMode.HALF_DOWN);
    }
}




import javax.swing.*;
import java.math.BigDecimal;
import java.math.RoundingMode;

public class NumberComboBoxModel extends NumberListModel implements ComboBoxModel<BigDecimal> {
    //用于保存用户选中项的索引
    private int selectId = 0;

    public NumberComboBoxModel(double start, double end, double step) {
        super(start, end, step);
    }

    //设置选择项
    @Override
    public void setSelectedItem(Object anItem) {
        if (anItem instanceof BigDecimal){
            BigDecimal target = (BigDecimal) anItem;
            selectId = target.subtract(super.start).divide(super.step,2, RoundingMode.HALF_DOWN).intValue();
        }
    }

    //获取选中项的索引
    @Override
    public BigDecimal getSelectedItem() {
         return BigDecimal.valueOf(selectId).multiply(step).add(start).setScale(1,RoundingMode.HALF_DOWN);

    }
}


import javax.swing.*;
import javax.swing.event.ListSelectionEvent;
import javax.swing.event.ListSelectionListener;
import java.awt.*;
import java.awt.event.ItemEvent;
import java.awt.event.ItemListener;
import java.math.BigDecimal;
import java.util.List;

public class ListModelTest {
    JFrame mainWin = new JFrame("测试ListModel");

    //根据NumberListModel对象创建一个JList
    JList<BigDecimal> numScopeList = new JList<>(new NumberListModel(1,21,2));

    //根据NumberComboBoxModel对象创建一个JComboBox
    JComboBox<BigDecimal> numScopeSelector = new JComboBox<>(new NumberComboBoxModel(0.1,1.2,0.1));

    JTextField showVal = new JTextField(10);

    public void init(){
        //JList可视高度可同时显示四个列表项
        numScopeList.setVisibleRowCount(4);

        //默认选中第三项到第五项
        numScopeList.setSelectionInterval(2,4);

        //设置每个列表项具有指定高度和宽度
        numScopeList.setFixedCellHeight(30);
        numScopeList.setFixedCellWidth(90);

        //为numScopeList添加监听器
        numScopeList.addListSelectionListener(new ListSelectionListener() {
            @Override
            public void valueChanged(ListSelectionEvent e) {
                //获取用户选中的所有数字
                List<BigDecimal> selectedValuesList = numScopeList.getSelectedValuesList();
                showVal.setText("");
                for (BigDecimal bigDecimal : selectedValuesList) {
                    showVal.setText(showVal.getText()+bigDecimal.toString()+", ");
                }
            }
        });

        //设置下拉列表的可视高度可显示5个列表项
        numScopeSelector.setMaximumRowCount(5);

        Box box = Box.createHorizontalBox();
        box.add(new JScrollPane(numScopeList));

        JPanel p = new JPanel();
        p.add(numScopeSelector);
        box.add(p);

        //为numberScopeSelector添加监听器
        numScopeSelector.addItemListener(new ItemListener() {
            @Override
            public void itemStateChanged(ItemEvent e) {
                Object value = numScopeSelector.getSelectedItem();
                showVal.setText(value.toString());
            }
        });


        JPanel bottom = new JPanel();
        bottom.add(new JLabel("您选择的值是："));
        bottom.add(showVal);

        mainWin.add(box);
        mainWin.add(bottom, BorderLayout.SOUTH);
        mainWin.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        mainWin.pack();
        mainWin.setVisible(true);

    }

    public static void main(String[] args) {
        new ListModelTest().init();
    }
}
```

### 3.5.3 强制存储列表项的DefaultListModel和DefaultComboBoxModel

前面只是介绍了如何创建 JList 、 JComboBox 对象， 当 调用 JList 和 JComboBox构造方法时时传入数组或 Vector 作为参数，这些数组元素或集合元素将会作为列表项。当使用JList 或 JComboBox 时 常常还需要动态地增加、删除列表项,例如JCombox提供了下列方法完成增删操作：

```java
addItem(E item):添加一个列表项
insertItemAt(E item, int index)：向指定索引处插入一个列表项
removeAllItems()：删除所有列表项
removeItem(Object anObject)：删除指定列表项
removeItemAt(int anIndex)：删除指定索引处的列表项
```

JList 并没有提供这些类似的方法。如果需要创建一个可以增加、删除列表项的 JList 对象，则应该在创建 JLi st 时显式使用 DefaultListModel作为构造参数 。因为 DefaultListModel 作为 JList 的 Model，它负责维护 JList 组件的所有列表数据，所以可以通过向 DefaultListModel 中添加、删除元素来实现向 JList 对象中增加 、删除列表项 。DefaultListModel 提供了如下几个方法来添加、删除元素:

```java
add(int index, E element): 在该 ListModel 的指定位置处插入指定元素 。
addElement(E obj): 将指定元素添加到该 ListModel 的末尾 。
insertElementAt(E obj, int index): 在该 ListModel 的指定位置处插入指定元素 。
Object remove(int index): 删除该 ListModel 中指定位置处的元素 
removeAllElements(): 删 除该 ListModel 中的所有元素，并将其的大小设置为零 。
removeElement(E obj): 删除该 ListModel 中第一个与参数匹配的元素。
removeElementAt(int index): 删除该 ListModel 中指定索引处的元素 。
removeRange(int 企omIndex ， int toIndex): 删除该 ListModel 中指定范围内的所有元素。
set(int index, E element) : 将该 ListModel 指定索引处的元素替换成指定元素。
setElementAt(E obj, int index): 将该 ListModel 指定索引处的元素替换成指定元素。
```

**案例：**

​	使用DefaultListModel完成下图效果：

​	![](./images/DefaultListModel.jpg)

**演示代码：**

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class DefaultListModelTest {

    JFrame mainWin = new JFrame("测试DefaultListModel");

    //定义一个JList对象
    JList<String> bookList;
    //定义一个DefaultListModel对象
    DefaultListModel<String> bookModel = new DefaultListModel<>();

    JTextField bookName = new JTextField(20);

    JButton removeBtn = new JButton("删除选中图书");
    JButton addBtn = new JButton("添加指定图书");

    public void init(){
        //向bookModel中添加元素
        bookModel.addElement("java自学宝典");
        bookModel.addElement("轻量级javaEE企业应用实战");
        bookModel.addElement("Android基础教程");
        bookModel.addElement("jQuery实战教程");
        bookModel.addElement("SpringBoot企业级开发");

        //根据DefaultListModel创建一个JList对象
        bookList = new JList<>(bookModel);
        //设置最大可视高度
        bookList.setVisibleRowCount(4);

        //设置只能单选
        bookList.setSelectionMode(ListSelectionModel.SINGLE_SELECTION);

        //为addBtn添加事件监听器
        addBtn.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                //当bookName文本框内容不为空时添加列表项
                if (!bookName.getText().trim().equals("")){

                    bookModel.addElement(bookName.getText());
                }

            }
        });

        //为removeBtn添加事件监听器
        removeBtn.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                int selectedIndex = bookList.getSelectedIndex();
                if (selectedIndex>=0){

                    bookModel.remove(selectedIndex);
                }
            }
        });

        JPanel p = new JPanel();
        p.add(bookName);
        p.add(addBtn);
        p.add(removeBtn);

        mainWin.add(new JScrollPane(bookList));
        mainWin.add(p, BorderLayout.SOUTH);
        mainWin.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        mainWin.pack();
        mainWin.setVisible(true);

    }

    public static void main(String[] args) {
        new DefaultListModelTest().init();
    }

}

```

### 3.5.4 使用ListCellRenderer改变列表外观

前面程序中的 JList 和 JComboBox 采用的都是简单的字符串列表项， 实际上 ， JList 和 JComboBox还可以支持图标列表项，如果在创建 JList 或 JComboBox 时传入图标数组，则创建的 JList 和 JComboBox的列表项就是图标 。

如果希望列表项是更复杂 的组件，例如，希望像 QQ 程序那样每个列表项既有图标，此时需要使用ListCellRenderer接口的实现类对象，自定义每个条目组件的渲染过程：

```java
public interface ListCellRenderer<E>
{
    Component getListCellRendererComponent(
        JList<? extends E> list,//列表组件
        E value,//当前列表项的值额索引
        int index,//当前列表项d
        boolean isSelected,//当前列表项是否被选中
        boolean cellHasFocus);//当前列表项是否获取了焦点
}
```

通过JList的`setCellRenderer(ListCellRenderer<? super E> cellRenderer)`方法，把自定义的ListCellRenderer对象传递给JList，就可以按照自定义的规则绘制列表项组件了。



**案例：**

​	使用ListCellRenderer实现下图效果：

​	![](./images/ListCellRenderer.jpg)

**演示代码：**

```java
import cn.itcast.swing.util.ImagePathUtil;

import javax.swing.*;
import java.awt.*;

public class ListCellRendererTest {

    private JFrame mainWin = new JFrame("好友列表");

    private String[] friends = {
            "李清照",
            "苏格拉底",
            "李白",
            "弄玉",
            "虎头"
    };

    //定义一个JList对象
    JList friendsList = new JList(friends);

    public void init() {
        //设置JList使用ImageCellRenderer作为列表项绘制器
        friendsList.setCellRenderer(new ImageCellRenderer());

        mainWin.add(new JScrollPane(friendsList));
        mainWin.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        mainWin.pack();
        mainWin.setVisible(true);

    }


    public static void main(String[] args) {
        new ListCellRendererTest().init();
    }

    class ImageCellRenderer extends JPanel implements ListCellRenderer {


        private ImageIcon icon;
        private String name;
        //定义绘制单元格的背景色
        private Color background;
        //定义绘制单元格的前景色
        private Color foreground;


        @Override
        public Component getListCellRendererComponent(JList list, Object value, int index, boolean isSelected, boolean cellHasFocus) {

            icon = new ImageIcon(ImagePathUtil.getRealPath("9\\" + value + ".gif"));
            name = value.toString();
            background = isSelected ? list.getSelectionBackground() : list.getBackground();
            foreground = isSelected ? list.getSelectionForeground() : list.getForeground();

            //返回当前JPanel对象，作为列表项绘制器
            return this;
        }

        @Override
        protected void paintComponent(Graphics g) {
            int width = icon.getImage().getWidth(null);
            int height = icon.getImage().getHeight(null);

            //填充背景矩形
            g.setColor(background);
            g.fillRect(0,0,getWidth(),getHeight());

            g.setColor(foreground);
            //绘制好友头像
            g.drawImage(icon.getImage(),getWidth()/2-width/2,10,null);

            //绘制好友昵称
            g.setFont(new Font("SansSerif",Font.BOLD,18));
            g.drawString(name,getWidth()/2-name.length()*10,height+30);
        }


        @Override
        public Dimension getPreferredSize() {
            return new Dimension(60,80);
        }
    }
}
```



## 3.6 JTree、TreeModel实现树

树也是图形用户界面中使用非常广泛的 GUI 组件，例如使用 Windows 资源管理器时，将看到如下图所示的目录树:

![](./images/目录树.jpg)



如上图所示的树，代表计算机世界里的树，它从自然界实际的树抽象而来 。 计算机世界里的树是由一系列具有严格父子关系的节点组成的，每个节点既可以是其上一级节点的子节点，也可以是其下一级节点的父节点，因此同一个节点既可以是父节点，也可以是子节点(类似于一个人，他既是他儿子的父亲，又是他父亲的儿子)。

**按照结点是否包含子结点，可以把结点分为下面两类：**

​	普通结点：包含子结点的结点；

​	叶子结点：没有子结点的结点；

**按照结点是否具有唯一的父结点，可以把结点分为下面两类：**

​	根结点：没有父结点的结点，计算机中，一棵树只能有一个根结点

​	普通结点：具有唯一父结点的结点

使用 Swing 里的 Jtree 、 TreeModel 及其相关的辅助类可以很轻松地开发出计算机世界里的树。

### 3.6.1 创建树

Swing 使用 JTree 对 象来代表一棵树，JTree 树中结点可以使用 TreePath 来标识，该对象封装了当前结点及其所有的父结点。

**当一个结点具有子结点时，该结点有两种状态：**

​	展开状态:当父结点处于展开状态时，其子结点是可见的；

​	折叠状态: 当父结点处于折叠状态时，其子结点都是不可见的 。

如果某个结点是可见的，则该结点的父结点(包括直接的、间接的父结点)都必须处于展开状态，只要有任意一个父结点处于折叠状态，该结点就是不可见的 。

**JTree常用构造方法：**

```java
JTree(TreeModel newModel):使用指定 的数据模型创建 JTree 对象，它默认显示根结点。
JTree(TreeNode root): 使用 root 作为根节 点创建 JTree 对象，它默认显示根结点 。
JTree(TreeNode root, boolean asksAllowsChildren): 使用root作为根结点创建JTree对象，它默认显示根结点。 asksAllowsChildren 参数控制怎样的结点才算叶子结点，如果该参数为 true ，则只有当程序使用 setAllowsChildren(false)显式设置某个结点不允许添加子结点时(以后也不会拥有子结点) ，该结点才会被 JTree 当成叶子结点:如果该参数为 false ，则只要某个结点当时没有子结点(不管以后是否拥有子结点) ，该结点都会被 JTree 当成叶子结点。
```

**TreeNode继承体系及使用：**

​	![](G:/%E7%A0%94%E5%8F%91/GUI/%E6%96%87%E6%A1%A3/images/TreeNode.png)	![](G:/%E7%A0%94%E5%8F%91/GUI/%E6%96%87%E6%A1%A3/images/%E7%9B%AE%E5%BD%95%E6%A0%912.jpg)

在构建目录树时，可以先创建很多DefaultMutableTreeNode对象，并调用他们的add方法构建好子父级结构，最后根据根结点构建一个JTree即可。

**案例：**

​	使用JTree和TreeNode完成下图效果：

​	![](G:/%E7%A0%94%E5%8F%91/GUI/%E6%96%87%E6%A1%A3/images/SimpleJTree.jpg)

**演示代码：**

```java
import javax.swing.*;
import javax.swing.tree.DefaultMutableTreeNode;

public class SimpleJTree {
    JFrame jf = new JFrame("简单树");

    JTree tree;
    DefaultMutableTreeNode root;
    DefaultMutableTreeNode guangdong;
    DefaultMutableTreeNode guangxi;
    DefaultMutableTreeNode foshan;
    DefaultMutableTreeNode shantou;
    DefaultMutableTreeNode guilin;
    DefaultMutableTreeNode nanning;

    public void init(){
        //依次创建所有结点
        root = new DefaultMutableTreeNode("中国");
        guangdong = new DefaultMutableTreeNode("广东");
        guangxi = new DefaultMutableTreeNode("广西");
        foshan = new DefaultMutableTreeNode("佛山");
        shantou = new DefaultMutableTreeNode("汕头");
        guilin = new DefaultMutableTreeNode("桂林");
        nanning = new DefaultMutableTreeNode("南宁");


        //通过add()方法建立父子层级关系
        guangdong.add(foshan);
        guangdong.add(shantou);
        guangxi.add(guilin);
        guangxi.add(nanning);
        root.add(guangdong);
        root.add(guangxi);

        //依据根结点，创建JTree
        tree = new JTree(root);

        jf.add(new JScrollPane(tree));
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.pack();
        jf.setVisible(true);

    }


    public static void main(String[] args) {
        new SimpleJTree().init();
    }
}
```

**JTree的其他外观设置方法：**

```java
tree.putClientProperty( "JTree.lineStyle", "None"):设置结点之间没有连接线
tree.putClientProperty("JTree.lineStyle" , "Horizontal")：设置结点之间只有水平分割线
tree.setShowsRootHandles(true)：设置根结点有"展开、折叠"图标
tree.setRootVisible(false)：隐藏根结点
```

**DefaultMutableTreeNode其他成员方法：**

```java
Enumeration breadthFirstEnumerationO/preorderEnumeration(): 按广度优先的顺序遍历以此结点为根的子树，并返回所有结点组成的枚举对象 。
Enumeration depthFirstEnumerationO/postorderEnumeration(): 按深度优先的顺序遍历以此结点为根的子树，并返回所有结点组成的枚举对象 。
DefaultMutableTreeNode getNextSibling(): 返回此结点的下一个兄弟结点 。
TreeNode getParent(): 返回此结点的父结点 。 如果此结点没有父结点，则返回null 。
TreeNode[] getPath(): 返回从根结点到达此结点的所有结点组成的数组。
DefaultMutableTreeNode getPreviousSibling(): 返回此结点的上一个兄弟结点。
TreeNode getRoot(): 返回包含此结点的树的根结点 。
TreeNode getSharedAncestor(DefaultMutableTreeNode aNode): 返回此结点和aNode最近的共同祖先 。
int getSiblingCount(): 返回此结点的兄弟结点数 。
boolean isLeaf(): 返回该结点是否是叶子结点 。
boolean isNodeAncestor(TreeNode anotherNode): 判断anotherNode是否是当前结点的祖先结点(包括父结点) 。
boolean isNodeChild(TreeNode aNode): 如果aNode是此结点的子结点，则返回true。
boolean isNodeDescendant(DefaultMutableTreeNode anotherNode): 如果 anotherNode 是此结点的后代，包括是此结点本身、此结点的子结点或此结点的子结点的后代，都将返回true 。
boolean isNodeRelated(DefaultMutableTreeNode aNode) : 当aNode和当前结点位于同一棵树中时返回 true 。
boolean isNodeSibling(TreeNode anotherNode): 返回anotherNode是否是当前结点的兄弟结点 。
boolean isRoot(): 返回当前结点是否是根结点 。
Enumeration pathFromAncestorEnumeration(TreeNode ancestor): 返回从指定祖先结点到当前结点的所有结点组成的枚举对象 。
```

### 3.6.2 拖动、编辑树结点

JTree 生成的树默认是不可编辑的，不可以添加、删除结点，也不可以改变结点数据 :如果想让某个 JTree 对象变成可编辑状态，则可以调用 JTree 的setEditable(boolean b)方法，传入 true 即可把这棵树变成可编辑的树(可以添加、删除结点，也可以改变结点数据) 。

**编辑树结点的步骤：**

1. 获取当前被选中的结点：

```java
获取当前被选中的结点，会有两种方式：
	一：
		通过JTree对象的某些方法，例如 TreePath getSelectionPath()等，得到一个TreePath对象，包含了从根结点到当前结点路径上的所有结点；
		调用TreePath对象的 Object getLastPathComponent()方法，得到当前选中结点
	二：
		调用JTree对象的 Object getLastSelectedPathComponent() 方法获取当前被选中的结点
```

1. 调用DefaultTreeModel数据模型有关增删改的一系列方法完成编辑，方法执行完后，会自动重绘JTree

**案例：**

​	使用JTree以及DefaultTreeModel、DefaultMutableTreeNode、TreePath完成下图效果：

​	![](G:/%E7%A0%94%E5%8F%91/GUI/%E6%96%87%E6%A1%A3/images/EditTree.jpg)

**演示代码：**

```java
import javax.swing.*;
import javax.swing.tree.*;
import java.awt.*;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;
import java.awt.event.MouseListener;

public class EditTree {

    JFrame jf ;
    JTree tree;

    //JTree关联的数据模型对象
    DefaultTreeModel model;

    //定义几个初始结点
    DefaultMutableTreeNode root = new DefaultMutableTreeNode("中国");
    DefaultMutableTreeNode guangdong = new DefaultMutableTreeNode("广东");
    DefaultMutableTreeNode guangxi = new DefaultMutableTreeNode("广西");
    DefaultMutableTreeNode foshan = new DefaultMutableTreeNode("佛山");
    DefaultMutableTreeNode shantou = new DefaultMutableTreeNode("汕头");
    DefaultMutableTreeNode guilin = new DefaultMutableTreeNode("桂林");
    DefaultMutableTreeNode nanning = new DefaultMutableTreeNode("南宁");

    //定义需要被拖动的TreePath
    TreePath movePath;

    //定义按钮，完成操作
    JButton addSiblingBtn = new JButton("添加兄弟结点");
    JButton addChildBtn = new JButton("添加子结点");
    JButton deleteBtn = new JButton("删除结点");
    JButton editBtn = new JButton("编辑当前结点");

    public void init(){

        //通过add()方法建立父子层级关系
        guangdong.add(foshan);
        guangdong.add(shantou);
        guangxi.add(guilin);
        guangxi.add(nanning);
        root.add(guangdong);
        root.add(guangxi);

        jf = new JFrame("可编辑结点的树");
        tree = new JTree(root);

        //获取JTree关联的数据模型TreeModel对象
        model = (DefaultTreeModel) tree.getModel();

        //设置JTree可编辑
        tree.setEditable(true);

        //创建鼠标事件监听器
        MouseListener ml = new MouseAdapter() {

            //按下鼠标时，获得被拖动的结点
            @Override
            public void mousePressed(MouseEvent e) {
                //如果需要唯一确定某个结点，则必须通过TreePath来获取
                TreePath tp = tree.getPathForLocation(e.getX(), e.getY());
                if (tp!=null){
                    movePath = tp;
                }
            }

            //松开树表示，确定即将被拖入到的父结点
            @Override
            public void mouseReleased(MouseEvent e) {

                TreePath tp = tree.getPathForLocation(e.getX(), e.getY());
                if (tp!=null && movePath!=null){
                    //阻止向子结点拖动
                    if (movePath.isDescendant(tp) && movePath!=tp){
                        JOptionPane.showMessageDialog(jf,"目标结点是被移动结点的子结点，无法移动！","非法移动",JOptionPane.WARNING_MESSAGE);
                    }
                    //不是向子结点移动，并且鼠标按下和松开也不是同一个结点

                    if (movePath!=tp){
                        //add方法内部，先将该结点从原父结点删除，然后再把该结点添加到新结点中
                        DefaultMutableTreeNode tartParentNode = (DefaultMutableTreeNode) tp.getLastPathComponent();
                        DefaultMutableTreeNode moveNode = (DefaultMutableTreeNode) movePath.getLastPathComponent();
                        tartParentNode.add(moveNode);

                        movePath=null;
                        tree.updateUI();
                    }
                }
            }
        };

        //为JTree添加鼠标监听器
        tree.addMouseListener(ml);

        JPanel panel = new JPanel();

        addSiblingBtn.addActionListener(e -> {
            //获取选中结点
            DefaultMutableTreeNode selectedNode = (DefaultMutableTreeNode) tree.getLastSelectedPathComponent();

            //如果结点为空，则直接返回
            if (selectedNode==null){
                return;
            }

            //获取该选中结点的父结点
            DefaultMutableTreeNode parent = (DefaultMutableTreeNode) selectedNode.getParent();

            //如果父结点为空，则直接返回
            if (parent==null){
                return;
            }

            //创建一个新结点
            DefaultMutableTreeNode newNode = new DefaultMutableTreeNode("新结点");

            //获取选中结点的索引
            int selectedIndex = parent.getIndex(selectedNode);

            //在选中位置插入新结点
            model.insertNodeInto(newNode,parent,selectedIndex);

            //----------显示新结点---------------
            //获取从根结点到新结点的所有结点
            TreeNode[] pathToRoot = model.getPathToRoot(newNode);

            //使用指定的结点数组创建TreePath
            TreePath treePath = new TreePath(pathToRoot);

            //显示指定的treePath
            tree.scrollPathToVisible(treePath);


        });

        panel.add(addSiblingBtn);

        addChildBtn.addActionListener(e -> {
            //获取选中结点
            DefaultMutableTreeNode selectedNode = (DefaultMutableTreeNode) tree.getLastSelectedPathComponent();

            if (selectedNode==null){
                return ;
            }

            //创建新结点
            DefaultMutableTreeNode newNode = new DefaultMutableTreeNode("新结点");

            //model.insertNodeInto(newNode,selectedNode,selectedNode.getChildCount());使用TreeModel的方法添加，不需要手动刷新UI
            selectedNode.add(newNode);//使用TreeNode的方法添加，需要手动刷新UI

            //显示新结点

            TreeNode[] pathToRoot = model.getPathToRoot(newNode);
            TreePath treePath = new TreePath(pathToRoot);
            tree.scrollPathToVisible(treePath);

            //手动刷新UI
            tree.updateUI();

        });

        panel.add(addChildBtn);

        deleteBtn.addActionListener(e -> {

            DefaultMutableTreeNode selectedNode = (DefaultMutableTreeNode) tree.getLastSelectedPathComponent();

            if (selectedNode!=null && selectedNode.getParent()!=null){
                model.removeNodeFromParent(selectedNode);
            }

        });

        panel.add(deleteBtn);

        //实现编辑结点的监听器
        editBtn.addActionListener(e -> {

            TreePath selectionPath = tree.getSelectionPath();

            if (selectionPath!=null){
                //编辑选中结点
                tree.startEditingAtPath(selectionPath);
            }

        });

        panel.add(editBtn);

        jf.add(new JScrollPane(tree));
        jf.add(panel, BorderLayout.SOUTH);

        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.pack();
        jf.setVisible(true);

    }

    public static void main(String[] args) {
        new EditTree().init();
    }
}

```

### 3.6.3 监听结点事件

**修改JTree的选择模式：**

JTree 专门提供了 一个 TreeSelectionModel 对象来保存该 JTree 选中状态的信息 。 也就是说，JTree组件背后隐藏了两个 model 对象 ， 其中TreeModel 用于保存该 JTree 的所有节点数据 ， 而TreeSelectionModel 用于保存该 JTree的所有选中状态的信息 。

程序可以改变 JTree 的选择模式 ， 但必须先获取该 JTree 对应的 TreeSelectionMode1 对象 ， 再调用该对象的 setSelectionMode(int mode);方法来设置该JTree的选择模式 ，其中model可以有如下3种取值：

1. TreeSelectionModel.CONTIGUOUS_TREE_SELECTION: 可 以连续选中多个 TreePath 。
2. TreeSelectionModel.DISCONTIGUOUS_TREE_SELECTION : 该选项对于选择没有任何限制 。
3. TreeSelectionModel.SINGLE_TREE_SELECTION: 每次只能选择一个 TreePath 。

**为JTree添加监听器:**

1. addTreeExpansionListener(TreeExpansionListener tel) : 添加树节点展开/折叠事件的监听器。
2. addTreeSelectionListener(TreeSelectionListener tsl) : 添加树节点选择事件的监听器。

**案例：**

​	实现下图效果：

​	![](G:/%E7%A0%94%E5%8F%91/GUI/%E6%96%87%E6%A1%A3/images/SelectJTree.jpg)

**演示代码：**

```java
import javax.swing.*;
import javax.swing.tree.DefaultMutableTreeNode;

public class SelectJTree {
    JFrame jf = new JFrame("监听树的选择事件");

    JTree tree;

    DefaultMutableTreeNode root = new DefaultMutableTreeNode("中国");
    DefaultMutableTreeNode guangdong = new DefaultMutableTreeNode("广东");
    DefaultMutableTreeNode guangxi = new DefaultMutableTreeNode("广西");
    DefaultMutableTreeNode foshan = new DefaultMutableTreeNode("佛山");
    DefaultMutableTreeNode shantou = new DefaultMutableTreeNode("汕头");
    DefaultMutableTreeNode guilin = new DefaultMutableTreeNode("桂林");
    DefaultMutableTreeNode nanning = new DefaultMutableTreeNode("南宁");

    JTextArea eventTxt = new JTextArea(5, 20);

    public void init() {

        //通过add()方法建立父子层级关系
        guangdong.add(foshan);
        guangdong.add(shantou);
        guangxi.add(guilin);
        guangxi.add(nanning);
        root.add(guangdong);
        root.add(guangxi);

        tree = new JTree(root);

        //添加监听器
        tree.addTreeSelectionListener(e -> {
            if (e.getOldLeadSelectionPath()!=null){
                eventTxt.append("原选中结点的路径："+e.getOldLeadSelectionPath().toString()+"\n");
            }

            eventTxt.append("新选中结点的路径："+e.getNewLeadSelectionPath().toString()+"\n");
        });

        tree.setShowsRootHandles(true);
        tree.setRootVisible(true);

        Box box = Box.createHorizontalBox();
        box.add(new JScrollPane(tree));
        box.add(new JScrollPane(eventTxt));

        jf.add(box);
        jf.pack();
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.setVisible(true);
    }

    public static void main(String[] args) {
        new SelectJTree().init();
    }
}
```

### 3.6.4 使用DefaultTreeCellRenderer改变结点外观

JTree默认的外观是比较单一的，它提供了如下几种改变结点外观的方式：

1. 使用 DefaultTreeCellRenderer 直接改变节点的外观，这种方式可 以 改变整棵树所有节点 的字体、颜色和图标 。
2. 为 JTree 指定 DefaultTreeCellRenderer 的扩展类对象作为 JTree 的节点绘制器，该绘制器负责为不同节点使用不同的字体、颜色和图标。通常使用这种方式来改变节点的外观 。
3. 为 JTree 指定一个实现 TreeCellRenderer 接口的节点绘制器，该绘制器可以为不同的节点自由绘制任意内容，这是最复杂但最灵活的节点绘制器 。

第 一种方式最简单 ， 但灵活性最差 ，因为它会改变整棵树所有节点的外观 。 在这种情况下 ， Jtree的所有节点依然使用相同的图标 ，相当于整体替换了 Jtree 中 节点的所有默认图标 。 用户指定 的节点图标未必就比 JTree 默认的图标美观 。

DefaultTreeCellRenderer 提供了如下几个方法来修改节点的外观：

```java
setBackgroundNonSelectionColor(Color newColor): 设置用于非选定节点的背景颜色 。
setBackgroundSelectionColor(Color newColor): 设置节点在选中状态下的背景颜色 。
setBorderSelectionColor(Color newColor): 设置选中状态下节点的边框颜色 。
setClosedIcon(Icon newIcon): 设置处于折叠状态下非叶子节点的图标 。
setFont(Font font) : 设置节点文本 的 字体。
setLeaflcon(Icon newIcon): 设置叶子节点的图标 。
setOpenlcon(Icon newlcon): 设置处于展开状态下非叶子节 点的图标。
setTextNonSelectionColor(Color newColor): 设置绘制非选中状态下节点文本的颜色 。
setTextSelectionColor(Color newColor): 设置绘制选中状态下节点文本的颜色 。
```

**案例：**

​	使用DefaultTreeCellRenderer完成下图效果：

​	![](G:/%E7%A0%94%E5%8F%91/GUI/%E6%96%87%E6%A1%A3/images/CellRender1.jpg)

**演示代码：**

```java
import cn.itcast.swing.util.ImagePathUtil;

import javax.swing.*;
import javax.swing.tree.DefaultMutableTreeNode;
import javax.swing.tree.DefaultTreeCellRenderer;
import java.awt.*;

public class ChangeAllCellRender {

    JFrame jf = new JFrame("改变所有结点外观");

    JTree tree;

    DefaultMutableTreeNode root = new DefaultMutableTreeNode("中国");
    DefaultMutableTreeNode guangdong = new DefaultMutableTreeNode("广东");
    DefaultMutableTreeNode guangxi = new DefaultMutableTreeNode("广西");
    DefaultMutableTreeNode foshan = new DefaultMutableTreeNode("佛山");
    DefaultMutableTreeNode shantou = new DefaultMutableTreeNode("汕头");
    DefaultMutableTreeNode guilin = new DefaultMutableTreeNode("桂林");
    DefaultMutableTreeNode nanning = new DefaultMutableTreeNode("南宁");

    public void init(){
        //通过add()方法建立父子层级关系
        guangdong.add(foshan);
        guangdong.add(shantou);
        guangxi.add(guilin);
        guangxi.add(nanning);
        root.add(guangdong);
        root.add(guangxi);

        tree = new JTree(root);

        //创建一个DefaultTreeCellRenderer对象
        DefaultTreeCellRenderer cellRenderer = new DefaultTreeCellRenderer();
        //设置非选定结点的背景颜色
        cellRenderer.setBackgroundNonSelectionColor(new Color(220,220,220));
        //设置选中结点的背景色
        cellRenderer.setBackgroundSelectionColor(new Color(140,140,140));
        //设置选中状态下结点的边框颜色
        cellRenderer.setBorderSelectionColor(Color.BLACK);
        //设置处于折叠状态下非叶子结点的图标
        cellRenderer.setClosedIcon(new ImageIcon(ImagePathUtil.getRealPath("10\\close.gif")));
        //设置结点文本的字体
        cellRenderer.setFont(new Font("SansSerif",Font.BOLD,16));
        //设置叶子结点图标
        cellRenderer.setLeafIcon(new ImageIcon(ImagePathUtil.getRealPath("10\\leaf.png")));
        //设置处于展开状态下非叶子结点图标跑
        cellRenderer.setOpenIcon(new ImageIcon(ImagePathUtil.getRealPath("10\\open.gif")));
        //设置绘制非选中状态下结点文本颜色
        cellRenderer.setTextNonSelectionColor(new Color(255,0,0));
        //设置选中状态下结点的文本颜色
        cellRenderer.setTextSelectionColor(new Color(0,0,255));

        tree.setCellRenderer(cellRenderer);

        tree.setShowsRootHandles(true);

        tree.setRootVisible(true);

        jf.add(new JScrollPane(tree));
        jf.pack();
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.setVisible(true);

    }


    public static void main(String[] args) {
        new ChangeAllCellRender().init();
    }

}
```

### 3.6.5 扩展DefaultTreeCellRenderer改变结点外观

DefaultTreeCellRenderer 实现类实现了TreeCellRenderer接口，该接口里只有 一个用于绘制节点内容的方法: getTreeCellRendererComponent() ， 该方法负责绘制 JTree 节点 。学习JList的时候，如果要绘制JList的列表项外观的内容，需要实现ListCellRenderer 接口，通过重写getTreeCellRendererComponent()方法返回一个Component 对象 ， 该对象就是 JTree 的节点组件 。两者之间非常类似

DefaultTreeCellRende rer 类继承了JLabel，实现 getTreeCellRendererComponent()方法时返回 this ，即返回一个特殊的 JLabel 对象 。 如果需要根据节点内容来改变节点的外观，则可以再次扩展DefaultTreeCellRenderer 类，并再次重写它提供的 getTreeCellRendererComponent()方法。



**案例：**

​	自定义类继承DefaultTreeCellRenderer,重写getTreeCellRendererComponent()方法，实现下图效果：

​	![](G:/%E7%A0%94%E5%8F%91/GUI/%E6%96%87%E6%A1%A3/images/%E6%89%A9%E5%B1%95DefaultTreeCellRenderer.jpg)

**演示代码：**

```java
import cn.itcast.swing.util.ImagePathUtil;

import javax.swing.*;
import javax.swing.tree.DefaultMutableTreeNode;
import javax.swing.tree.DefaultTreeCellRenderer;
import java.awt.*;

public class ExtendsDefaultCellTreeRenderer {

    JFrame jf = new JFrame("根据结点类型定义图标");

    JTree tree;

    //定义几个初始结点
    DefaultMutableTreeNode root = new DefaultMutableTreeNode(new NodeData(DBObjectType.ROOT,"数据库导航"));
    DefaultMutableTreeNode salaryDb = new DefaultMutableTreeNode(new NodeData(DBObjectType.DATABASE,"公司工资数据库"));
    DefaultMutableTreeNode customerDb = new DefaultMutableTreeNode(new NodeData(DBObjectType.DATABASE,"公司客户数据库"));
    DefaultMutableTreeNode employee = new DefaultMutableTreeNode(new NodeData(DBObjectType.TABLE,"员工表"));
    DefaultMutableTreeNode attend = new DefaultMutableTreeNode(new NodeData(DBObjectType.TABLE,"考勤表"));
    DefaultMutableTreeNode concat = new DefaultMutableTreeNode(new NodeData(DBObjectType.TABLE,"联系方式表"));
    DefaultMutableTreeNode id = new DefaultMutableTreeNode(new NodeData(DBObjectType.INDEX,"员工ID"));
    DefaultMutableTreeNode name = new DefaultMutableTreeNode(new NodeData(DBObjectType.COLUMN,"姓名"));
    DefaultMutableTreeNode gender = new DefaultMutableTreeNode(new NodeData(DBObjectType.COLUMN,"性别"));

    public void init(){
        //通过结点的add方法，建立结点的父子关系

        root.add(salaryDb);
        root.add(customerDb);

        salaryDb.add(employee);
        salaryDb.add(attend);

        customerDb.add(concat);

        concat.add(id);
        concat.add(name);
        concat.add(gender);

        tree = new JTree(root);

        tree.setCellRenderer(new MyRenderer());

        tree.setShowsRootHandles(true);
        tree.setRootVisible(true);

        //设置使用windows外观风格
        try {
            UIManager.setLookAndFeel("com.sun.java.swing.plaf.windows.WindowsLookAndFeel");
        } catch (Exception e) {
            e.printStackTrace();
        }

        //更新JTree的UI外观
        SwingUtilities.updateComponentTreeUI(tree);

        jf.add(new JScrollPane(tree));
        jf.pack();
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.setVisible(true);

    }

    public static void main(String[] args) {
        new ExtendsDefaultCellTreeRenderer().init();
    }

    class MyRenderer extends DefaultTreeCellRenderer{
        //初始化5个图标
        ImageIcon rootIcon = new ImageIcon(ImagePathUtil.getRealPath("10\\root.gif"));
        ImageIcon databaseIcon = new ImageIcon(ImagePathUtil.getRealPath("10\\database.gif"));
        ImageIcon tableIcon = new ImageIcon(ImagePathUtil.getRealPath("10\\table.gif"));
        ImageIcon columnIcon = new ImageIcon(ImagePathUtil.getRealPath("10\\column.gif"));
        ImageIcon indexIcon = new ImageIcon(ImagePathUtil.getRealPath("10\\index.gif"));

        @Override
        public Component getTreeCellRendererComponent(JTree tree, Object value, boolean sel, boolean expanded, boolean leaf, int row, boolean hasFocus) {
            //执行父类默认的绘制结点操作
            super.getTreeCellRendererComponent(tree,value,sel,expanded,leaf,row,hasFocus);
            DefaultMutableTreeNode  node = (DefaultMutableTreeNode) value;

            NodeData data = (NodeData) node.getUserObject();
            //根据结点数据中的nodeType决定结点的图标
            ImageIcon icon = null;
            switch (data.nodeType){
                case DBObjectType.ROOT:
                    icon = rootIcon;
                    break;
                case DBObjectType.DATABASE:
                    icon = databaseIcon;
                    break;
                case DBObjectType.TABLE:
                    icon = tableIcon;
                    break;
                case DBObjectType.COLUMN:
                    icon = columnIcon;
                    break;
                case DBObjectType.INDEX:
                    icon = indexIcon;
                    break;
            }

            //改变图标
            this.setIcon(icon);

            return this;
        }
    }


    //定义一个NodeData类，用于封装结点数据
    class NodeData{
        public int nodeType;
        public String nodeData;

        public NodeData(int nodeType, String nodeData) {
            this.nodeType = nodeType;
            this.nodeData = nodeData;
        }

        @Override
        public String toString() {
            return this.nodeData;
        }
    }

    //定义一个接口，该接口里包含数据库对象类型的常量
    interface  DBObjectType{
        int ROOT=0;
        int DATABASE=1;
        int TABLE=2;
        int COLUMN=3;
        int INDEX=4;
    }

}
```

### 3.6.6 实现TreeCellRenderer接口改变结点外观

这种改变结点外观的方式是最灵活的，程序实现TreeCellRenderer接口时同样需要实现getTreeCellRendererComponent()方法，该方法可以返回任意类型的组件，该组件将作为JTree的结点。通过这种方式可以最大程度的改变结点的外观。

**案例：**

​	自定义类，继承JPanel类，实现TreeCellRenderer接口，完成下图效果：

​	![](G:/%E7%A0%94%E5%8F%91/GUI/%E6%96%87%E6%A1%A3/images/TreeCellRenderer.jpg)

**演示代码：**

```java
import cn.itcast.swing.util.ImagePathUtil;

import javax.swing.*;
import javax.swing.tree.DefaultMutableTreeNode;
import javax.swing.tree.TreeCellRenderer;
import java.awt.*;

public class CustomerTreeNode {

    JFrame jf = new JFrame("定制树的结点");

    JTree tree;

    //定义几个初始结点

    DefaultMutableTreeNode friends = new DefaultMutableTreeNode("我的好友");
    DefaultMutableTreeNode qingzhao = new DefaultMutableTreeNode("李清照");
    DefaultMutableTreeNode suge = new DefaultMutableTreeNode("苏格拉底");
    DefaultMutableTreeNode libai = new DefaultMutableTreeNode("李白");
    DefaultMutableTreeNode nongyu = new DefaultMutableTreeNode("弄玉");
    DefaultMutableTreeNode hutou = new DefaultMutableTreeNode("虎头");

    public void init() {

        friends.add(qingzhao);
        friends.add(suge);
        friends.add(libai);
        friends.add(nongyu);
        friends.add(hutou);

        tree = new JTree(friends);

        tree.setShowsRootHandles(true);
        tree.setRootVisible(true);


        tree.setCellRenderer(new ImageCellRenderer());



        jf.add(new JScrollPane(tree));
        jf.pack();
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.setVisible(true);

    }

    public static void main(String[] args) {
        new CustomerTreeNode().init();
    }


    class ImageCellRenderer extends JPanel implements TreeCellRenderer {

        private ImageIcon icon;
        private String name;
        //定义绘制单元格时的背景色
        private Color background;
        //定义绘制单元格时的前景色
        private Color foreground;


        @Override
        public Component getTreeCellRendererComponent(JTree tree, Object value, boolean selected, boolean expanded, boolean leaf, int row, boolean hasFocus) {
            icon = new ImageIcon(ImagePathUtil.getRealPath("10\\" + value + ".gif"));

            name = value.toString();

            background = hasFocus ? new Color(140, 200, 235) : new Color(255, 255, 255);
            foreground = hasFocus ? new Color(255,255,3) : new Color(0,0,0);
            //返回当前JPanel作为结点
            return this;
        }

        //重写paintComponent改变JPanel的外观

        @Override
        protected void paintComponent(Graphics g) {
            int imageWidth = icon.getImage().getWidth(null);
            int imageHeight = icon.getImage().getHeight(null);
            g.setColor(background);
            g.fillRect(0,0,getWidth(),getHeight());

            g.setColor(foreground);
            //绘制好友图标
            g.drawImage(icon.getImage(),getWidth()/2-imageWidth/2,10,null);

            //绘制好友姓名
            g.setFont(new Font("SansSerif",Font.BOLD,18));

            g.drawString(name,getWidth()/2-name.length()*10,imageHeight+30);

        }


        //设置当前组件结点最佳大小
        @Override
        public Dimension getPreferredSize() {
            return new Dimension(80,80);
        }
    }
}
```



## 3.7 JTable、TableModel实现表格

表格也是GUI程序中常用的组件，表格是一个由多行、多列组成的二维显示区 。 Swing 的 JTable 以及相关类提供了这种表格支持 ， 通过使用 JTable 以及相关类，程序既可以使用简单的代码创建出表格来显示二维数据，也可以开发出功能丰富的表格，还可以为表格定制各种显示外观、编辑特性 。

### 3.7.1 创建简单表格

**使用JTable创建简单表格步骤:**

1. 创建一个一维数组，存储表格中每一列的标题
2. 创建一个二维数组，存储表格中每一行数据，其中二维数组内部的每个一维数组，代表表格中的一行数据
3. 根据第一步和第二步创建的一维数组和二维数组，创建JTable对象
4. 把JTable添加到其他容器中显示



**案例：**

​	使用JTable实现下图效果：

​	![](G:/%E7%A0%94%E5%8F%91/GUI/%E6%96%87%E6%A1%A3/images/SimpleTable.jpg)

**演示代码：**

```java
import javax.swing.*;

public class SimpleTable {

    JFrame jf = new JFrame("简单表格");

    JTable table;

    //定义二维数组作为表格数据

    Object[][] tableData = {

            new Object[]{"李清照",29,"女"},
            new Object[]{"苏格拉底",56,"男"},
            new Object[]{"李白",35,"男"},
            new Object[]{"弄玉",18,"女"},
            new Object[]{"虎头",2,"男"},

    };

    //定义一个一维数组，作为列标题
    Object[] columnTitle = {"姓名","年龄","性别"};

    public void init(){
        //以二维数组和一维数组来创建一个JTable对象

        table = new JTable(tableData,columnTitle);

        jf.add(new JScrollPane(table));
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.pack();
        jf.setVisible(true);
    }

    public static void main(String[] args) {
        new SimpleTable().init();
    }
}

```

在上面实现的简单表格中，大概有如下几个功能：

1. 当表格高度不足以显示所有的数据行时，该表格会自动显示滚动条 。
2. 把鼠标移动到两列之间的分界符时，鼠标形状会变成可调整大小的形状，表明用户可以自由调整表格列的大小 。
3. 在表格列上按下鼠标并拖动时，可以将表格的整列拖动到其他位置 。
4. 当单击某一个单元格时，系统会自动选中该单元格所在的行 。    
5. 当双击某一个单元格时，系统会自动进入该单元格的修改状态 。    



**JTable调整列：**

JTable提供了一个setAutoResizeMode(int mode)方法用来调整表格的格式，该方法可以接收下面几个值：

1. JTable.AUTO_RESIZE_OFF: 关闭表格的自动调整功能。当调整某一列的宽度时，其他列的宽度不会发生变化；
2. JTable.AUTO_RESIZE_NEXT_COLUMN:只调整下一列的宽度，其他列及表格的宽度不会发生改变；
3. JTable.AUTO_RESIZE_SUBSEQUENT_COLUMNS:平均调整当前列后面所有列的宽度，当前列的前面所有列及表格的宽度都不会发生变化，这是默认的调整方式
4. JTable.AUTO_RESIZE_LAST_COLUMN:只调整最后一列的宽度，其他列及表格的宽度不会发生变化；
5. JTable.AUTO_RESIZE_ALL_COLUMNS:平均调整表格中所有列的宽度，表格的宽度不会发生改变



如果需要精确控制每一列的宽度，则可通过 TableColumn 对象来实现 。 JTable 使用 TableColumn 来表示表格中的每一列， JTable 中表格列的所有属性，如最佳宽度、是否可调整宽度、最小和最大宽度等都保存在该 TableColumn 中 。 此外， TableColumn 还允许为该列指定特定的单元格绘制器和单元格编辑器(这些内容将在后面讲解) 。 TableColumn 具有如下方法 。

1.  setMaxWidth(int maxWidth): 设置该列的最大宽度 。 如果指定的 maxWidth 小于该列的最小宽度， 则 maxWidth 被设置成最小宽度 。    
2. setMinWidth(int minWidth): 设置该列的最小宽度 。
3. setPreferredWidth(int preferredWidth): 设置该列的最佳宽度 。
4. setResizable(boolean isResizable): 设置是否可以调整该列的 宽度 。
5. sizeWidthToFit(): 调整该列的宽度，以适合其标题单元格的 宽度 。



**JTable调整选择模式：**

1. 选则行：JTable默认的选择方式就是选择行，也可以调用setRowSelectionAllowed(boolean rowSelectionAllowed)来修改；
2. 选择列：调用 setColumnSelectionAllowed(boolean columnSelectionAllowed)方法，修改当前JTable的选择模式为列；
3. 选择单元格：setCellSelectionEnabled(boolean cellSelectionEnabled) ，修改当前JTable的选择模式为单元格；



**JTable调整表格选择状态：**

与 JList 、 JTree 类似的是， JTable 使用了 一个 ListSelectionModel 表示该表格的选择状态，程序可以 通过 ListSelectionModel 来控制 JTable 的选择模式 。 JTable 的选择模式有如下三种：

1. ListSelectionMode.MULTIPLE_INTERVAL_SELECTION:没有任何限制，可以选择表格中任何表格单元，这是默认的选择模式 。 通过 Shi负和 Ctrl 辅助键的帮助可以选择多个表格单元 。

2. ListSelectionMode.SINGLE_INTERVAL_SELECTION:选择单个连续区域，该选项可以选择多个表格单元，但多个表格单元之间必须是连续的 。 通过 Shift 辅助键的帮助来选择连续区域。

3. ListSelectionMode.SINGLE_SELECTION:只能选择单个表格单元 。  

     

**案例：**

​	通过JTable实现的宽度调整，选择模式调整，选择状态调整，实现下图效果：

​	![](G:/%E7%A0%94%E5%8F%91/GUI/%E6%96%87%E6%A1%A3/images/adjust1.png)

​	![](G:/%E7%A0%94%E5%8F%91/GUI/%E6%96%87%E6%A1%A3/images/adjust2.png)

​	![](G:/%E7%A0%94%E5%8F%91/GUI/%E6%96%87%E6%A1%A3/images/adjust3.png)

**演示代码：**

```java
import javax.swing.*;
import javax.swing.table.TableColumn;

public class AdjustingWidth {

    JFrame jf = new JFrame("调整表格宽度");

    JMenuBar menuBar = new JMenuBar();

    JMenu adjustModeMenu = new JMenu("调整方式");
    JMenu selectUnitMenu = new JMenu("选择单元");
    JMenu selectModeMenu = new JMenu("选择方式");

    //定义5个单选框按钮，用以控制表格的宽度调整方式
    JRadioButtonMenuItem[] adjustModeItem = new JRadioButtonMenuItem[5];

    //定义3个单选框按钮，用以控制表格的选择方式
    JRadioButtonMenuItem[] selectModeItem = new JRadioButtonMenuItem[3];

    //定义复选菜单项，控制选择单元
    JCheckBoxMenuItem rowsItem = new JCheckBoxMenuItem("选择行");
    JCheckBoxMenuItem columnItem = new JCheckBoxMenuItem("选择列");
    JCheckBoxMenuItem cellItem = new JCheckBoxMenuItem("选择单元格");

    //定义按钮组，实现单选
    ButtonGroup adjustBg = new ButtonGroup();
    ButtonGroup selectBg = new ButtonGroup();

    //定义一个int类型的数组，用于保存表格所有的宽度调整方式

    int[] adjustModes = {
            JTable.AUTO_RESIZE_OFF,
            JTable.AUTO_RESIZE_NEXT_COLUMN,
            JTable.AUTO_RESIZE_SUBSEQUENT_COLUMNS,
            JTable.AUTO_RESIZE_LAST_COLUMN,
            JTable.AUTO_RESIZE_ALL_COLUMNS
    };


    //定义一个int乐行数组，用于保存表格所有的选择方式
    int[] selectModes = {
            ListSelectionModel.MULTIPLE_INTERVAL_SELECTION,
            ListSelectionModel.SINGLE_INTERVAL_SELECTION,
            ListSelectionModel.SINGLE_SELECTION
    };

    //声明JTable
    JTable table;

    //定义一个二维数组，作为表格行数据
    Object[][] tableData = {

            new Object[]{"李清照",29,"女"},
            new Object[]{"苏格拉底",56,"男"},
            new Object[]{"李白",35,"男"},
            new Object[]{"弄玉",18,"女"},
            new Object[]{"虎头",2,"男"},

    };

    //定义一个一维数组，作为列标题
    Object[] columnTitle = {"姓名","年龄","性别"};


    public void init(){

        //创建JTable对象
        table  = new JTable(tableData,columnTitle);


        //-----------------为窗口安装设置表格调整方式的菜单--------------------
        adjustModeItem[0] = new JRadioButtonMenuItem("只调整表格");
        adjustModeItem[1] = new JRadioButtonMenuItem("只调整下一列");
        adjustModeItem[2] = new JRadioButtonMenuItem("平均调整余下列");
        adjustModeItem[3] = new JRadioButtonMenuItem("只调整最后一列");
        adjustModeItem[4] = new JRadioButtonMenuItem("平均调整所有列");

        menuBar.add(adjustModeMenu);

        for (int i = 0; i < adjustModeItem.length; i++) {
            //默认选中第三个菜单项，即对应表格默认的宽度调整方式
            if (i==2){
                adjustModeItem[i].setSelected(true);
            }
            adjustBg.add(adjustModeItem[i]);
            adjustModeMenu.add(adjustModeItem[i]);

            //为菜单项设置事件监听器
            int index = i;
            adjustModeItem[i].addActionListener(e -> {
                if (adjustModeItem[index].isSelected()){
                    table.setAutoResizeMode(adjustModes[index]);
                }
            });
        }

        //---------------为窗口安装设置表格选择方式的菜单-------------------
        selectModeItem[0] = new JRadioButtonMenuItem("无限制");
        selectModeItem[1] = new JRadioButtonMenuItem("单独的连续区");
        selectModeItem[2] = new JRadioButtonMenuItem("单选");

        menuBar.add(selectModeMenu);

        for (int i = 0; i < selectModeItem.length; i++) {

            //默认选中第一个菜单项，即表格的默认选择方式
            if (i==0){
                selectModeItem[i].setSelected(true);
            }

            selectBg.add(selectModeItem[i]);
            selectModeMenu.add(selectModeItem[i]);


            int index = i;

            selectModeItem[i].addActionListener(e -> {

                if (selectModeItem[index].isSelected()){
                    table.getSelectionModel().setSelectionMode(selectModes[index]);
                }

            });

        }

        //---------------为窗口添加选择单元菜单----------------------
        menuBar.add(selectUnitMenu);
        rowsItem.setSelected(table.getRowSelectionAllowed());
        columnItem.setSelected(table.getColumnSelectionAllowed());
        cellItem.setSelected(table.getCellSelectionEnabled());

        rowsItem.addActionListener(e -> {
            //清除表格的选中状态
            table.clearSelection();
            //如果该菜单项处于选中状态，设置表格的选择单元是行
            table.setRowSelectionAllowed(rowsItem.isSelected());
            //如果选择行、选择列同时被选中，其实质是选择单元格
            table.setCellSelectionEnabled(table.getCellSelectionEnabled());

        });

        selectUnitMenu.add(rowsItem);

        columnItem.addActionListener(e -> {
            //清除表格的选中状态
            table.clearSelection();

            //如果该菜单项处于选中状态，设置表格的选择单元是列
            table.setColumnSelectionAllowed(columnItem.isSelected());
            ///如果选择行、选择列同时被选中，其实质是选择单元格
            table.setCellSelectionEnabled(table.getCellSelectionEnabled());
        });

        selectUnitMenu.add(columnItem);

        cellItem.addActionListener(e -> {
            //清除表格的选中状态
            table.clearSelection();

            //如果该菜单项处于选中状态，设置表格的选择单元是单元格
            table.setCellSelectionEnabled(cellItem.isSelected());
            ///该选项的改变会同时影响选择行、选择列两个菜单
            table.setRowSelectionAllowed(table.getRowSelectionAllowed());
            table.setColumnSelectionAllowed(table.getColumnSelectionAllowed());

        });

        selectUnitMenu.add(cellItem);

        jf.setJMenuBar(menuBar);

        //分别获取表格的三个表格列，并设置三列的最小宽、最佳宽度和最大宽度
        TableColumn nameColumn = table.getColumn(columnTitle[0]);
        nameColumn.setMinWidth(40);
        TableColumn ageColumn = table.getColumn(columnTitle[1]);
        ageColumn.setPreferredWidth(50);
        TableColumn genderColumn = table.getColumn(columnTitle[2]);
        genderColumn.setMaxWidth(50);

        jf.add(new JScrollPane(table));
        jf.pack();
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.setVisible(true);

    }

    public static void main(String[] args) {
        new AdjustingWidth().init();
    }

}
```

### 3.7.2 TableModel和监听器

与 JList、 JTree 类似的是 ， JTable 采用了 TableModel 来保存表格中的所有状态数据 : 与 ListModel类似的是， TableModel 也不强制保存该表格显示的数据 。 虽然在前面程序中看到的是直接利用 一个二维数组来创建 JTable 对象，但也可以通过 TableModel 对象来创建表格。

**使用TableModel步骤：**

1. 自定义类，继承AbstractTableModel抽象类，重写下面几个方法：

```java
int getColumnCount():返回表格列的数量
int getRowCount()：返回表格行的数量
Object getValueAt(int rowIndex, int columnIndex)：返回rowIndex行，column列的单元格的值
String getColumnName(int columnIndex)：返回columnIndex列的列名称
boolean isCellEditable(int rowIndex, int columnIndex)：设置rowIndex行，columnIndex列单元格是否可编辑
setValueAt(Object aValue, int rowIndex, int columnIndex)：设置rowIndex行，columnIndex列单元格的值
```

1. 创建自定义类对象，根据该对象，创建JTable对象



**案例：**

​	

1. 连接数据库，把库中所有的表名称显示到下拉列表中
2. 点击下拉列表中某个表名时，查询数据库该表的数据，并把结果封装到TableModel中，使用JTable展示
3. 点击表格中某个单元格，修改数据，能实时修改数据库中的数据
4. 每修改一次数据，把修改的信息打印到下方的文本域中



​	![](G:/%E7%A0%94%E5%8F%91/GUI/%E6%96%87%E6%A1%A3/images/TableModel.png)

**演示代码：**

```java
import javax.swing.*;
import javax.swing.event.TableModelEvent;
import javax.swing.event.TableModelListener;
import javax.swing.table.AbstractTableModel;
import java.awt.*;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;
import java.sql.*;

public class TableModelTest {
    JFrame jf = new JFrame("数据表管理工具");

    JScrollPane scrollPane;
    ResultSetTableModel model;

    //用于装载数据表的JComboBox
    JComboBox<String> tableNames = new JComboBox<>();
    JTextArea changeMsg = new JTextArea(4, 80);

    ResultSet rs;

    Connection conn;
    Statement stmt;

    public void init() {
        //为JComboBox添加监听事件，当用户选择某个数据表时，触发该方法
        tableNames.addActionListener(e -> {

            try {
                //如果装载JTable的JScrollPane不为空
                if (scrollPane != null) {
                    //从主窗口中删除表格
                    jf.remove(scrollPane);
                }

                //从JComboBox中取出用户视图管理的数据表的表名
                String tableName = (String) tableNames.getSelectedItem();

                //如果结果集不为空，则关闭结果集
                if (rs != null) {
                    rs.close();
                }

                String query = "select * from " + tableName;
                //查询用户选择的数据表
                rs = stmt.executeQuery(query);
                //使用查询到的ResultSet创建TableModel对象
                model = new ResultSetTableModel(rs);

                //为TableModel添加监听器，监听用户的修改
                model.addTableModelListener(new TableModelListener() {
                    @Override
                    public void tableChanged(TableModelEvent e) {
                        int row = e.getFirstRow();
                        int column = e.getColumn();
                        changeMsg.append("修改的列：" + column + ",修改的行：" + row + ",修改后的值：" + model.getValueAt(row, column)+".\n");
                    }
                });

                //使用TableModel创建JTable
                JTable table = new JTable(model);

                scrollPane = new JScrollPane(table);
                jf.add(scrollPane);
                jf.validate();

            } catch (SQLException e1) {
                e1.printStackTrace();
            }

        });

        JPanel p = new JPanel();
        p.add(tableNames);
        jf.add(p, BorderLayout.NORTH);
        jf.add(new JScrollPane(changeMsg), BorderLayout.SOUTH);


        //--------------数据库相关操作--------------------
        try {
            //获取数据库连接
            conn = getConn();
            //获取数据库的metaData对象
            DatabaseMetaData metaData = conn.getMetaData();


            //游标可以上下移动，可以使用结果集更新数据库中的表
            stmt = conn.createStatement(ResultSet.TYPE_SCROLL_INSENSITIVE,ResultSet.CONCUR_UPDATABLE);


            //查询数据库中的全部表
            ResultSet tables = metaData.getTables(null, null, null, new String[]{"TABLE"});

            //将全部表添加到JCombox中
            while(tables.next()){
                tableNames.addItem(tables.getString(3));
            }
            tables.close();

        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        }

        //为JFrame添加窗口事件
        jf.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                if (conn!=null){
                    try {
                        conn.close();
                    } catch (SQLException e1) {

                    }
                }
            }
        });

        jf.pack();
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.setVisible(true);

    }

    public static void main(String[] args) {
        new TableModelTest().init();
    }


    public Connection getConn() throws ClassNotFoundException, SQLException {
        Class.forName("com.mysql.jdbc.Driver");

        return DriverManager.getConnection("jdbc:mysql://localhost:3306/test", "root", "root");
    }


    class ResultSetTableModel extends AbstractTableModel {


        private ResultSet rs;
        private ResultSetMetaData rsmd;

        //构造方法，初始化rs和rsmd两个属性
        public ResultSetTableModel(ResultSet aResultSet) {
            this.rs = aResultSet;
            try {
                rsmd = rs.getMetaData();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        //重写getColumnName方法，为表格设置列名
        @Override
        public String getColumnName(int column) {
            //column是表格列的标号，从0开始，而rsmd获取列时，标号从1开始，所以要column+1
            try {
                return rsmd.getColumnName(column + 1);
            } catch (SQLException e) {
                e.printStackTrace();
                return "";
            }
        }

        //重写getValueAt()方法，用于设置该表格指定单元格的值
        @Override
        public Object getValueAt(int rowIndex, int columnIndex) {

            try {
                //把游标移动到指定行,swing表格中行号从0开始，但是游标中行号从1开始，所以要修正
                rs.absolute(rowIndex+1);
                return rs.getObject(columnIndex + 1);
            } catch (SQLException e) {
                e.printStackTrace();
                return null;
            }

        }

        //重写getRowCount()方法，用于设置该TableModel的行数
        @Override
        public int getRowCount() {
            try {
                rs.last();
                return rs.getRow();
            } catch (SQLException e) {
                e.printStackTrace();
                return 0;
            }

        }

        //重写getColumnCount()方法，用于设置表格的列数
        @Override
        public int getColumnCount() {
            try {
                return rsmd.getColumnCount();
            } catch (SQLException e) {
                e.printStackTrace();
                return 0;
            }
        }

        //重写isEditable()方法，让每个单元格可编辑


        @Override
        public boolean isCellEditable(int rowIndex, int columnIndex) {
            return true;
        }

        //重写setValueAt()方法，当用户编辑单元格时，会触发该方法


        @Override
        public void setValueAt(Object aValue, int rowIndex, int columnIndex) {

            try {
                //把游标定位到对应的行数
                rs.absolute(rowIndex+1);
                //修改对应单元格的值
                rs.updateObject(columnIndex + 1, aValue);
                //提交修改
                rs.updateRow();
                //触发单元格的修改事件
                fireTableCellUpdated(rowIndex, columnIndex);

            } catch (SQLException e) {
                e.printStackTrace();
            }

        }
    }
}

```

​	不仅用户可以扩展 AbstractTableModel 抽象类， Swing 本身也为 AbstractTableModel 提供了 一个DefaultTableModel 实现类，程序可以通过使用 DefaultTableModel 实现类来创建 JTable 对象 。 通过DefaultTableModel 对象创建 JTable 对象后，就可以调用它提供的方法来添加数据行、插入数据行 、删除数据行和移动数据行 。 DefaultTableModel 提供了如下几个方法来控制数据行操作:

```
addColumn(Object columnName)/addColumn(Object columnName, Object[] columnData):添加一列
addRow(Object[] rowData)：添加一行
insertRow(int row, Object[] rowData)：指定位置处插入一行
removeRow(int row)：删除一行
moveRow(int start, int end, int to)：移动指定范围内的数据行
```



### 3.7.3 TableColumnModel和监听器

JTable 使用 TableColumnModel 来保存该表格所有数据列的状态数据，如果程序需要访问 JTable 的所有列状态信息，则可以通过获取该 JTable 的 TableColumnModel 来实现 。 TableColumnModel 提供了如下几个方法来增加、删除和移动数据列 ：

1. addColumn(TableColumn aColumn): 该方法用于为 TableModel 添加一列 。 该方法主要用于将原来隐藏的数据列显示出来 。
2. moveColumn(int columnIndex, int newIndex): 该方法用于将指定列移动到其他位置 。
3. removeColumn(TableColumn column): 该方法用于从 TableModel 中删 除指定列。实际上，该方法并未真正删除指定列，只是将该列在TableColumnModel 中隐藏起来，使之不可见 。

JTable中也提供了类似的方法完成列的操作，只是其底层依然是通过TableColumnModel来完成的。



**案例：**

​	使用DefaultTableModel和TableColumnModel完成下图效果：

​	![](G:/%E7%A0%94%E5%8F%91/GUI/%E6%96%87%E6%A1%A3/images/DefaultTableModel.png)

**演示代码：**

```java
import javax.swing.*;
import javax.swing.table.DefaultTableModel;
import javax.swing.table.TableColumn;
import javax.swing.table.TableColumnModel;
import java.awt.*;
import java.util.ArrayList;

public class DefaultTableModelTest {

    JFrame mainWin = new JFrame("管理数据行、数据列");

    final int COLUMN_COUNT = 5;

    DefaultTableModel model;

    JTable table;
    //用于保存被隐藏列的List集合
    ArrayList<TableColumn> hiddenColumns = new ArrayList<>();

    public void init(){

        //创建DefaultTableModel，5行5列
        model = new DefaultTableModel(COLUMN_COUNT,COLUMN_COUNT);

        //给每个单元格设置内容
        for (int i = 0; i < COLUMN_COUNT; i++) {
            for (int j = 0; j < COLUMN_COUNT; j++) {
                model.setValueAt("老单元格值"+i+" "+j,i,j);

            }
        }

        //创建表格
        table = new JTable(model);
        mainWin.add(new JScrollPane(table), BorderLayout.CENTER);

        //为窗口安装菜单
        JMenuBar menuBar = new JMenuBar();
        mainWin.setJMenuBar(menuBar);
        JMenu tableMenu = new JMenu("管理");
        menuBar.add(tableMenu);

        JMenuItem hideColumnsItem = new JMenuItem("隐藏选中列");
        hideColumnsItem.addActionListener(e -> {
            //获取所有选中列的索引
            int[] selectedColumns = table.getSelectedColumns();
            TableColumnModel columnModel = table.getColumnModel();
            //依次把每个选中的列隐藏起来，并使用hideColumns集合把隐藏的列保存起来

            for (int i = 0; i < selectedColumns.length; i++) {
                //获取列对象TableColumn
                TableColumn column = columnModel.getColumn(selectedColumns[i]);
                //隐藏指定列
                table.removeColumn(column);

                //把隐藏的列保存起来，确保以后可以显示出来
                hiddenColumns.add(column);
            }
        });

        tableMenu.add(hideColumnsItem);

        JMenuItem showColumsItem = new JMenuItem("显示隐藏列");
        showColumsItem.addActionListener(e -> {

            for (TableColumn column : hiddenColumns) {
                table.addColumn(column);
            }

            //清空隐藏列集合
            hiddenColumns.clear();

        });

        tableMenu.add(showColumsItem);

        JMenuItem addColumnItem = new JMenuItem("插入选中列");
        addColumnItem.addActionListener(e -> {
            //获取所有选中列的索引
            int[] selectedColumns = table.getSelectedColumns();
            TableColumnModel columnModel = table.getColumnModel();
            //依次插入选中列
            for (int i = selectedColumns.length-1; i >=0; i--) {
                TableColumn column = columnModel.getColumn(selectedColumns[i]);
                table.addColumn(column);

            }
        });

        tableMenu.add(addColumnItem);


        JMenuItem addRowItem = new JMenuItem("增加行");
        addRowItem.addActionListener(e -> {
            //创建一个String数组，作为新增行的内容
            String[] newCells = new String[COLUMN_COUNT];
            for (int i = 0; i < newCells.length; i++) {
                newCells[i] = "新单元格的值"+model.getRowCount()+" "+i;
            }

            //向table中新增一行
            model.addRow(newCells);
        });

        tableMenu.add(addRowItem);

        JMenuItem removeRowsItem = new JMenuItem("删除选中行");

        removeRowsItem.addActionListener(e -> {
            //获取被选中的行
            int[] selectedRows = table.getSelectedRows();

            //依次删除每一行
            for (int i = selectedRows.length-1; i >=0; i--) {
                model.removeRow(selectedRows[i]);
            }

        });

        tableMenu.add(removeRowsItem);

        mainWin.pack();
        mainWin.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        mainWin.setVisible(true);

    }


    public static void main(String[] args) {
        new DefaultTableModelTest().init();
    }

}
```

如果程序需要监昕 JTable 里列状态的改变，例如监听列的增加、删除 、 移动等改变， 则必须使用该 JTable 所对应的 TableColumnModel 对象，该对象提供了 一个 addColumnModelListener()方法来添加监听器， 该监听器接口里包含如下几个方法 ：

1. columnAdded(TableColumnModelEvent e) : 当向 TableColumnModel 里添加数据列时将会触发该方法。
2.  columnMarginChanged(ChangeEvent e) : 当由于页面距 ( Margin ) 的改变引起列状态改变时将会触发该方法 。
3.  columnMoved(TableColumnModelEvent e): 当移动 TableColumnModel 里的数据列时将会触发该方法 。
4.  columnRemoved(TableColumnModelEvent e): 当删除 TableColumnModel 里的数据列时将会触发该方法 。
5.  columnSelectionChanged(ListSelectionEvent e): 当改变表格的选择模式时将会触发该方法。

但表格的数据列通常需要程序来控制增加、 删除 ，用户操作通常无法直接为表格增加 、删除数据列，所以使用监听器来监听 TableColumnModel 改变的情况比较少见。



### 3.7.4 实现列排序

使用 JTable 实现的表格并没有实现根据指定列排序的功能 ， 但开发者可以利用 AbstractTableModel 类来实现该功能。由于 TableModel 不强制要求保存表格里的数据，只要 TableModel 实现了 getValueAt()、getColumnCount()和 getRowCount()三个方法， JTable 就可以根据该 TableModel 生成表格 。 因此可以创建个 SortableTableModel 实现类 ， 它可以将原 TableModel 包装起来，并实现根据指定列排序的功能 。

程序创建的 SortableTableModel 实现类会对原 TableModel 进行包装，但它实际上并不保存任何数据，它会把所有的方法实现委托给原 TableModel 完成。 SortableTableModel 仅保存原 TableModel 里每行的行索引， 当程序对 SortableTableModel 的指定列排序时， 实际上仅仅对SortableTableModel 里的行索引进排序一一这样造成的结果是 : SortableTableModel 里的数据行的行索引与原 TableModel 里数据行的行索引不一致，所以对于 TableModel 的那些涉及行索引的方法都需要进行相应的转换。下面程序实现了SortableTableModel 类，并使用该类来实现对表格根据指定列排序的功能 。



**案例：**

​	实现下图功能：

​		双击列的头部，按照该列从小到大的顺序进行排序

​	![](G:/%E7%A0%94%E5%8F%91/GUI/%E6%96%87%E6%A1%A3/images/sorttable.png)

**演示代码：**

```java
import javax.swing.*;
import javax.swing.table.AbstractTableModel;
import javax.swing.table.TableModel;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;
import java.util.Arrays;

public class SortTable {

    JFrame jf = new JFrame("可按照列排序的表格");

    //定义二维数组作为表格数据

    Object[][] tableData = {

            new Object[]{"李清照",29,"女"},
            new Object[]{"苏格拉底",56,"男"},
            new Object[]{"李白",35,"男"},
            new Object[]{"弄玉",18,"女"},
            new Object[]{"虎头",2,"男"},

    };

    //定义一个一维数组，作为列标题
    Object[] columnTitle = {"姓名","年龄","性别"};

    JTable table = new JTable(tableData,columnTitle);

    //将原表格里面的TableModel封装成SortTableModel对象
    SortTableModel sorterModel = new SortTableModel(table.getModel());

    public void init(){
        //使用包装后的SortTableModel对象作为JTable的model对象
        table.setModel(sorterModel);

        //为每一列的列头增加鼠标监听器
        table.getTableHeader().addMouseListener(new MouseAdapter() {
            @Override
            public void mouseClicked(MouseEvent e) {
                //如果单击次数小于2，则返回，不是双击
                if (e.getClickCount()<2){
                    return;
                }

                //找出鼠标双击事件所在列的索引
                int tableColumn = table.columnAtPoint(e.getPoint());

                //将JTable中的列索引，转换成对应的TableModel中的列索引
                int modelColumn = table.convertColumnIndexToModel(tableColumn);

                //根据指定列进行排序
                sorterModel.sort(modelColumn);
            }
        });

        jf.add(new JScrollPane(table));
        jf.pack();
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.setVisible(true);
    }


    public static void main(String[] args) {
        new SortTable().init();
    }


    //自定义SortTableModel，增强原有的TableModel

    class SortTableModel extends AbstractTableModel{

        private TableModel model;
        private int sortColumn;
        private Row[] rows;

        public SortTableModel(TableModel model){
            this.model = model;
            rows = new Row[model.getRowCount()];
            //将原TableModel中的每行记录的索引用Row数组保存起来
            for (int i = 0; i < rows.length; i++) {
                rows[i] = new Row(i);
            }

        }

        //实现根据指定列进行排序
        public void sort(int c){
            sortColumn = c;
            Arrays.sort(rows);
            //触发数据改变的事件
            fireTableDataChanged();
        }

        //下面3个方法需要访问model中的数据，所以涉及本model中数据和被封装model数据中的索引转换，程序使用rows完成这种转换

        @Override
        public Object getValueAt(int rowIndex, int columnIndex) {
            return model.getValueAt(rows[rowIndex].index,columnIndex);
        }

        @Override
        public boolean isCellEditable(int rowIndex, int columnIndex) {
            return isCellEditable(rows[rowIndex].index,columnIndex);
        }

        @Override
        public void setValueAt(Object aValue, int rowIndex, int columnIndex) {
            model.setValueAt(aValue,rows[rowIndex].index,columnIndex);
        }

        //下面方法的实现把该model的方法委托给原封装的model来实现


        @Override
        public int getRowCount() {

            return model.getRowCount();
        }

        @Override
        public int getColumnCount() {
            return model.getColumnCount();
        }


        @Override
        public String getColumnName(int column) {
            return model.getColumnName(column);
        }

        @Override
        public Class<?> getColumnClass(int columnIndex) {
            return model.getColumnClass(columnIndex);
        }

        private class Row implements Comparable<Row>{
            //该index保存着被封装Model里每行记录的索引
            public int index;

            public Row(int index) {
                this.index = index;
            }

            //实现两行之间大小的比较
            @Override
            public int compareTo(Row o) {
                Object a = model.getValueAt(index, sortColumn);
                Object b = model.getValueAt(o.index, sortColumn);

                if (a instanceof Comparable){
                    return ((Comparable) a).compareTo(b);
                }else{
                    return a.toString().compareTo(b.toString());
                }
            }
        }
    }

}
```

### 3.7.5 绘制单元格内容

前面看到的所有表格的单元格内容都是宇符串，实际上表格的单元格内容也可以是更复杂的内容。JTable 使用 TableCellRenderer 绘制单元格， Swing 为该接口提供了 一 个实现类 : DefaultTableCellRenderer,该单元格绘制器可以绘制如下三种类型的单元格值(根据其 TableModel 的 getColurnnClass()方法来决定该单元格值的类型) :

1. Icon: 默认的单元格绘制器会把该类型的单元格值绘制成该Icon对象所代表的图标 。
2. Boolean: 默认的单元格绘制器会把该类型的单元格值绘制成复选按钮。
3. Object: 默认的单元格绘制器在单元格内绘制出该对象的 toString()方法返回的字符串 。

在默认情况下，如果程序直接使用 二维数组或 Vector 来创建 JTable ， 程序将会使用 JTable 的匿名内部类或 DefaultTableModel 充当该表格的 model 对象，这两个 TableModel 的 getColumnClass()方法的返回值都是 Object 。 这意味着，即使该二维数组里值的类型是 Icon ， 但由于两个默认的 TableModel 实现类的 getColumnClass()方法总是返回 Object，这将导致默认的单元格绘制器把 Icon 值当成 Object 值处
理一一只是绘制出其 toString()方法返回的字符串。

​	为了让默认的单元格绘制器可以将 Icon 类型 的值绘制成图标，把 Boolean 类型的值绘制成复边框 ，创建 JTable 时所使用的 TableModel 绝不能采用默认的 TableModel ，必须采用扩展后的 TableModel 类，如下所示 :

```java
//定义一个DefaultTableModel的子类
class ExtendedTableModel extends DefaultTableModel{
    ...
    //重写getColumnClass方法，根据每列的第一个值，来返回每列的真实数据类型
        public class getColumnClass(int c){
            return getValueAt(0,c).getClass();
        }
        
    ...
    
}
```

​	提供了上面的 ExtendedTableModel 类之后 ， 程序应该先创建 ExtendedTableModel 对象，再利用该对象来创建 JTable，这样就可以保证 JTable 的 model 对象的 getColumnClass()方法会返回每列真实的数据类型，默认的单元格绘制器就会将 Icon 类型的单元格值绘制成图标 ， 将 Boolean 类型 的单元格值绘制成复选框。

​	如果希望程序采用自己定制的单元格绘制器，则必须实现自己的单元格绘制器，单元格绘制器必须实现 TableCellRenderer 接口。与前面的TreeCellRenderer 接口完全相似， 该接口里也只包含一 个getTableCellRendererComponent()方法，该该方法返回的 Component 将会作为指定单元格绘制的组件。

​	一旦实现了自己的单元格绘制器之后，还必须将该单元格绘制器安装到指定的 JTable 对象上，为指定的 JTable 对象安装单元格绘制器有如下两种方式 ：

1. 局部方式 ( 列级 ) : 调用 TableColumn的setCellRenderer()方法为指定列安装指定的单元格绘制器。    
2. 全局方式 (表级) :调用 JTable 的setDefaultRendererO方法为指定的 JTable 对象安装单元格绘制器, setDefaultRendererO方法需要传入两个参数,即列类型和单元格绘制器 ， 表明指定类型的数据列才会使用该单元格绘制器 。



**案例：**

​	使用TableCellRenderer和TableModel实现下图效果：

​	![](G:/%E7%A0%94%E5%8F%91/GUI/%E6%96%87%E6%A1%A3/images/TableCellRenderer.png)

**演示代码：**

```java
import cn.itcast.swing.util.ImagePathUtil;

import javax.swing.*;
import javax.swing.table.DefaultTableModel;
import javax.swing.table.TableCellRenderer;
import javax.swing.table.TableColumn;
import java.awt.*;

public class TableCellRendererTest {

    JFrame jf = new JFrame("使用单元格绘制器");

    JTable table;

    //定义二维数组作为表格数据

    Object[][] tableData = {

            new Object[]{"李清照",29,"女",new ImageIcon(ImagePathUtil.getRealPath("11\\3.gif")),true},
            new Object[]{"苏格拉底",56,"男",new ImageIcon(ImagePathUtil.getRealPath("11\\1.gif")),false},
            new Object[]{"李白",35,"男",new ImageIcon(ImagePathUtil.getRealPath("11\\4.gif")),true},
            new Object[]{"弄玉",18,"女",new ImageIcon(ImagePathUtil.getRealPath("11\\2.gif")),true},
            new Object[]{"虎头",2,"男",new ImageIcon(ImagePathUtil.getRealPath("11\\5.gif")),false},

    };

    //定义一个一维数组，作为列标题
    String[] columnTitle = {"姓名","年龄","性别","主头像","是否中国人"};

    public void init(){
        //以二维数组和一维数组来创建一个ExtendedTableModel对象
        ExtendedTableModel model = new ExtendedTableModel(columnTitle,tableData);

        //创建JTable
        table = new JTable(model);

        table.setRowSelectionAllowed(false);
        table.setRowHeight(40);

        //获取第三列
        TableColumn column = table.getColumnModel().getColumn(2);
        //对第三列采用自定义的单元格绘制器
        column.setCellRenderer(new GenderTableCellRenderer());

        jf.add(new JScrollPane(table));
        jf.pack();
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.setVisible(true);
    }

    public static void main(String[] args) {
        new TableCellRendererTest().init();
    }

    //自定义ExtendedTableModel对象
    class ExtendedTableModel extends DefaultTableModel{

        //重新提供一个构造器，该构造器的实现委托给DefaultTableModel父类
        public  ExtendedTableModel(String[] columnNames,Object[][] cells){
            super(cells,columnNames);
        }

        //重写getColumnClass方法，根据每列第一个值，返回其真实的数据类型

        @Override
        public Class<?> getColumnClass(int columnIndex) {
            return getValueAt(0,columnIndex).getClass();
        }
    }

    //自定义的单元格绘制器
    class GenderTableCellRenderer extends JPanel implements TableCellRenderer {
        private String cellValue;
        //定义图标的宽度和高度
        final int ICON_WIDTH = 23;
        final int ICON_HEIGHT = 21;


        @Override
        public Component getTableCellRendererComponent(JTable table, Object value, boolean isSelected, boolean hasFocus, int row, int column) {
            cellValue = (String) value;

            //设置选中状态的绘制边框
            if (hasFocus){
                setBorder(UIManager.getBorder("Table.focusCellHighlightBorder"));
            }else{
                setBorder(null);
            }
            return this;
        }

        //重写paint方法，负责绘制单元格的内容
        @Override
        public void paint(Graphics g) {
            //如果表格的内容为男或male,则绘制一个男性图标
            if (cellValue.equals("男") || cellValue.equals("male")){
                drawImage(g,new ImageIcon(ImagePathUtil.getRealPath("11\\male.gif")).getImage());
            }

            //如果表格的内容为nv或female，则绘制一个女性图标
            if (cellValue.equals("女") || cellValue.equals("female")){
                drawImage(g,new ImageIcon(ImagePathUtil.getRealPath("11\\female.gif")).getImage());
            }
        }

        private void drawImage(Graphics g,Image image){
            g.drawImage(image,(getWidth()-ICON_WIDTH)/2,(getHeight()-ICON_HEIGHT)/2,null);
        }
    }
}
```

### 3.7.6 编辑单元格内容

如果用户双击 JTable 表格的指定单元格，系统将会开始编辑该单元格的内容。在默认情况下，系统会使用文本框来编辑该单元格的内容，与此类似的是 ，如果用户双击 JTree 的节 点，默认也会采用文本框来编辑节点 的内容 。

但如果单元格内容不是文字内容，用户当然不希望使用文本编辑器来编辑该单元格的内容，因为这种编辑方式非常不直观，用户体验相当差 。 为了避免这种情况，可以实现自己的单元格编辑器，从而可以给用户提供更好的操作界面。

实现 JTable 的单元格编辑器应该实现 TableCellEditor 接口 ，Swing 为 TableCellEditor提供了 DefaultCellEditor 实现类，efaultCellEditor 类有三
个构造器， 它们分别使用文本框、复选框和JComboBox 作 为单元格编辑器，其中使用文本框编辑器是最常见的情形，如果单元格的值是 Boolean
类型 ，则系统默认使用复选框编辑器。如果想指定某列使用 JComboBox 作为单元格编辑器，则需要显式创建 JComboBox 实例 ，然后以此实例来创建 DefaultCellEditor 编辑器 。

**使用DefaultCellEditor步骤：**

1. 自定义类，继承DefaultCellEditor，重写getTableCellEditorComponent()方法；
2. 创建自定义类对象
3. 为JTable安装单元格编辑器

```java
局部安装：通过TableColumn的setEditor（）方法完成安装，只是为某一列安装。
全局安装：调用 JTable 的 setDefaultEditor（）方法为该表格安装默认的单元格编辑器。该方法需要两个参数，即列类型和单元格编辑器，这两个参数表明对于指定类型的数据列使用该单元格编辑器 。

```



**案例：**

​	使用TableCellEditor和TableModel完成下图效果：

​	![](G:/%E7%A0%94%E5%8F%91/GUI/%E6%96%87%E6%A1%A3/images/TableCellEditor1.png)

​	![](G:/%E7%A0%94%E5%8F%91/GUI/%E6%96%87%E6%A1%A3/images/TableCellEditor2.png)

**演示代码：**

```java
import cn.itcast.swing.util.ImagePathUtil;

import javax.swing.*;
import javax.swing.filechooser.FileFilter;
import javax.swing.table.DefaultTableModel;
import javax.swing.table.TableColumn;
import java.awt.*;
import java.io.File;

public class TableCellEditorTest {
    JFrame jf = new JFrame("使用单元格编辑器");

    JTable table;

    //定义二维数组作为表格数据

    Object[][] tableData = {

            new Object[]{"李清照",29,"女",new ImageIcon(ImagePathUtil.getRealPath("11\\3.gif")),new ImageIcon(ImagePathUtil.getRealPath("11\\3.gif")),true},
            new Object[]{"苏格拉底",56,"男",new ImageIcon(ImagePathUtil.getRealPath("11\\1.gif")),new ImageIcon(ImagePathUtil.getRealPath("11\\1.gif")),false},
            new Object[]{"李白",35,"男",new ImageIcon(ImagePathUtil.getRealPath("11\\4.gif")),new ImageIcon(ImagePathUtil.getRealPath("11\\4.gif")),true},
            new Object[]{"弄玉",18,"女",new ImageIcon(ImagePathUtil.getRealPath("11\\2.gif")),new ImageIcon(ImagePathUtil.getRealPath("11\\2.gif")),true},
            new Object[]{"虎头",2,"男",new ImageIcon(ImagePathUtil.getRealPath("11\\5.gif")),new ImageIcon(ImagePathUtil.getRealPath("11\\5.gif")),false},

    };

    //定义一个一维数组，作为列标题
    String[] columnTitle = {"姓名","年龄","性别","主头像","次头像","是否中国人"};


    public void init(){
        ExtendedTableModel model = new ExtendedTableModel(columnTitle,tableData);

        table  =  new JTable(model);

        table.setRowSelectionAllowed(false);
        table.setRowHeight(40);

        //为表格指定默认的编辑器
        table.setDefaultEditor(ImageIcon.class,new ImageCellEditor());

        //获取第5列
        TableColumn column = table.getColumnModel().getColumn(4);
        //创建JComboBox对象，并添加多个图标列表项
        JComboBox<ImageIcon> editCombo = new JComboBox<>();
        for (int i = 1; i <= 10; i++) {
            editCombo.addItem(new ImageIcon(ImagePathUtil.getRealPath("11\\"+i+".gif")));
        }

        //设置第5列使用基于JComboBox的DefaultCellEditor
        column.setCellEditor(new DefaultCellEditor(editCombo));

        jf.add(new JScrollPane(table));
        jf.pack();
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.setVisible(true);
    }


    public static void main(String[] args) {
        new TableCellEditorTest().init();
    }


    //自定义ExtendedTableModel对象
    class ExtendedTableModel extends DefaultTableModel {

        //重新提供一个构造器，该构造器的实现委托给DefaultTableModel父类
        public  ExtendedTableModel(String[] columnNames,Object[][] cells){
            super(cells,columnNames);
        }

        //重写getColumnClass方法，根据每列第一个值，返回其真实的数据类型

        @Override
        public Class<?> getColumnClass(int columnIndex) {
            return getValueAt(0,columnIndex).getClass();
        }
    }

    //扩展DefaultCellEditor来实现TableCellEditor
    class ImageCellEditor extends DefaultCellEditor{

        //定义文件选择器
        private JFileChooser fDialog = new JFileChooser();
        //定义文本域
        private JTextField field = new JPasswordField(15);
        //定义按钮
        private JButton button = new JButton("...");


        public ImageCellEditor() {
            //因为DefaultCellEditor没有无参构造器
            //所以这里显示调用父类有参数的构造器
            super(new JTextField());
            initEditor();
        }

        private void initEditor() {
            //禁止编辑
            field.setEnabled(false);
            //为按钮添加监听器，当用户单击按钮时，
            //系统将出现一个文件选择器让用户选择图标文件
            button.addActionListener(e->{
                fDialog.setCurrentDirectory(new File(ImagePathUtil.getRealPath("11")));
                int result = fDialog.showOpenDialog(null);

                if (result==JFileChooser.CANCEL_OPTION){
                    //用户点击了取消
                    super.cancelCellEditing();
                    return;
                }else{
                    //用户点击了确定按钮
                    field.setText(ImagePathUtil.getRealPath("11\\"+fDialog.getSelectedFile().getName()));
                    button.getParent().transferFocus();
                }
            });

            //为文件选择器安装文件过滤器
            fDialog.addChoosableFileFilter(new FileFilter() {
                @Override
                public boolean accept(File f) {
                    if (f.isDirectory()){
                        return true;
                    }

                    String extension = Utils.getExtension(f);
                    if (extension!=null){
                        if (extension.equals(Utils.tiff)
                            || extension.equals(Utils.tif)
                            || extension.equals(Utils.gif)
                            || extension.equals(Utils.jpeg)
                            || extension.equals(Utils.jpg)
                            || extension.equals(Utils.png)

                        ){
                            return true;
                        }else {
                            return false;
                        }
                    }

                    return false;
                }

                @Override
                public String getDescription() {
                    return "有效的图片文件";
                }
            });

            fDialog.setAcceptAllFileFilterUsed(false);
        }

        //重写getTableCellEditorComponent方法，绘制单元格组件


        @Override
        public Component getTableCellEditorComponent(JTable table, Object value, boolean isSelected, int row, int column) {
            this.button.setPreferredSize(new Dimension(20,20));
            JPanel panel = new JPanel();
            panel.setLayout(new BorderLayout());
            field.setText(value.toString());
            panel.add(this.field,BorderLayout.CENTER);
            panel.add(this.button,BorderLayout.EAST);

            return panel;
        }

        //重写getCellEditorValue方法，填充单元格的内容
        @Override
        public Object getCellEditorValue() {
            return new ImageIcon(field.getText());
        }


    }

}
class Utils{
    public final static String jpeg = "jpeg";
    public final static String jpg = "jpg";
    public final static String gif = "gif";
    public final static String tiff = "tiff";
    public final static String tif = "tif";
    public final static String png = "png";

    public static String getExtension(File f){
        String ext = null;
        String s = f.getName();
        int i = s.lastIndexOf('.');
        if (i>0 && i<s.length()-1){
            ext=s.substring(i+1).toLowerCase();
        }
        return ext;
    }
}
```

# 四. 综合案例

## 4.1 项目概述

## 4.2 环境搭建

## 4.3 项目开发

## 4.4 项目打包











