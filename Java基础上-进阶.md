
## 面向对象进阶
### 1.static
static表示静态，是Java中的一个修饰符，可以修饰成员方法或者成员变量

-修饰成员变量的情况：
被static修饰的成员变量,叫做静态变量
修饰后的变量被该类所有对象共享
**不属于对象，属于类**
**随着类的加载而加载，优先于对象存在**

调用方式：
类名调用（推荐）
对象名调用

例如：
Student.java
```
public class Student {  
    private String name;  
    private int age;  
    public static String teacherName;  
    public String getName() {  
        return name;  
    }  
  
    public void show(){  
        System.out.println(name + "  " + age + "  " + teacherName);  
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
  
    public Student(String name, int age) {  
        this.name = name;  
        this.age = age;  
    }  
  
    public Student() {  
  
    }  
}
```


StaticTest1.java:
```
public class StaticTest1 {  
    public static void main(String[] args) {  
        Student.teacherName = "Mr.Wang";  //类名调用（推荐）
        Student stu1 = new Student("zhangsan",23);  
        Student stu2 = new Student("lisi",18);  
        //stu1.teacherName = "Mr.Wang";  //对象名调用，效果相同  
        stu1.show();  
        stu2.show();  
    }  
}
```

输出：
```
zhangsan  23  Mr.Wang
lisi  18  Mr.Wang
```

static内存原理：

![](Java基础上-进阶-photos/截图%202023-10-10%2021-29-06.png)

-修饰成员方法的情况：
被static修饰的成员方法,叫做静态方法
多用在测试类和工具类中，Javabean类比较少用

调用方式：
类名调用（推荐）
对象名调用

JavaBean类：用来描述一类事物的类。
测试类：用来检查其他类是否书写正确的类，带有main方法的类，是程序的入口。
工具类：不是用来描述事物的类，是帮助我们做一些事情的类

工具类要求：
1.类名见名知意
2.私有化构造方法
原因：私有化构造方法不让外界创造这个对象，工具类创造对象没有意义

定义静态的方法以便通用

例如：定义一个工具类获取集合中最大学生的年龄。
StudentUtil.java:
```
import java.util.ArrayList;  
  
public class StudentUtil {  
    private StudentUtil(){}  
  
    public static int getMaxAge(ArrayList<Student> list){  
        int maxAge = list.get(0).getAge();  
        for (int i = 1; i < list.size(); i++) {  
            int age = list.get(i).getAge();  
            if(age > maxAge){  
                maxAge = age;  
            }  
        }  
        return maxAge;  
    }  
}
```

```
import java.util.ArrayList;  
  
public class StaticTest2 {  
    public static void main(String[] args) {  
        ArrayList<Student> list = new ArrayList<>();  
        Student stu1 = new Student("zhangsan",19);  
        Student stu2 = new Student("lisi",20);  
        Student stu3 = new Student("wangwu",21);  
  
        list.add(stu1);  
        list.add(stu2);  
        list.add(stu3);  
  
        System.out.println(StudentUtil.getMaxAge(list));  
    }  
}
```

**static的注意事项：
1.静态方法只能访问静态变量和方法
2.非静态方法可以访问静态变量和静态方法，也可以访问非静态的成员变量和非静态的成员方法
3.静态方法中没有this关键字**

非静态方法中，有一个隐藏的this，不能手动赋值，是调用方法时虚拟机赋值，表示当前方法调用者的地址值

public void show(){  
    System.out.println(name + "  " + age + "  " + teacherName);  
}

实际上是：
public void show(Student this){  
    System.out.println(name + "  " + age + "  " + teacherName);  
}

为理解证明，修改Student.java中的show方法为：
```
public void show(Student this){  
    System.out.println("this:" + this);  
    System.out.println(name + "  " + age + "  " + teacherName);  
}
```

修改StaticTest1.java:
```
public class StaticTest1 {  
    public static void main(String[] args) {  
        Student stu1 = new Student("zhangsan",23);  
        Student stu2 = new Student("lisi",18);  
        Student.teacherName = "Mr.Wang";  
        //stu1.teacherName = "Mr.Wang";  //效果相同  
        System.out.println("stu1:" + stu1);  
        stu1.show();  
        System.out.println("stu2:" + stu2);  
        stu2.show();  
    }  
}
```

输出：
```
stu1:Student@4617c264
this:Student@4617c264
zhangsan  23  Mr.Wang
stu2:Student@27716f4
this:Student@27716f4
lisi  18  Mr.Wang
```

可以看到this的地址与调用者的地址一致

而且，在非静态方法中调用其他方法时前面也隐含了this.

```
public void show(){  
    System.out.println("this:" + this);  
    System.out.println(name + "  " + age + "  " + teacherName);  
    show2();//前面隐含了this.  
    this.show2();  
}  
  
public void show2(){  
    System.out.println("show2");  
}
```

由于静态方法没有this，所以静态方法只能访问静态变量和方法，非静态方法可以访问所有

内存解释：
静态是随着类的加载而加载的
非静态是和对象有关的

![](Java基础上-进阶-photos/截图%202023-10-12%2013-46-21.png)

![](Java基础上-进阶-photos/截图%202023-10-12%2013-48-45.png)

![](Java基础上-进阶-photos/截图%202023-10-12%2013-51-22.png)

![](Java基础上-进阶-photos/截图%202023-10-12%2013-52-57.png)

单例设计模式会在多线程阶段讲解

**重新认识main方法：**
```
public class HelloWorld{
	public static void main(String[] args){
		System.out.println("HelloWorld!");
	}
}
```

public:被JVM调用，访问权限足够大
static:被JVM调用，不用创建对象，直接类名访问。因为main方法是静态的，只能调用静态方法，所以测试类中其他方法也需要是静态的
void:被JVM调用，不需要给JVM返回值
main:一个通用的名称，程序主入口，虽然不是关键字，但是可以被JVM识别
String\[] args:以前用于接受键盘录入数据的，现在没用，为向下兼容保留



### 2.继承

面向对象三大特征：封装 继承 多态
封装：对象代表什么，就得封装对应的数据，并提供数据对应的行为

继承：
Java中提供一个关键字extends，用这个关键字，我们可以让一个类和另一个类建立起继承关系。
```
public class Student extends Person {}
```
Student称为**子类（派生类）**，Person称为**父类（基类或超类）**。

使用继承的好处：可以把多个子类中重复的代码抽取到父类中，提高代码复用性。
同时，子类可以在父类的基础上，增加其他的功能，使子类更加强大。

-什么时候用继承？
-当类与类之间，存在**相同（共性）的内容**，并满足**子类是父类**的一种，就可以考虑使用继承，来优化代码。

继承的特点：Java只支持单继承，不支持多继承，但支持多层继承。每一个类都直接或者间接地继承与Object。
单继承：一个子类只能继承一个父类
不支持多继承：子类不能同时继承多个父类
多层继承：子类A继承父类B，父类B可以继承父类C。称B为A的直接父类，C为A的间接父类。
**每一个类都直接或者间接地继承于Object**
```
public class A {

}
```
虚拟机自动默认继承Object类
```
public class A extends Object{

}
```

**子类只能访问父类中非私有的成员**

案例：
Animal.java:
```
public class Animal {  
    public void eat(){  
        System.out.println("吃东西");  
    }  
  
    public void drink(){  
        System.out.println("喝水");  
    }  
}
```

Cat.java
```
public class Cat extends Animal{  
    public void catchMouse(){  
        System.out.println("猫抓老鼠");  
    }  
}
```

Husky.Java
```
public class Husky extends Dog{  
    public void breakHome(){  
        System.out.println("哈士奇在拆家");  
    }  
}
```

LiHua.java
```
public class LiHua extends Cat{  
}
```

Ragdoll.java
```
public class Ragdoll extends Cat{  
}
```

Teddy.java
```
public class Teddy extends Dog{  
    public void touch(){  
        System.out.println("泰迪蹭了蹭你");  
    }  
}
```

TestExtends.java
```
public class TestExtends {  
    public static void main(String[] args) {  
        Ragdoll rd = new Ragdoll();  
        rd.eat();  
        rd.drink();  
        rd.catchMouse();  
  
        System.out.println("-----------------------------");  
  
        Husky h = new Husky();  
        h.eat();  
        h.drink();  
        h.lookHome();  
        h.breakHome();  
    }  
}
```


#### 子类到底能继承父类中的哪些内容？

![](Java基础上-进阶-photos/截图%202023-10-17%2016-07-59.png)

父类构造方法不能被子类继承，原因：子类的名称和父类不同，构造方法的命名不同，不能继承。

父类成员变量能被子类继承，但私有变量不能直接使用

内存图角度分析：

![](Java基础上-进阶-photos/截图%202023-10-17%2016-21-13.png)

![](Java基础上-进阶-photos/截图%202023-10-17%2016-24-36.png)

父类成员方法中虚方法能被子类继承，但私有方法不能被继承。

![](Java基础上-进阶-photos/截图%202023-10-17%2016-29-14.png)

不再虚方法表中，只能往上一个一个找，在虚方法中直接调用。

![](Java基础上-进阶-photos/截图%202023-10-17%2016-35-16.png)

fushow2不在虚方法中，一个个往上找找到Fu.class发现是private不能调用报错。

严谨说法：

![](Java基础上-进阶-photos/截图%202023-10-17%2016-37-24.png)
内存分析工具验证

#### 继承中：成员变量的访问特点
就近原则
```
public class Fu{
	String name = "Fu";
}

public class Zi extends Fu{
	String name = "zi";
	public void ziShow(){
		String name = "ziShow";
		System.out.println(name);
	}
}
```

先在局部位置找，本类成员位置找，父类成员位置找，逐级往上。

```
public class Fu{
	String name = "Fu";
}

public class Zi extends Fu{
	String name = "zi";
	public void ziShow(){
		String name = "ziShow";
		System.out.println(name);
		System.out.println(this.name);
		System.out.println(super.name);
	}
}
```
先在局部位置找，本类成员位置找，父类成员位置找，逐级往上。
最多只能一次super

#### 继承中：成员方法的访问特点
直接调用满足就近原则
super调用直接访问父类

类似成员变量

方法重写：当父类的方法不满足子类现在的需求时，需要进行方法的重写。

书写格式：在继承体系中，子类出现了和父类中一模一样的方法声明，我们就称子类这个方法是方法重写的方法。

@Override重写注解：
1.@Override是放在重写后的方法上，较验子类重写时语法是否正确。
2.加上注解后如果后红色波浪线，表示语法错误。
3.建议重写方法都加@Override注解，代码安全，优雅。
例如：
```
@Override
public void eat(){
	System.out.println("吃意大利面");
}
```

方法重写的本质：覆盖了虚方法表中的方法。

注意事项与要求：
1.重写方法的名称、形参列表必须与父类中的一致。
2.子类重写方法时，访问权限子类必须大于等于父类（暂时了解：空着不写<protected<public）
3.子类重写父类方法时，返回值类型子类必须小于等于父类
4.由于重写本质是对虚方法表的覆盖，所以私有方法和静态方法不能被重写，或者说，**只有被添加到虚方法表中的方法可以被重写**

基于2、3两点的难以理解，建议重写时方法尽量和父类保持一致。

#### 继承中：构造方法的访问特点
父类中的构造方法无法被子类继承。
子类中所有的构造方法默认先访问父类中的无参构造，再执行自己的。
原因：子类在初始化的时候，有可能会使用父类中的数据，如果父类没有完成初始化，子类将无法使用父类的数据。

-怎么调用父类的构造方法？
-子类构造方法的第一行语句默认都是``super()``，**不写也存在，虚拟机会加载，且必须在第一行**
如果想调用父类有参构造，必须手动写super进行调用。
Person.java
```
public class Person {  
    String name;  
    int age;  
    public Person(){  
        System.out.println("父类的空参构造");  
    }  
    public Person(String name,int age){  
        this.name = name;  
        this.age = age;  
        System.out.println("父类的带参构造");  
    }  
}
```

Student.java
```
public class Student extends Person{  
    public Student(){  
        super();//子类默认隐藏的方法  
        System.out.println("子类的空参构造");  
    }  
  
    public Student(String name,int age){  
        super(name,age);  
    }  
}
```

Test.java:
```
public class Student extends Person{  
    public Student(){  
        super();//子类默认隐藏的方法  
        System.out.println("子类的空参构造");  
    }  
  
    public Student(String name,int age){  
        super(name,age);  
    }  
}
```

this:理解为一个变量，表示当前方法调用者的地址值
super:代表父类的存储空间

this()：调用本类构造方法
使用场景，例如默认所有学生是王老师
Student.java:
```
package test;  
  
public class Student{  
    String name;  
    int age;  
    String teacher;  
    public Student(){  
        //表示调用本类其他构造方法  
        //这里的this也是必须在第一行
        //细节：虚拟机这时候就不会再添加super()  
        //原因：下面的构造有了，只要一个有super()就行了
        this(null,0,"Mr.Wang");  
    }  
  
    public Student(String name,int age,String teacher){  
        this.age = age;  
        this.name = name;  
        this.teacher = teacher;  
    }  
}
```


### 3.多态
#### 多态概述
面向对象三大特征：封装、继承、多态
封装：对象代表什么，就得封装对应用的数据，并提供数据对应的行为
继承是多态的前提条件
例如，Person类是Student类的父类
此时，学生有学生形态和人的形态，这就是多态
```
Student s = new Student();//学生形态
Person p = new Student();//人的形态
```

多态：同类型的对象，表现出不同的形态。
多态的形式：
```
父类类型 对象名称 = 子类对象;
```

多态的前提：
-有继承/实现关系
-有父类引用指向子类对象 ``Fu f = new Zi();``
-有方法重写

多态的好处：使用父类型作为参数，可以接收所有子类对象，体现了多态的扩展性和便利

例子：
Person.java:
```
public class Person {  
    private String name;  
    private int age;  
  
    public Person() {  
    }  
  
    public Person(String name, int age) {  
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
  
    public void show(){  
        System.out.println(name + "，" + age);  
    }  
}
```
Administrator.java:
```
public class Administrator extends Person{  
    @Override  
    public void show(){  
        System.out.println("管理员的信息为：" + getName() + "," + getAge());  
    }  
}
```
Student.java:
```
public class Student extends Person {  
    @Override  
    public void show(){  
        System.out.println("学生的信息为：" + getName() + "," + getAge());  
    }  
}
```
Teacher.java:
```
public class Teacher extends Person {  
    @Override  
    public void show() {  
        System.out.println("老师的信息为：" + getName() + "," + getAge());  
    }  
}
```
Test.java:
```
public class Test {  
    public static void main(String[] args) {  
        Student s = new Student();  
        s.setName("zhangsan");  
        s.setAge(18);  
  
        Teacher t = new Teacher();  
        t.setName("wang");  
        t.setAge(27);  
  
        Administrator a = new Administrator();  
        a.setName("admin");  
        a.setAge(35);  
  
        register(s);  
        register(t);  
        register(a);  
    }  
  
    //写一个方法，既能接收老师，又能接收学生，还能接收管理员  
    public static void register(Person p) {  
        p.show();  
    }  
}
```
通过多态，我们可以用一个父类Person接收老师，学生，管理员这些子类
输出:
```
学生的信息为：zhangsan,18
老师的信息为：wang,27
管理员的信息为：admin,35
```

#### 多态调用成员的特点
变量调用：编译看左边，运行看左边
方法调用：编译看左边，运行看右边

编译看左边：Javac编译代码时，会看左边的父类中有没有这个变量，如果有，编译成功，反之失败。
运行看左边：Java运行代码时，实际获取的就是左边父类中成员变量的值。

编译看左边：Javac编译代码时，会看左边的父类中有没有这个方法，如果有，编译成功，反之失败。
运行看右边：Java运行代码时，实际运行的是子类中的方法。

理解：f为父类类型，用f调用默认都是从Fu类找，而子类对象中继承了父类的成员变量。如果子类对方法进行了重写，那么在虚方法中是会把父类的方法进行覆盖的。

内存图角度：
加载字节码文件时候是先加载父的再加载子类的。

![](Java基础上-进阶-photos/截图%202023-11-08%2022-37-39.png)

#### 多态的优势与弊端
多态的优势：
-在多态形式下，右边对象可以实现解耦合，便于扩展和维护
-定义方法的时候，使用父类型作为参数，可以接收所有子类的对象，体现多态的扩展性与便利。

多态的弊端：
不能调用子类的特有方法（原因：编译看左边）

解决方案：将调用者变回子类类型就就行了，强制转换类型
注意：转换时不能转成其它有相同父类的子类

判断子类类型是不是某一个类：instanceof
```
if(a instanceof Dog){
	Dog d = (Dog)a;
	d.lookHome();
}else if(a instanceof Cat){
	Cat c = (Cat)a;
	c.catchMouse();
}else{
	System.out.println("没有这个类型");
}
```

为了方便，JDK14有了一个新特性：可以将判断和强转和在一起写：

```
if(a instanceof Dog d){
	d.lookHome();
}
else if(a instanceof Cat c){
	c.catchMouse();
}else{
	System.out.println("没有这个类型");
}

```

强制类型转换可以转换成真正子类的类型，从而调用子类独有的功能
转换类型与真实类型不一致时会报错
转换的时候用instanceof关键字判断

#### 多
### 4.包、final、权限修饰符、代码块
#### 包
包就是文件夹。用来管理各种不同功能的Javva类，方便后期代码维护。
-包名的规则：公司域名反写+包的作用，全部英文小写，简明知意

包名+类名=全类名（全限定名）
top.rippleqaq.Student

使用其他类时候，需要用全类名
```
public class Test{
	public static void main(String[] args){
		top.rippleqaq.Student s = new top.rippleqaq.Student();
	}
}
```
太麻烦，使用import导包
```
import top.rippleqaq.Student
public class Test{
	public static void main(String[] args){
		Student s = new Student();
	}
}
```
使用其他类的规则：
使用同一个包中的类时，不需要导包（默认）
使用java.lang包中的类时，不需要导包
其他情况都需要导包
如果同时要用两个包中的同名类，需要用全类名。

#### final关键字
final 最终的 -> 不可被改变的
可以修饰方法、类、变量

final修饰方法：表明该方法是最终方法，不能被重写
final修饰类：表明该类是最终类，不能被继承
final修饰变量：叫做常量，只能被赋值一次

关于常量：
实际开发中，常量一般作为系统的配置信息，方便维护，提高可读性。
命名规范：
-单个单词：全部大写
-多个单词：全部大写，单词间用下划线隔开

final修饰基本数据类型：数据值不能改变
final修饰引用数据类型：地址值不能改变，对象内部可以改变

#### 权限修饰符

权限修饰符：是用来控制一个成员能够被访问的范围的。
可以修饰成员变量、方法、构造方法、内部类。

权限修饰符有四种作用范围：由小到大（private<空着<protected<public）

![](Java基础上-进阶-photos/截图%202023-11-11%2000-13-48.png)

实际开发中，一般只用private和public
-成员变量私有
-方法公开

特例：如果方法中的代码是抽取其他方法中的共性代码，这个方法也一般私有

#### 代码块
{}
##### 局部代码块
在方法中的一个单独的代码块，可以以前结束变量的生命周期，在过去内存比较小的时候用到，如今用处不是很大了

##### 构造代码块
写在成员位置的代码块，在创建对象是优先于构造方法执行的，可以将多个构造方法中重复的部分写在构造代码块中。现在也被淘汰了，因为一定会被执行，不灵活。

如果要灵活的话可以把重复的部分写在一个构造方法中，其他要用这个部分的构造方法用调用这个构造方法的方式实现

##### 静态代码块
格式：static{}
特点：需要通过static关键字修饰，随着类的加载而加载，自动触发且**只执行一次**
使用场景：在类加载的时候，做一些数据初始化时使用

### 5.抽象类、接口、内部类
#### 抽象类
抽象方法：将子类**共性的**行为（方法）抽取到父类之后。由于每一个子类执行的内容是不一样的，所以在父类中**不能确定具体的方法体**，该方法就可以定义为抽象方法

抽象类：一个类中**存在抽象方法**，那么该类就必须**声明为抽象类**

定义格式：
抽象方法的定义格式：
```
public abstract 返回值类型 方法名(参数列表);
```
抽象类的定义格式：
```
public abstract class 类名{};
```

注意事项：
1.抽象类不能实例化
2.抽象类中不一定有抽象方法，有抽象方法的类一定是抽象类
3.抽象类可以有构造方法
4.抽象类的子类要么重写抽象类的所有抽象方法，要么是抽象类

抽象类和抽象方法的意义
强制子类必须按照某种格式写，方便多人开发

当直接创建顶层父类没有意义，不想让别人直接区创建这种对象时，也可以写成抽象的。

#### 接口
接口就是一种规则，是对行为的抽象

当部分类中需要用到相似的代码，可以定义接口规范

接口的定义和使用
使用关键字interface定义
```
public interface 接口名{}
```

注意事项：
1.接口不能实例化
2.接口和类之间是实现关系，通过implements关键字表示

```
public class 类名 implements 接口名{}
```

3.接口的子类（实现类）要么重写接口中的所有方法，要么是抽象类
4.接口和类之间的实现关系可以但实现，也可以多实现

```
public class 类名 implements 接口名1,接口名2{}
```

5.实现类还可以在继承一个类的同时实现多个接口

```
public class 类名 extends 父类 implements 接口名1,接口名2{}
```

例如：
Swim.java:
```
public interface Swim {  
    public abstract void swim();  
}
```

Animal.Java:
```
public abstract class Animal {  
    private String name;  
    private int age;  
  
    public Animal() {  
    }  
  
    public Animal(String name, int age) {  
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
  
    public abstract void eat();  
}
```

Frog.Java:
```
public class Frog extends Animal implements Swim{  
    public Frog() {  
    }  
  
    public Frog(String name, int age) {  
        super(name, age);  
    }  
  
    @Override  
    public void eat() {  
        System.out.println("青蛙在吃虫子");  
    }  
  
    @Override  
    public void swim() {  
        System.out.println("青蛙在蛙泳");  
    }  
}
```

Dog.Java:
```
public class Dog extends Animal implements Swim{  
  
    public Dog() {  
    }  
  
    public Dog(String name, int age) {  
        super(name, age);  
    }  
  
    @Override  
    public void eat() {  
        System.out.println("狗吃骨头");  
    }  
  
    @Override  
    public void swim() {  
        System.out.println("狗在狗刨");  
    }  
}
```

Rabbit.Java:
```
public class Rabbit extends Animal{  
  
    public Rabbit() {  
    }  
  
    public Rabbit(String name, int age) {  
        super(name, age);  
    }  
  
    @Override  
    public void eat() {  
        System.out.println("兔子在吃胡萝卜");  
    }  
}
```

Test.Java:
```
public class Test {  
    public static void main(String[] args) {  
        Frog f = new Frog("小青",1);  
        System.out.println(f.getName() + ", " + f.getAge());  
        f.eat();  
        f.swim();  
  
        Dog d = new Dog("旺财",4);  
        System.out.println(d.getName() + ", " + d.getAge());  
        d.eat();  
        d.swim();  
  
        Rabbit r = new Rabbit("小白",2);  
        System.out.println(r.getName() + ", " + r.getAge());  
        r.eat();  
    }  
}
```

输出：
```
小青, 1
青蛙在吃虫子
青蛙在蛙泳
旺财, 4
狗吃骨头
狗在狗刨
小白, 2
兔子在吃胡萝卜
```

接口中成员的特点：
-成员变量
	只能是常量
	默认修饰符:public static final （就算不写，Java也会加上）
-成员方法
	JDK7以前：只能定义抽象方法
	默认修饰符:public abstract
-构造方法
	没有构造方法

类和接口的关系：
-类和类之间的关系：
	继承关系，只能单继承，不能多继承，但是可以多层继承
-类和接口的关系：
	实现关系，可以单实现，也可以多实现，还可以在继承一个类的同时实现接口
-接口和接口之间的关系：
	继承关系，可以单继承，可以多继承
	如果实现类实现了最下面的字接口，那么要重写所有的方法


