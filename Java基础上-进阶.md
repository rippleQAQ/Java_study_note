
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




#### 1.自己设计







#### 2.用别人的