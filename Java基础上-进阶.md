
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
123
