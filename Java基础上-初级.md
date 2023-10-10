																																		## 计算机相关基础知识
### 人机交互-图形化界面与命令行

图形化界面的缺点：
1.消耗内存
2.运行速度慢

windows-cmd：以·命令行的形式操作计算机
打开cmd:win+R 输出cmd回车

### 常见cmd命令（win下）
按tab键可以关联
1.盘符名称+冒号
盘符切换，如：E:回车，表示切换到E盘
2.dir
查看当前路径下的内容(包括隐藏目录)
3.cd +目录
进入目录
cd .. 返回上一目录
4.cd \\目录1\\目录2\\..
进入多级目录
5.cd \\
返回到盘符目录
6.cls
清屏
7.exit
推出cmd
### 环境变量
在正常情况下去打开D盘下面qq/Bin/QQ.exe
win+R cmd之后我们需要执行
```
D:
cd qq\Bin
qq.exe
```
三步，这比较麻烦
如何在不使用图形化界面的情况下去简化步骤让我们在任意的目录下下去打开QQ呢？
-只要把QQ的路径记录在电脑的某个地方，在当前目录下没有我们的QQ的时候去这个地方找就行了
这个地方就是**环境变量**

把QQ的路径记录到环境变量中（win下）：
win+E打开此电脑，右键-属性-高级系统设置-高级-环境变量，找到系统变量里面的Path，编辑-新建，将QQ.exe的路径添加，确定后保存，此时在任意目录下输入QQ.exe就可以打开QQ。

我们想要在任意的目录下打开指定的文件，就可以把软件的的路径添加到环境变量中。


### 计算机的存储规则

计算机中常见的数据：text文本数据 image图片数据 sound声音数据
文本数据又包括数据 字母 汉字等等

**在计算机中，任意数据都是以二进制形式来存储的**

不同进制在Java代码中的表现形式:二进制以0b开头，十进制不加前缀正常表示，八进制以0开头，十六进制以0x开头。（JDK7开始）

ASCII码表
GB2312编码
BIG5编码
GBK编码
Unicode编码

图片数据可分为黑白图 灰度图 彩色图
分辨率
像素
三原色
黑白图：白1黑0
灰度图：用0~255表示灰度数据
彩色图：红绿蓝RGB（光学三原色）三个0~255表示光学三原色，形成各种色彩，（0,0,0）为黑 （255,255,255）为白

声音数据：采样

原码、反码、补码

## java知识
### 1.Java基础

#### Java是什么？
Java是一门计算机语言
而且比较火，如图：
![[截图 2023-08-24 15-15-14.png]]


下载JDK后安装
JDK安装目录中：
bin:该路径下存放了各种工具命令。其中比较重要的有javac和java
conf:存放相关配置文件
include:该路径下存放了一些平台特定头文件
jmods:该路径下存放了各种模块
legal:存放各模块的授权文档
lib:存放工具的一些补充JAR包

bin文件下面最重要，其他稍作了解即可。
java自动配置了部分环境变量，如果想用其他的，可以配置bin文件夹到环境变量。更好的配置方式是新建一个系统变量JAVA_HOME，变量值不带bin，添加\%JAVA_HOME\%\\bin
 
#### 第一个java程序
HelloWorld.java:
```
public class HelloWorld{
		public static void main(String[] args){
				System.out.println("HelloWorld");
		}
}
```

编写程序->编译->运行
javac编译，java运行
在HelloWorld.java目录下
```
javac HelloWorld.java
```
生成HelloWorld.class
```
java HelloWorld
```
运行代码

#### java可以做什么呢
-Java SE
桌面应用开发，不合适，练习用，打基础
-Java ME
用于嵌入式电子设备或小型移动设备（凉了）
-Java EE
Web方向网站开发，这个领域厉害
浏览器+服务器

#### java为什么这么火
用户量大、适用面广、更新速度快、自身特点好（面向对象 安全性 多线程 简单易用 开源 跨平台）

跨平台：可以在不同操作系统下运行，windows liunx mac
Java跨平台原因：
高级语言编译运行方式有：**编译型**、**解释型**、**混合型**（半编译半解释）

**编译型**例子：C语言
根据C源代码和不同的操作系统整体翻译为二进制再交给机器运行
.c->.obj->运行 
不同的操作系统要重新编译

**解释型**例子：python
根据源代码读一行解释一行，按行翻译
不会产生新的文件，直接根据源代码逐行解释，再给设备运行

Java：**混合型**
存在编译，也存在解释
先整体编译出一个.class文件（字节码文件），再按行交给设备运行，而且不是直接运行在系统中，而是运行在**虚拟机**中，虚拟机是java提供好的，只需根据不同的操作系统安装不用虚拟机即可。
JVM(Java Virtual Machine):Java虚拟机，真正运行Java的地方
Windows JVM
Linux JVM
Mac JVM

#### JRE和JDK
运行java需要的环境：JVM 核心类库 开发工具（javac编译、java运行、jdb调试、jhat内存分析等等）  

**JDK**(Java Decelopment kit Java开发工具包)：JVM、核心类库
开发工具

当只需要运行代码时（.class文件），只需要JVM、核心类库和运行工具（java等，javac这些就不需要了）

**JRE**(Java Runtime Environment Java运行环境)：JVM、核心类库、运行工具

JDK包括JRE，JRE包括JVM

#### Java基础语法
-**注释**
单行注释—— //  
多行注释—— /*   \*/
文档注释（了解）—— /**   \*/

**注意：注释不参与编译，也不参与运行** ，多行注释不要嵌套**

-关键字
关键字：被Java赋予了特定含义的单词
特点：字母小写，在常见编辑器中有语法高亮

关键字：**class**
class:用于创建或定义一个类，类是Java的最基本的组成单元

-字面量
字面量类型：整数类型(-1 666)、小数类型(3.14)、字符类型(单引号，内容有且只有一个 'A' '0')、字符串类型(双引号，可空 "HelloWorld")、布尔类型(true false)、空类型(null)

```
public class value_test{  
    public static void main(String[] args){  
        System.out.println(666);  
        System.out.println(-1);  
  
        System.out.println(3.14);  
        System.out.println(-2.71);  
  
        System.out.println("Hello World!");  
        System.out.println('A');  
  
        System.out.println(true);  
        System.out.println(false);  
        //System.out.println(null);  null不能直接打印  
    }  
}
```

特殊字符： \\t \\r \\n ...
\\t：制表符   将前面的字符串补齐到8或8的倍数。补1～8个空格
(IDEA中:将前面的字符串补齐到4或4的倍数。补1～4个空格)
```
System.out.println("name"+'\t'+"age");  
System.out.println("Kevin"+'\t'+"20");
```

-变量
变量：在程序执行过程中，其值可能发生改变的量
定义变量的格式：
数据类型 变量名 = 数据值;

```
public class Variable{  
    public static void main(String[] args){  
        int a = 10;  
        int b = 20;  
        System.out.println(a);  
        System.out.println(a + b);  
        a = 15;  
        System.out.println(a);  
    }  
}
```

变量在使用前需要赋值



#### Java数据类型

![[截图 2023-08-25 00-03-24.png]]
要定义long类型变量时，最后需要加一个L或l作为后缀
要定义float类型变量时，最后需要加一个F或f作为后缀
其他不需要
double>float>long>int>short>byte

标识符：给类、方法、变量等起的名字
命名规则：由数字、字母、下划线、美元符组成
                 不能数字开头
                 不能是关键字
                 区分大小写

#### 键盘录入-Scanner类
导包->创建对象->接收数据
```
import java.util.Scanner;  //导包
  
public class Scannertest {  
    public static  void main(String[] args){  
        Scanner sc = new Scanner(System.in);  //创建对象
        int i = sc.nextInt();  //接收数据
        System.out.println(i);  
    }  
}
```

小练习：输入两个整数，输出相加结果
```
import java.util.Scanner;  
  
public class add {  
    public static void main(String[] args){  
        Scanner sc = new Scanner(System.in);  
        System.out.println("请输入第一个整数:");  
        int number1 = sc.nextInt();  
        System.out.println("请输入第二个整数:");  
        int number2 = sc.nextInt();  
        System.out.println(number1 + number2);  
    }  
}
```


键盘录入：
遇到**空格、制表符、回车**就停止接受，后面的数据就不接受了
接受整数：nextInt();
接受小数：nextDouble();
接受字符串：next();

遇到**回车**才停止接受，可以接受空格、制表符
接受字符串：nextLine();

这两套最好不要混用，有弊端：例如先用nextInt，再用nextLine会导致下面的nextLine接受不到数据（原因：nextInt的回车键在内存中直接被nextLine用了）
#### IDEA
全称IntelliJ IDEA，是用于java语言开发的集成环境
https://www.jetbrains.com/idea/

IDEA项目结构介绍
-project(项目)
	-module(模块)
		-package(包)
			-class(类)
			

psvm可以直接快捷生成程序主入口
sout直接生成输出语句
输入Scanner回车会自动import
真方便😋
Editor-General-Code Completion关闭Match case提示忽略大小写

在IDEA中，可以自动快速生成数组的遍历方式
数组名.fori
回车即可

.fori  正着遍历
.forr 倒着遍历

IDEA中ctrl+alt+L格式化代码

ctrl+alt+M自动抽取方法

ctrl + alt + V写了右边自动生成左边

按住鼠标滚轮（或者按住Alt键）向下拖动可以选中列

Alt + insert(或Alt + Fn + insert)选择不同的选项方便构造标准JavaBean类
或者使用插件PTG，右键后ptg to JavaBean快速生成便准JavaBean类

光标放在想调用的方法的括号中，ctrl + P查看方法中所需要的参数

选中代码区域后ctrl + Alt + T可以选择用什么语句包裹（linux会跳终端。。）

ctrl + N搜索

ctrl + F12查找方法

ctrl + B(ctrl + 左键点击)进入方法

#### 运算符
运算符：对字面量或者变量进行操作的符号
表达式：用运算符把字面量或者变量连接起来的式子

隐式转换（自动类型提升）:取值范围小的和大的在一起运算，会先提升到大的再运算。byte short char三种数据在运算的时候都会先提升到int再进行运算。
强制转换：那把一个取值范围大的转换为小的——目标数据类型)被转的数据


-算术运算符
	加(+)、减(-)、乘(\*)、除(/)、取余  (%)
	类似C
	“+”的两边出现字符串时，就是字符串连接符了，会把前后数据拼接(只要一边有就行)
	"abc" + 1.23 = "abc1.23"           "abc" + true = "abctrue"
	字符加字符或字符加数字时，加的是ASCII值

-自增自减运算符
	++(前置/后置)、--(前置/后置)
	类似C

-赋值运算符
	=、+=、-=、/=、%= ...(底层隐藏了一个强制类型转换)
	类似C

-关系运算符/比较运算符
	\==、!=、>=、<=、>、<
	结果为boolean类型，成立为true、不成立为false

-逻辑运算符
	&、|、^、!

-短路逻辑运算符号
	&&、||
	具有短路效果，用的更多些
	&、|、~可以按位，>> <<也是有的

-位逻辑运算符
	&(按位与)、|(按位或)、<<(左移，低位补0)、>>(右移，高位补0或1，由原来正负决定)、>>>(无符号右移，高位补0)


-三元运算符
	?   :
	关系表达式?表达式1:表达式2

IDEA中ctrl+alt+L格式化代码

运算优先级：

![[截图 2023-08-26 23-01-50.png]]

建议加小括号让代码便于阅读

#### 流程控制语句
-顺序结构
从上往下依次执行

-分支结构

if语句:类似C，大括号建议写在第一行末尾

if(关系表达式){
	//语句体;
}


if(关系表达式){
	//语句体1;
}
else{
	//语句体2;
}


if(关系表达式1){
	//语句体1;
}
else if(关系表达式2){
	//语句体2;
}
else if(关系表达式3){
	//语句体3;
}
......
else{
	//语句体;
}


switch语句:类似C

switch(表达式){
	case 值1:
		语句体1;
		break;
	case 值2:
		语句体2;
		break;
	case 值3:
		语句体3;
		break;
	......
	default:
		语句体;
		break;

}

说明：1.表达式的取值为byte、short、int、char类型。JDK5后可以是枚举，JDK7后可以是String。

2.case后面只能是字面量，不能是变量，且不允许重复。

3.default可以省略，但不建议省略。可以不写在最下面，但建议写在最下面。

4.break省略的话会case穿透，有时可以用case穿透简化代码。

5.JDK12中switch新特性：可以省略break且不造成case穿透

switch(表达式){  
	case 值1 -> {  
		语句体1;
	}  
	case 值2 -> {  
		语句体2;
	}  
	case 值3 -> {  
		语句体3;
	}  
	default -> {  
		语句体;
	}  
}

语句体只有一行时可以省略大括号

switch(表达式){  
	case 值1 -> 语句1;
	case 值2 -> 语句2;
	case 值3 -> 语句3;
	default -> 语句体;
}

返回的都是一个变量的值是JDK12也可以直接赋值到变量

以简化代码

```
//    switch(a){  
//        case 1:  
//            System.out.println("一");  
//            break;  
//        case 2:  
//            System.out.println("二");  
//        case 3:{  
//            System.out.println("三");  
//            break;  
//        }  
//        default:{  
//            System.out.println("非法输入");  
//            break;  
//        }  
//    }  


        switch(a){  
            case 1 -> {  
                System.out.println("一");  
            }  
            case 2 -> {  
                System.out.println("二");  
            }  
            case 3 -> {  
                System.out.println("三");  
            }  
            default -> {  
                System.out.println("非法输入");  
            }  
        }


        String str = switch(a){  
            case 1 -> "一"；
            case 2 -> "二"；
            case 3 -> "三"；
            default -> ""
        };

```

case中多个情况结果一致时可以用case穿透或者直接逗号隔开。
```
case 1,2,3,4,5:
```


-循环结构
1.for循环
类似C：
for (初始化语句;条件判断语句;条件控制语句){
	循环体语句;
}
```
for(int i = 1;i<=10;i++){
	System.out.println("HelloWorld");
}
```

2.while循环
类似C：
初始化语句;
while (条件判断语句){
	循环体语句;
	条件控制语句;
}

```
int i = 1;
while (i<=10){
	System.out.println("HelloWorld");
	i++；
}
```

3.do while循环
类似C：
初始化语句;
do{
	循环体语句;
	条件控制语句;
}while(条件判断语句);

```
int i = 1;
do {
	System.out.println("HelloWorld");
	i++；
}while(i <= 10)
```

无限循环
for(;;){
	语句;
}

while(true){
	语句;
}

do{
	语句;
}while(true);

跳转控制语句：关键字——continue、break    类似C
IDEA中用fori可以创建一个for循环
```
for (int i = 0; i < ; i++) {  
      
}
```

在一个变量已经被定义后加上.fori或者用一个整数加上.fori可以补全
int num = 0;
num.fori->
```
for (int i = 0; i < num; i++) {  
      
}
```

10.fori->
```
for (int i = 0; i < 10; i++) {  
      
}

```

#### 生成随机数——Random类
导包->创建对象->接收数据
```
import java.util.Random;  //导包
  
public class RandomTest {  
    public static  void main(String[] args){  
        Random r = new Random();  //创建对象
        int number = r.nextInt(随机数范围);  //接收数据
    }  
}
```

其中，随机数范围感觉和python很像，左闭右开
int number = r.nextInt(1,100);
是1~99之间的整数范围
只写一个数时，从0开始到这个数-1
int number = r.nextInt(100);
是0~99之间的整数范围
#### 数组
1.数组介绍
数组是一种容器，可以用来存储**同种数据类型**的多个值

2.数组的定义和静态初始化
定义：两种格式
int\[] 数组名                   int \[] array 
int 数组名\[]                   int array\[]

在Java中习惯用第一种形式

初始化：静态/动态，在内存中为数组容器开辟空间，并将数据存入容器过程
静态初始化方法：
完整格式是：数据类型\[] 数组名 = new 数据类型{元素1 ,  元素2, 元素3 ,...};
例如：
```
int[] array = new int[]{11,22,33};
double[] array2 = new double[]{11.1, 22.2, 33.3};
```

new 数据类型\[] 可以简化掉
简化格式是：数据类型\[] 数组名 = {元素1 ,  元素2, 元素3 ,...};
例如：
```
int[] array = {11,22,33};
double[] array2 = {11.1, 22.2, 33.3};
```

这时候数组长度就固定了

3.数组的地址

```
int[] arr = {1,2,3,4,5};  
System.out.println(arr);//[I@3fee733d
```

打印的是数字的地址，表示数组在内存中的位置。

对``[I@3fee733d``的解释：
\[  表示数组
I  表示数组的元素类型都是int
@  固定格式，是一个分隔的符号
3fee733d  数组的地址值(16进制表示)

习惯上可以把整个叫做数组的地址值，但实际上只有@后面的是数组的地址值

4.数组元素访问
格式：数组名\[索引];
索引从0开始，也叫下标，角标

5.数组的遍历
可以用for循环，但是数组的长度怎么求呢?
在Java中，关于数组的一个长度属性：length
调用方式：数组名.length

举例：
```
//遍历arr数组
for (int i = 0; i < arr.length; i++)
{
	System.out.println(arr[i]);
}
```

在IDEA中，可以自动快速生成数组的遍历方式
数组名.fori
回车即可

6.数组的动态初始化
动态初始化：初始化时只指定数组长度，由系统为数组分配初始化值。

格式：数据类型\[] 数组名 = new 数据类型\[数组长度];

举例:
```
int[] arr = new int[3];
```

其中默认初始化值与类型有关i:
整数类型：默认初始化值为0
浮点数类型：默认初始化值为0.0
字符类型：默认初始化值为'\\u0000' (打印出来就是一个空格)
布尔类型：默认初始化值为false
引用数据类型（如：string）：默认初始化值为null

静态/动态初始化的区别：
静态初始化：手动指定数组元素，系统根据元素计算长度。适用于已知所有要操作的具体数据的情况。

动态初始化：手动制定数组长度，系统给出默认初始值。适用于已知要操作的元素个数而不知道具体数值的情况。

7.数组的注意事项
访问数组中不存在的索引会引发索引越界异常。
**索引从0开始**

```
System.out.println();//会换行
System.out.print();//不换行
```

8.数组内存图
-Java的内存分配
在JVM中，内存被分为以下部分：
JDK7以前，分为：**本地方法栈、寄存器、栈、堆、方法区**，其中堆、方法区是连在一起的
而堆、方法区是连在一起的的方式存在弊端。
所以在JDK8后，分为**本地方法栈、寄存器、栈、堆、元空间**，取消方法区，新增元空间，将原来方法区的功能有的放到堆中，有的放在元空间中。

为方便理解，先以方法区来说：
栈：方法运行时使用的内存，比如main方法运行，进入方法栈中执行。
堆：储存对象或数组，用new来创建，都储存在堆内存。
方法区：储存可以运行的class文件。
本地方法栈：JVM在使用操作系统功能时候使用，和开发无关。
寄存器：给CPU使用。和开发无关

![[截图 2023-08-30 21-48-46.png]]


![[截图 2023-08-30 21-54-46.png]]

new一个数组之后，在堆里面开辟一个空间，栈里面main中arr存空间地址，多个new就是开辟多个不同的小空间。

由此，也可以让两个数组同时指向一个空间

```
public class array_test {  
    public static void main(String[] args) {  
        int[] arr1 = {1,2,3};  
        int[] arr2 = arr1;  
        System.out.println(arr1);  //[I@3fee733d
        System.out.println(arr2);  //[I@3fee733d
        System.out.print("arr1: ");  
        for (int i = 0; i < arr1.length; i++) {  
            System.out.print(arr1[i] + " ");  //arr1: 1 2 3 
        }  
        arr2[0] = 3;  
        System.out.println();  
        System.out.print("arr1: ");  
        for (int i = 0; i < arr1.length; i++) {  
            System.out.print(arr1[i] + " ");  //arr1: 3 2 3 
        }  
    }  
}
```
output：
![[截图 2023-08-30 22-03-34.png]]
当两个数组同时指向同一块空间时，一个数组的改变会影响另一个。

9.二维数组
存放一维数组

二维数组静态初始化：
数据类型\[]\[] 数组名 = new 数据类型\[]\[] {{元素1,元素2,...},{元素1,元素2,...}};

其中类似一维数组可以简化new 数据类型
数据类型\[]\[] 数组名 = \[]\[] {{元素1,元素2,...},{元素1,元素2,...}};
也类似一维数组写成：数据类型 数组名\[]\[]
但Java中更加建议第一种方式
建议二维数组中每个一维数组分开换行写便于阅读

```
public class array_test {  
    public static void main(String[] args) {  
        int[][] arr1 = new int[][]{{1,2,3},{4,5,6,7,8}};  
        int[][] arr2 = {{1,2,3},{4,5,6,7,8}};  
        int[][] arr3 = {  
                {1,2,3},  
                {4,5,6,7,8}  
        };  
        System.out.println(arr1);  //[[I@3fee733d
        System.out.println(arr1[0]);  //[I@5acf9800
        System.out.println(arr1[0][0]);  //1
    }  
}
```

arr\[0]中是第一个一维数组的地址

二维数组的遍历：
```
for (int i = 0; i < arr1.length; i++) {  
    for(int j = 0; j < arr1[i].length; j++)  
    {  
        System.out.println(arr1[i][j]);  
    }  
}
```

二维数组动态初始化：
数据类型\[]\[] 数组名 = new 数据类型\[m]\[n];
m表示二维数组的长度。可以放多少个一维数组
n表示和每一个一维数组可以放多少个元素

n可以省略后面再定义一维数组存

二维数组的内存图

![[截图 2023-09-01 02-08-57.png]]

![[截图 2023-09-01 02-12-47.png]]

![[截图 2023-09-01 02-12-56.png]]

#### 方法
1.方法
方法是什么？
方法（method）是程序中最小的执行单元。

方法有什么用呢？
可以将重复的或有独立功能的代码写在方法中，提高代码的复用性和代码的可维护性。

2.方法的格式
IDEA中可以ctrl + D 将本行代码复制到下一行
(1)方法的定义
```
public static 返回值类型 方法名(参数){
	方法体;
	return 返回值;
}
```

例子：
```
public class method_test {  

    public static void main(String[] args) {  
        System.out.println(add(10,20));  //30
    }  
  
    public static int add(int num1,int num2) {  
        int res = num1 + num2;  
        return res;  
    }  
}
```

注意：方法调用时，实参的数量与类型必须与形参的数量与类型一一对应，否则会报错。

形参：形式参数，方法定义中的参数
实参：实际参数，方法调用中的参数

方法和方法之间不能嵌套**定义**

3.方法的重载

在**同一个类**中，定义多个**同名的**方法，这些同名方法具有同种功能，而每个方法具有**不同的参数类型**或**参数个数**。这些同名的方法，就构成了重载关系。

即：**同一个类**中，方法名相同，参数不同的方法，构成重载。**与返回值类型无关**
参数不同包括：个数不同、类型不同、顺序不同

顺序不同可以构成重载，但不建议。

Java虚拟机会通过不同的参数来区分同名的方法。

4.方法调用的内存原理

方法被调用之后进栈运行

栈：先进后出

方法传递基本数据类型与引用数据类型的区别

基本数据类型：整数类型、浮点数类型、布尔类型、字符类型
引用数据类型：存储地址值，new出来的

传递基本数据类型时，传的是真实的数据，形参的改变不影响实际参数的值。
传递引用数据类型时，传的是地址值，形参的改变影响实际参数的值。

### 2.面向对象

面向对象：写程序的套路
面向：拿、找
对象：能干活的东西
面向对象编程：拿东西来做对应的事情

面向对象的例子
```
Random r = new Random();
Scanner sc = new Scanner(System.in);
System.out.println();
```

学习获取已有对象使用、学习设计对象使用

#### 设计对象并使用
（1）类和对象
类：是对对象共同特征的描述，相当是一个设计图
对象：是真实存在的具体东西

**在Java中，必须先设计类，才能获得对象**

定义类：
```
public class 类名{
	成员变量（代表属性，一般是名词）
	成员方法（代表行为，一般是动词）
	构造器
	代码块
	内部类
}
```
先学习：成员变量（代表属性，一般是名词）、成员方法（代表行为，一般是动词）
例如：
```
public class phone{
	//属性（成员变量）
	String brand;
	double price;
	//行为（方法）
	public void call(){
	
	}
	public void playGame(){
	
	}
}
```

得到类的对象：
类名 对象名 = new 类名();
例如：
```
phone p = new phone();
```

使用对象

访问属性：
对象名.成员变量

访问行为：
对象名.方法名

例如：
Phone.java:
```
public class Phone {  
    //属性（成员变量）  
    String brand;  
    double price;  
  
    //行为（方法）  
    public void call() {  
        System.out.println("打电话");  
    }  
  
    public void playGame() {  
        System.out.println("玩游戏");  
    }  
}
```

PhoneTest.java:
```
public class phonetest {  
    public static void main(String[] args) {  
        //创建手机的对象  
        Phone p = new Phone();  
  
        //给手机品牌赋值  
        p.brand = "华为";  
        p.price = 1999.98;  
  
        //获取手机对象中的值  
        System.out.println(p.brand);  
        System.out.println(p.price);  
  
        //调用手机对象中的方法  
        p.call();  
        p.playGame();  
    }  
}
```

注意事项：
1.Javabean类：用来描述一类事物的类。
在Javabean类中，是不写main方法的。

2.测试类：编写main方法的类
我们可以在测试类中创建Javabean类的对象并进行赋值调用。

类名首字母建议大写，需要见名知意，驼峰模式。
一个Java文件中可以定义多个class类，且只能一个类是public修饰，而且public修饰的类名必须是代码文件名。
**实际开发中还是建议一个文件定义一个class类**

成员变量的完整定义格式是：
修饰符 数据类型 变量名 = 初始化值; 
但一般无需指定初始化值，存在默认初始化值。

默认初始化规则：
![[截图 2023-09-03 21-20-07.png]]

修饰符在后面介绍。

开发中类的设计：可以从需求中提取名词作为属性，动词作为方法

#### 封装
面向对象的三大特征：**封装、继承、多态**

封装用于告诉我们**如何正确设计对象的属性和方法**
封装的思想：对象代表什么，就得封装对应的数据，并提供数据对应的行为

例如：人画圆的方法draw();应该放在人对象中还是圆对象中呢？
应该放在圆方法中，因为圆方法中才提供了圆的半径，而画圆需要圆的半径。

封装的好处：
让编程变得简单，有什么事，找对象，调方法就行。
降低我们的学习成本，可以少学、少记或者说不用怎么学，不用记对象有哪些方法，有需要时找到方法就行。

#### private关键字
private关键字是一个**权限修饰符**，可以修饰成员（成员变量和成员方法），被private修饰的成员只能在本类中才能访问。

这样可以防止数据被赋值为不合理的值，但这样正常的值也不能被赋值了。

我们想要的是正常的数据可以赋值，错误的数据无法赋值
在测试类赋值时加一个if判断并不方便（每次新建对象都要判断）
而且根据封装原则，对象代表什么，就得封装对应的数据，并提供数据对应的行为。我们最好在类中提供相应的方法。

例如：要求女朋友对象中女朋友的年龄要大于等于18岁，小于等于50岁。我们就可以将年龄定义为私有(private)，防止直接赋值，而在**类中提供相应方法来赋值和获取**。

GirlFriend.java：
```
public class GirlFriend {  
    private int age;  
    public void SetAge(int a){  //赋值方法
        if(a >= 18 && a <= 50){
	        age = a;
        }
        else{
	        System.out.println("非法数据");  
        }
    }  
    public int GetAge(){  //获取方法
        return age;
    }  
}
```

GirlFriendTest.java：
```
public class GirlFriendTest {  
    public static void main(String[] args) {  
        GirlFriend gf = new GirlFriend();  
        gf.SetAge(-18);  
        System.out.println(gf.GetAge());  
  
        gf.SetAge(19);  
        System.out.println(gf.GetAge());  
    }  
}
```

输出：
![[截图 2023-09-04 20-09-54.png]]
#### this关键字
当代码中成员变量与局部变量重名时，Java会优先使用局部变量
例如上面的代码中SetAge我们不想用a这个不太有意义的变量名：
```
public class GirlFriend {  
    private int age;  
    public void SetAge(int age){  //赋值方法
        if(age >= 18 && age <= 50){
	        age = age;  //这时前面的age是局部变量的，无法赋值到成员变量中
        }
        else{
	        System.out.println("非法数据");  
        }
    }  
    public int GetAge(){  //获取方法
        return age;
    }  
}
```

而this关键字可以指定为成员变量，修改为
```
public class GirlFriend {  
    private int age;  
    public void SetAge(int age){  //赋值方法
        if(age >= 18 && age <= 50){
	        this.age = age;  //这时前面的age是成员变量的age
        }
        else{
	        System.out.println("非法数据");  
        }
    }  
    public int GetAge(){  //获取方法
        return age;
    }  
}
```

#### 构造方法

构造方法也叫做构造期、构造函数。
作用是在创建对象的时候由虚拟机自动调用给成员变量进行初始化的。

格式：
```
public 类名{
	修饰符 类名(参数){
		方法体;
	}
}
```

特点：
（1）方法名与类名相同，大小写也要一致
（2）没有返回值类型，连void都不能写
（3）没有具体的返回值（不能return）

构造方法不能手动调用，创建对象时由虚拟机调用
每创建一次对象，就会调用一次构造方法

构造方法中参数为空时称之空参构造
构造方法中有参数是带参构造方法

没有写构造方法时虚拟机会默认加上一个空参构造方法

例如：
```
public class GirlFriend {  
    private int age;  
    public GirlFriend()  
    {  
        System.out.println("空参构造方法被执行");  
    }  
  
    public GirlFriend(int age)  
    {  
        if(age >= 18 && age <= 50){  
            this.age = age;  //这时前面的age是成员变量的age  
        }  
        else{  
            System.out.println("非法数据");  
        }  
    }  
    public void SetAge(int age){  //赋值方法  
        if(age >= 18 && age <= 50){  
            this.age = age;  //这时前面的age是成员变量的age  
        }  
        else{  
            System.out.println("非法数据");  
        }  
    }  
    public int GetAge(){  //获取方法  
        return age;  
    }  
}
```


```
public class GirlFriendTest {  
    public static void main(String[] args) {  
        GirlFriend gf1 = new GirlFriend();  
        GirlFriend gf2 = new GirlFriend(19);  
  
        System.out.println(gf1.GetAge());  
        System.out.println(gf2.GetAge());  
    }  
}
```

结果：
```
空参构造方法被执行
0
19

Process finished with exit code 0
```
注意事项：
1.如果没有定义构造方法，系统将给出一个默认的无参数构造方法。

2.如果定义了构造方法，系统就不再提供默认的构造方法。
例如将上面的代码注释一部分：
```
public class GirlFriend {  
    private int age;  
//    public GirlFriend()  
//    {  
//        System.out.println("空参构造方法被执行");  
//    }  
  
    public GirlFriend(int age)  
    {  
        if(age >= 18 && age <= 50){  
            this.age = age;  //这时前面的age是成员变量的age  
        }  
        else{  
            System.out.println("非法数据");  
        }  
    }  
    public void SetAge(int age){  //赋值方法  
        if(age >= 18 && age <= 50){  
            this.age = age;  //这时前面的age是成员变量的age  
        }  
        else{  
            System.out.println("非法数据");  
        }  
    }  
    public int GetAge(){  //获取方法  
        return age;  
    }  
}
```

GirlFriendTest.java中这句就会报错：
GirlFriend gf1 = new GirlFriend();

有时候我们可能需要先new一个对象，再去得到数据，所以空参构造也是有必要的。

构造方法是可以重载的，像最开始的代码中我们就写了两个构造方法，一个带参，一个无参，方法名相同但参数不同，构成重载。

所以建议**无论是否使用，都手动书写无参数的构造方法和带参数的构造方法**



#### 标准JavaBean类
（1）类名见名知意
（2）成员变量用private修饰以保证安全
（3）提供至少两构造方法：无参构造方法和带全部参数的构造方法
（4）成员方法要至少提供每一个成员变量的setXXX()和getXXX()

#### 对象的内存图
加载字节码文件的工作在元空间，但暂时我们还是叫方法区。
将字节码文件加载到方法区中临时存储。

一个对象的内存图：
在创建对象时，会做：
1.加载class文件
2.申明局部变量
3.在堆中开辟空间
4.默认初始化
5.显示初始化：在定义成员变量时如果直接给值了就会显示初始化
6.构造方法初始化
7.将空间的地址值赋值给左边的局部变量

![[截图 2023-09-07 20-27-45.png]]

两个（多个）对象的内存图:

![[截图 2023-09-07 20-32-39.png]]

类比数组，两个引用指向同一个对象：

![[截图 2023-09-07 20-35-16.png]]

#### 基本数据类型与引用数据类型

基本数据类型：存的是真实的值，数据值存储在自己的空间中
引用数据类型：存地址，数据值存储在其他的空间中，自己空间储存地址值

#### this的内现原理
this可以区分同名的局部变量和成员变量

this的本质：所在方法调用者的地址值。

![[截图 2023-09-08 20-26-05.png]]

![[截图 2023-09-08 20-29-59.png]]
![[截图 2023-09-08 20-31-15.png]]

#### 成员变量和局部变量的区别

成员变量：类中方法外的变量
局部变量：方法中的变量

![[截图 2023-09-08 20-36-24.png]]

#### 面向对象综合案例

题目1：设计一个文字格斗游戏，开始A，B有100血量，A打B一下，扣随机1~20血量，再B打A扣随机1~20血量的回合制游戏。

代码样例：
Role.java:
```
import java.util.Random;  
  
public class Role {  
    private String name;  
    private int blood;  
    public Role(){  
    }  
  
    public Role(String name,int blood){  
        this.name = name;  
        this.blood = blood;  
    }  
  
    public void setName(String name){  
        this.name = name;  
    }  
  
    public String getName(){  
        return name;  
    }  
  
    public void setBlood(int blood){  
        this.blood = blood;  
    }  
  
    public int getBlood(){  
        return blood;  
    }  
  
    public void attack(Role role){  
        Random r = new Random();  
        int hurt = r.nextInt(20) + 1;  
        int remainBlood = role.getBlood() - hurt;  
        remainBlood = remainBlood > 0 ? remainBlood : 0;  
        role.setBlood(remainBlood);  
        System.out.println(this.getName() + "攻击了" + role.getName() + "，造成了" + hurt + "的伤害，" +  
                role.getName() + "还剩下" + role.getBlood() + "点血量。");  
  
    }  
  
}
```


GameTest.java:
```
public class GameTest {  
    public static void main(String[] args) {  
        Role role1 = new Role("A",100);  
        Role role2 = new Role("B",100);  
        while(true){  
            role1.attack(role2);  
            if(role2.getBlood() == 0){  
                System.out.println("游戏结束，" + role1.getName() + "胜利！");  
                break;  
            }  
            role2.attack(role1);  
            if(role1.getBlood() == 0){  
                System.out.println("游戏结束，" + role2.getName() + "胜利！");  
                break;  
            }  
        }  
    }  
}
```

System.out.printf();语句介绍：
类似C的printf，格式化输出
System.out.printf("Hello %s!","World"); //Hello World!

题目2：对象数组，设计一个对象数组，存三个商品对象，商品的类中有：id、名字、价格、库存。

参考代码：
Goods.java
```
public class Goods {  
    private String id;  
    private String name;  
    private double price;  
    private int count;  
  
    public Goods(){  
    }  
  
    public Goods(String id,String name,double price,int count){  
        this.id = id;  
        this.name = name;  
        this.price = price;  
        this.count = count;  
    }  
  
    public String getId() {  
        return id;  
    }  
  
    public void setId(String id) {  
        this.id = id;  
    }  
  
    public String getName() {  
        return name;  
    }  
  
    public void setName(String name) {  
        this.name = name;  
    }  
  
    public double getPrice() {  
        return price;  
    }  
  
    public void setPrice(double price) {  
        this.price = price;  
    }  
  
    public int getCount() {  
        return count;  
    }  
  
    public void setCount(int count) {  
        this.count = count;  
    }  
}
```

GoodsTest.java:
```
package demo2_object;  
  
import java.util.Scanner;  
  
public class GoodsTest {  
    public static void main(String[] args) {  
        Goods[] goods = new Goods[3];  
        Scanner sc = new Scanner(System.in);  
        for (int i = 0; i < goods.length; i++) {  
            Goods g = new Goods();  
            System.out.println("输入商品id：");  
            String id = sc.next();  
            g.setId(id);  
            System.out.println("输入商品名称：");  
            String name = sc.next();  
            g.setName(name);  
            System.out.println("输入商品价格：");  
            double price = sc.nextDouble();  
            g.setPrice(price);  
            System.out.println("输入商品存货数目：");  
            int count = sc.nextInt();  
            g.setCount(count);  
  
            goods[i] = g;  
        }  
        for (int i = 0; i < goods.length; i++) {  
            System.out.println(goods[i].getId() + " " + goods[i].getName() + " " + goods[i].getPrice()+ " " + goods[i].getCount());  
        }  
    }  
}
```






### 3.API&字符串
#### API

API(Appiication Programming Interface)：应用程序编程接口
API简单理解就是使用别人已经写好的东西。
```
public static void main(String[] args){
	Random r = new Random();
	int number = r.nextInt(100);
}
```

Java API：指的就是JDK中提供的各种功能的Java类
这些类将底层的实现封装了起来，我们不需要关心这些类是怎么实现的，只需要学习这些类如何使用即可。

例如我们以及学习过的API：Scanner、Random

还有许许多多其他的API，在Java文档中收录：JDK-API帮助文档.CHM

API帮助文档使用：
1.打开帮助文档
2.点击显示，找到索引下面的输入
3.在输入框中输入类名并显示
4.查看类所在的包
5.查看类的描述
6.查看构造方法
7.查看成员方法

#### String
接下来，我们就可以通过API帮助文档查看字符串的使用方法。

由于字符串的操作内容有很多，所以Java也提供了很多字符串的API，例如：String,StringBuilder,StringJonier,Pattern,Matcher。

String概述：
Java.lang.String类代表字符串，Java程序中所有字符串文字都为此类的对象。

注意：字符串的内容是不会发生改变的，它的对象在创建之后值不能被更改。

String是Java定义好的一个类，在Java.lang包中。Java.lang包不需要导包。

创建字符串对象
1.直接赋值：String name = "ripple";
2.new
构造方法：
```
public String()  创建空白字符串，不含任何内容
public String(String original)  根据传入的字符串，创建字符串对象
public String(char[] chs)  根据字符数组，创建字符串对象
public String(byte[] chs)  根据字节数组，创建字符串对象 
```

字符串的内存模型：
StringTable --- 串池（在JDK7版本开始，StringTable从方法区中挪到了堆内存中）

第一种方法直接赋值的字符串在StringTable中

![[截图 2023-09-18 19-49-20.png]]

当使用双引号直接赋值时，系统会检查该字符串是否在串池中存在，不存在才创建新的，存在的话就复用。

![[截图 2023-09-18 20-01-14.png]]


用第二种创建方式时，不会复用，所以相同的字符串较多时可能会浪费空间。所以一般用第一种创建方式，简单又节约内存。

##### 比较字符串

直接用\==行吗？
String是引用数据类型，当用\==去比较字符串的时候其实是比较的地址值，而不是具体的内容，所以是不行的，例如下面的例子：

```
public class Test {  
    public static void main(String[] args) {  
        String str1 = "123";  
        String str2 = "123";  
        String str3 = new String("123");  
        String str4 = new String("123");  
        System.out.println(str1 == str2);  //true
        System.out.println(str3 == str4);  //false
    }  
}
```


上面的例子结合字符串内存原理就可以很好的体现了

那如何去判断呢？-可以使用方法：
.equals()

```
public class Test {  
    public static void main(String[] args) {  
        String str1 = "123";  
        String str2 = "123";  
        String str3 = new String("123");  
        String str4 = new String("1234");  
        System.out.println(str1.equals(str3));  //true
        System.out.println(str3.equals(str4));  //false
    }  
}
```

.equalsIgnoreCase()  忽略大小写比较

```
public class Test {  
    public static void main(String[] args) {  
        String str1 = "abc";  
        String str2 = new String("aBc");  
        System.out.println(str1.equalsIgnoreCase(str2));  //true
    }  
}
```

String str = sc.next();
这里的next是new出来的字符串

##### 遍历字符串

public char charAt(int index)    根据索引返回字符，类似数组的索引
public int length()    返回数组的长度

对比：数组的长度是属性，所以是arr.length
          求字符的长度是方法，所以是str.length()

IEDA可以用str.length().fori来快速创建for循环

遍历字符串：
```
import java.util.Scanner;  
  
public class StringDemo1 {  
    public static void main(String[] args) {  
        Scanner sc = new Scanner(System.in);  
        String str = sc.next();  
        for (int i = 0; i < str.length(); i++) {  
            System.out.println(str.charAt(i));  
        }  
    }  
}
```

##### 截取字符串
方法：substring
String substring(int beginIndex,int endIndex)

左闭右开
beginIndex取得到，endIndex取不到

重载方法：
String substring(int beginIndex)
从beginIndex取到尾

返回值为子串，对原字符串无影响

##### 字符串替换
方法：replace
String replace(旧值,新值)

返回值为替换后结果，对原字符串无影响，替换的是所有的旧值

#### StringBuilder
StringBuilder可以看成是一个容器，创建之后里面的内容是**可变的**。
作用：提高字符串的操作效率。

构造方法：
public StringBuilder()  //创建一个空白的可变字符串对象，不含有任何内容

public StringBuilder(String str)  //根据字符串内容，来创建可变的字符串对象

常用成员方法：
public StringBuilder append(任意类型)  //添加数据，并返回对象本身

public StringBuilder reverse()  //反转容器中的内容

public int length()  //返回长度

public String toString()  //把StringBuilder转换为String

由于StringBuilder是Java已经写好的类，Java在底层对他作了一些特殊处理，打印对象不是地址值而是属性值。

链式编程:调用一个方法之后，不用变量接收结果，继续调用其他方法。例如：
```
String str_reverse = new StringBuilder().append(str).reverse().toString();
```

使用StringBuilder场景：
1.字符串的拼接
2.字符串的反转

#### StringJoiner

StringJoiner与StringBuilder一样，也可以看作是一个容器，创建后内容可变。

作用：提高字符串的操作效率，且代码编写简洁。但目前市场上很少人有人用。

import java.util.StringJoiner;

**JDK8出现的**

构造方法：
public StringJoiner(间隔符号)  //创建一个StringJoiner对象，指定拼接的间隔符号

public StringJioner(间隔符号,开始符号,结束符号)  //创建一个StringJoiner对象，指定拼接的间隔符号、开始符号、结束符号

成员方法：
public StringJoiner add(添加的内容)  //添加数据，并返回对象本身

public int length()  //返回字符串长度，为所有字符的总个数

public String toString()  //转换为字符串

创建之后利用add添加元素

例如，写一个方法，将整型数组中的元素转换为字符串，格式为：\[1, 2, 3]

```
import java.util.StringJoiner;  
  
public class StringJoinerTest1 {  
    public static void main(String[] args) {  
        int[] arr = {1, 2, 3};  
        System.out.println(arrToString(arr));  
    }  
  
    public static String arrToString(int[] arr) {  
        StringJoiner sj = new StringJoiner(", ", "[", "]");  
        for (int i = 0; i < arr.length; i++) {  
            sj.add(arr[i] + "");  
        }  
        return sj.toString();  
    }  
}
```

#### 字符串原理

##### 字符串存储的内存原理
参考String部分：
1.直接赋值会复用字符串常量池中的
2.new出来不会复用，而是开辟一个新的空间

##### \==号比什么？
比较基本数据类型时比的是数据值
比较引用数据类型时比的是地址值

##### 字符串拼接的底层原理
在等号右边没有变量参与和有变量参与

没有变量参与:
```
String s = "a" + "b" + "c";
System.out.println(s);
```

有变量参与:
```
String s1 = "a";
String s2 = s1 + "b";
String s3 = s2 + "c";
System.out.println(s3);
```

1.在等号右边没有变量参与时，会触发字符串优化机制，在编译时就已经是最终结果了。
在.class文件中。就已经是``String s = "abc";``
为拼接之后的结果了

2.在等号右边有变量参与时：
**JDK8以前**底层会使用StringBuilder进行拼接
在执行``String s2 = s1 + "b";``时，本质上是``String s2 = new StringBuilder().append(s1).append("b").toString();``

而toString();方法可以在IEDA中用ctrl + N选择all place搜索StringBuilder找到源码后ctrl + F12查找toString方法可以发现是调用了newString方法，ctrl + B跟进，发现是new出来的一个字符串，因此在堆中非串池处。

![[截图 2023-10-03 11-10-10.png]]

而我们发现创建了两个StringBuilder对象，因此效率不高。

**JDK8及以后**对字符串的拼接做了优化，有许多方案，介绍默认的一种。
会先预估最终字符串拼接的长度，并创建一个数组，存入拼接内容最后拼接为字符串。

不过预估也是需要时间的，会减慢效率。

因此，如果很多字符串需要拼接，不要直接用+
否则，会在底层创建多个对象，浪费时间，浪费性能。

##### StringBuilder提高效率的原理

由前面直接+的坏处来看StringBuilder提高效率的原理已经呼之欲出了。
直接用StringBuilder只创建了一个StringBuilder对象，不会创建很多无用的空间，节约内存、节约时间。

##### StringBuilder源码分析
容量：最多装多少
长度：已经装多少
默认创建一个容量为16的字节数组
一次性添加的内容长度小于等于容量16时，直接存
添加的内容长度大于容量时扩容为原来的容量\*2+2
一次性添加的内容长度扩容后的，就到实际长度为准。

sb.capacity查看容量

```
public class StringBuilderTest3 {  
    public static void main(String[] args) {  
        StringBuilder sb = new StringBuilder();  
        System.out.println(sb.capacity());  
        System.out.println(sb.length());  
  
        System.out.println();  
  
        sb.append("abc");  
        System.out.println(sb.capacity());  
        System.out.println(sb.length());  
  
        System.out.println();  
  
        sb.append("defghijklmnopqrstuvwxyz");  
        System.out.println(sb.capacity());  
        System.out.println(sb.length());  
  
        System.out.println();  
  
        sb.append("0123456789");  
        System.out.println(sb.capacity());  
        System.out.println(sb.length());  
  
        System.out.println();  
  
        StringBuilder sb2 = new StringBuilder();  
        sb2.append("abcdefghijklmnopqrstuvwxyz0123456789");  
        System.out.println(sb2.capacity());  
        System.out.println(sb2.length());  
  
    }  
}
```

输出：
```
16
0

16
3

34
26

70
36

36
36

Process finished with exit code 0
```

#### 字符串小练习

.toCharArray();  //将String变成字符数组

### 5.集合

#### 集合定义与意义

数组的长度是固定的，有没有长度可变的容器呢？--集合

数组的长度是固定的
集合的长度是可变的

数组可以存基本数据类型和引用数据类型
而集合能存引用数据类型但不能存基本数据类型，需要先转换为包装类

Java中有很多集合，如：
```
LineHashMap   LinkedHashSet   TreeSet   TreeMap   Map
HashSet   HashMap   Vector   LinkedList   Collection
Arraylist
```

先来学习较常见的：**Arraylist**

Arraylist类定义在Java.util包下的，所以需要导包
import Java.util.Arraylist

Arraylist<\E>
泛型：限定集合中存储数据的类型，用<>

例如：
```
Arraylist<String> list = new Arraylist<String>();
```
Arraylist\<int> list = new Arraylist\<int>();报错，为什么？-不能存基本数据类型

JDK7以后，后面的String可以省略

```
Arraylist<String> list = new Arraylist<>();
```

Arraylist是Java中一个已经写好的类，在底层做了处理，打印对象不是地址值，而是集合中存储的数据内容，在展示时用\[]把所有数据包裹。

Arraylist成员方法：

|     作用       |   方法名                 |       具体说明                 |
|     -------    |    --------------      |   -------------------------   |
|     增         |boolean add(E e)        | 添加指定元素，返回值代表是否成功    |
|     删         |boolean remove(E e)     | 删除指定元素，返回值代表是否成功    |
|     删         |E remove(int index)     |删除指定索引的元素，返回被删除元素   | 
|     查         | int size()             | 集合的长度，也就是集合中元素的个数  |
|     查         |   E get(int index)     | 获取指定索引的元素               |
|     改         | E set(int index,E e)   | 修改指定索引下的元素，返回原来的元素|

Arraylist中add方法的返回值永远是true
remove方法删除的是第一个，如果删除不存在的值返回false
索引从0开始

```
import java.util.ArrayList;  
  
public class ArraylistTest1 {  
    public static void main(String[] args) {  
        ArrayList<String> list = new ArrayList<>();  
        //添加元素  
        list.add("aaa");  
        list.add("bbb");  
        list.add("ccc");  
        list.add("aaa");  
        System.out.println(list);  
        list.remove("aaa");  
        System.out.println(list);  
  
        //删除元素  
        System.out.println(list.remove("ddd"));  
        System.out.println(list.remove(0));  
        System.out.println(list);  
  
        //修改元素  
        System.out.println(list.set(1,"ddd"));  
        System.out.println(list);  
  
        //查询元素  
        System.out.println(list.get(1));  
  
        //利用size方法遍历   IEDA中：list.fori  
        for (int i = 0; i < list.size(); i++) {  
            System.out.println(list.get(i));  
        }  
    }  
}


//output:
//[aaa, bbb, ccc, aaa]  
//[bbb, ccc, aaa]  
//false  
//bbb  
//[ccc, aaa]  
//aaa  
//[ccc, ddd]  
//ddd  
//ccc  
//ddd
```

基本数据类型对应的包装类：

byte -> Byte
short -> Short
char -> Character
int -> Integer
long -> Long
float -> Float
double -> Double
boolean -> Boolean

JDK5以后int Integer时可以相互转换的

```
import java.util.ArrayList;  
  
public class ArrayListTest2 {  
    public static void main(String[] args) {  
        ArrayList<Integer> list = new ArrayList<>();  
  
        list.add(1);  
        list.add(2);  
        list.add(3);  
        list.add(4);  
  
        System.out.println(list);  
    }  
}

//[1, 2, 3, 4]
```

当然也可以是一个对象

Student.java:
```
public class Student {  
    private String name;  
    private int age;  
  
    public Student() {  
    }  
  
    public Student(String name, int age) {  
        this.name = name;  
        this.age = age;  
    }  
  
    public String getName() {  
        return name;  
    }  
  
    public void setName(String name) {  
        this.name = name;  
    }  
  
    public int getAge() {  
        return age;  
    }  
  
    public void setAge(int age) {  
        this.age = age;  
    }  
}
```

ArrayListTest3.java
```
import java.util.ArrayList;  
  
public class ArrayListTest3 {  
    public static void main(String[] args) {  
        ArrayList<Student> list = new ArrayList<>();  
        Student s1 = new Student("zhandsan",23);  
        Student s2 = new Student("lisi",24);  
        Student s3 = new Student("wangwu",25);  
  
        list.add(s1);  
        list.add(s2);  
        list.add(s3);  
  
        System.out.println(list);  
  
        for (int i = 0; i < list.size(); i++) {  
            Student stu = list.get(i);  
            System.out.println(stu.getName() + ", " + stu.getAge());  
        }  
    }  
}
```

输出：
```
[ArrayListTest.Student@5acf9800, ArrayListTest.Student@4617c264, ArrayListTest.Student@36baf30c]
zhandsan, 23
lisi, 24
wangwu, 25
```


由于Student类是我们自己写的，所以Java底层不会处理。打印的就是地址值了。

如果有时需要一个方法要返回多个数据，可以把这些数据先放到一个容器中再返回容器。

可以给循环起一个名字来实现跳出指定循环
```
public class test {  
    public static void main(String[] args) {  

        loop : for (int i = 0; i < 3; i++) {  
            for (int j = 0; j < 3; j++) {  
                if(i == 0){  
                    break loop;  
                }  
                System.out.println("我没被执行，因为跳出了外层的");  
            }  
        }  
    }  
}
```

System.exit(0);//停止虚拟机运行，相当于退出了整个程序。



### 6.综合应用

#### 学生管理系统



