
## 面向对象进阶
### 1.static
static表示静态，是Java中的一个修饰符，可以修饰成员方法或者成员变量

修饰成员变量的情况：
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

![[Java基础上-进阶-photos/截图 2023-10-10 21-29-06.png]]










### 2.继承
