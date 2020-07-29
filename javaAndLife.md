# java与生活

## 1.一带而过

### 1-1.Java是怎么执行的

jdk：Java的开发工具

jre：Java的开发环境

jvm：Java虚拟及机



Java程序 XXXX.java

编译出的字节码文件 XXXX.class

### 1-2.package

文件夹 

命名规范

\9. 【强制】包名统一使用**小写**，点分隔符之间有且仅有一个**自然语义的英语单词**。包名统一使 用**单数**形式，但是类名如果有复数含义，类名可以使用复数形式。 正例：应用工具类包名为 com.alibaba.ai.util、类名为 MessageUtils（此规则参考 spring 的框架结构）

### 1-3.第一个程序的讲解

```java
package com.microsof.dome; 
```

 文件位置/定位



快捷键 查询File->Setting->keymap



程序运行 ：Ctrl + Shift + F10

main函数，程序入口点

```java
public static void main(String[] args)
```

快捷输入：	psvm + Enter键

```java
System.out.println() ;
```


快捷输入：	sout + Enter键

```java
System.out.println("sum = " + sum); 
```

快捷输入：	soutv+ Enter键 ： 输出就近的一个对象

### 1-4.注释和文档

单行注释：//

​		快捷键：ctrl + /

段落注释：/* 段落注释*/

​		快捷键：ctrl + shift + /

方法注释：

​		快捷键：/**  + Enter

```java
    /**
     * 该方法传递两个int型参数，用来求和
     * @param number_a 第一个加数
     * @param number_b 第二个加数
     * @return 返回两数之和
     */
    public static int sum(int number_a, int number_b) {
        return number_a + number_b;
    }
```

类注释：

​		快捷键：/**  + Enter

```java
**
 * @author xuanjin
 * @createDate 2020/6/27
 * @version 1.8
 */

public class Main {
	...
}
```

### 2-0.一带而过



### 2-1.字符串演示



自己练习



```java
 	String str_1 = "hello";
    String str_2 = "world";

	System.out.println("str_1 = " + str_1);
    System.out.println("Str_2 = " + str_2);

        System.out.println("Str_1 -> length : " + str_1.length());
```

str.length : 获取字符串长度



### 2-2.字符串结束符

c语言中字符串结束符：\0，但Java中没有

### 2-3.自动类型转换

在java中特有String类，基本不使用char类型

### 2-4.import导包和API文档

导包

import + 包名；

import java.long; // 该包不用导，为其自带的；

如果未导包，则先使用自己包内的对象



### 2-5.java中的数组

静态数组

int[] arr_1 = {1, 2, 3};

int[] arr_2 = new int[];

```java
public class TestArray {
   public static void main(String[] args) {
      // 数组大小
      int size = 10;
      // 定义数组
      double[] myList = new double[size];
      myList[0] = 5.6;
      myList[1] = 4.5;
      myList[2] = 3.3;
      myList[3] = 13.2;
      myList[4] = 4.0;
      myList[5] = 34.33;
      myList[6] = 34.0;
      myList[7] = 45.45;
      myList[8] = 99.993;
      myList[9] = 11123;
      // 计算所有元素的总和
      double total = 0;
      for (int i = 0; i < size; i++) {
         total += myList[i];
      }
      System.out.println("总和为： " + total);
   }
}
```

处理数组

```java
public class TestArray {
   public static void main(String[] args) {
      double[] myList = {1.9, 2.9, 3.4, 3.5};
 
      // 打印所有数组元素
      for (int i = 0; i < myList.length; i++) {
         System.out.println(myList[i] + " ");
      }
      // 计算所有元素的总和
      double total = 0;
      for (int i = 0; i < myList.length; i++) {
         total += myList[i];
      }
      System.out.println("Total is " + total);
      // 查找最大元素
      double max = myList[0];
      for (int i = 1; i < myList.length; i++) {
         if (myList[i] > max) max = myList[i];
      }
      System.out.println("Max is " + max);
   }
}
```

for-each循环

```java
public class TestArray {
   public static void main(String[] args) {
      double[] myList = {1.9, 2.9, 3.4, 3.5};
 
      // 打印所有数组元素
      for (double element: myList) {
         System.out.println(element);
      }
   }
}
```

多维数组

```java
String str[][] = new String[typelength1][typelength2];
int a[][] = new int[2][3];
```

### 2-6.Arrays

java.util.Arrays 类能方便地操作数组，它提供的所有方法都是静态的。

具有以下功能：

- 给数组赋值：通过 fill 方法。
- 对数组排序：通过 sort 方法,按升序。
- 比较数组：通过 equals 方法比较数组中元素值是否相等。
- 查找数组元素：通过 binarySearch 方法能对排序好的数组进行二分查找法操作。

**public static int binarySearch(Object[] a, Object key)**
用二分查找算法在给定数组中搜索给定值的对象(Byte,Int,double等)。数组在调用前必须排序好的。如果查找值包含在数组中，则返回搜索键的索引；否则返回 (-(*插入点*) - 1)。

**public static boolean equals(long[] a, long[] a2)**

 如果两个指定的 long 型数组彼此*相等*，则返回 true。如果两个数组包含相同数量的元素，并且两个数组中的所有相应元素对都是相等的，则认为这两个数组是相等的。换句话说，如果两个数组以相同顺序包含相同的元素，则两个数组是相等的。同样的方法适用于所有的其他基本数据类型（Byte，short，Int等）。

**public static void fill(int[] a, int val)**

 将指定的 int 值分配给指定 int 型数组指定范围中的每个元素。同样的方法适用于所有的其他基本数据类型（Byte，short，Int等）。 

**public static void sort(Object[] a)**

对指定对象数组根据其元素的自然顺序进行升序排列。同样的方法适用于所有的其他基本数据类型（Byte，short，Int等）。

### 2-7函数和方法，方法的重载

java中叫方法



正则表达式



方法的重载：

**一是方法名相同，二是参数个数或参数类型不相同**

```java
public static int sum (int number_1, int number_2) {
	return number_1 + number_2;
}

public static int sum (int number_1, number_2, number_3) {
	return number_1 + number_2 + number_3;
}

public static double sum (double number_1, number_2) {
	return number_1 + number_2;
}
```

### 2-8.规范约束（java）

**参阅阿里巴巴Java开发手册**





##  2.OOP上半部分

### 变换思维

由面向过程POP到面向对象OOP

1.该程序要大众化

2.明确目标

3.不强调过程

### 规划明确目标站在更高层次思考问题

1.计划、规划、设计它

2.当你执行完计划时，达到目标

3.OOP：站在更高层面看待事物

### 类属性

成员变量

成员方法

### OOP封装Geter and Seter

快捷键：Alt + insert  生成Geter abd Seter 方法

```java
public class Dogs {
    // 狗的名字
    private String name;
    // 狗的年龄
    private int age;
    // 狗的种类
    private String variety;
    // 狗的食物
    private String food;

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
        if (age < 0 || age > 30) {
            System.out.println("输入数据不合法，已自动清零！");
        } else {
            this.age = age;
        }
    }

    public String getVariety() {
        return variety;
    }

    public void setVariety(String variety) {
        this.variety = variety;
    }

    public String getFood() {
        return food;
    }

    public void setFood(String food) {
        this.food = food;
    }

    public void eat() {
        System.out.println(name + "在吃" + food);
    }

    public void sleep() {
        System.out.println(name + "在睡觉...");
    }

    public void DogInformation() {
        System.out.println("名字" + "\t" + name);
        System.out.println("年龄" + "\t" + age);
        System.out.println("品种" + "\t" + variety);
        System.out.println("食物" + "\t" + food);

    }

}

```



```java
public class ApplicationRun {
    public static void main(String[] args) {
        Dogs zhangDog = new Dogs();
        zhangDog.setName("Jerry");
        zhangDog.setAge(2);
        zhangDog.setVariety("拉布拉多");
        zhangDog.setFood("狗粮");

        Dogs wangDog = new Dogs();
        wangDog.setName("Tom");
        wangDog.setAge(10);
        wangDog.setVariety("藏獒");
        wangDog.setFood("肉");

        zhangDog.DogInformation();
        zhangDog.sleep();
        System.out.println(zhangDog.getName());
        wangDog.DogInformation();
        wangDog.eat();
    }
}
```



### Lomobk插件， jar导入

File -> Settings -> Plugins -> Lombok

下载jar包,导入jar，File -> New -> Directory 命名为jar，将下载好的jar包拖入这个文件夹

右键点击Add as library...

Settings -> build -> Compiler -> Annotation Processors -> 勾选Enable annotation processing

Build -> rebuild Project

```java
import lombok.Getter;
import lombok.Setter;

@Getter
@Setter  
public class Dogs {
    // 狗的名字
    private String name;
    // 狗的年龄
    private int age;
    // 狗的种类
    private String variety;
    // 狗的食物
    private String food;

    // 对于有特殊要求的，可以单独再写
    public void setAge(int age) {
        if (age < 0 || age > 30) {
            System.out.println("输入数据不合法，已自动清零！");
        } else {
            this.age = age;
        }
    }

    public void eat() {
        System.out.println(name + "在吃" + food);
    }

    public void sleep() {
        System.out.println(name + "在睡觉...");
    }

    public void DogInformation() {
        System.out.println("名字" + "\t" + name);
        System.out.println("年龄" + "\t" + age);
        System.out.println("品种" + "\t" + variety);
        System.out.println("食物" + "\t" + food);

    }

}

```



### toString

快捷键：Alt + Inster 选择toString 生成

也可以使用Lombok生成，

```java
import lombok.Getter;
import lombok.Setter;
import lombok.ToString;

@Getter
@Setter
@ToString
@Date // 此句可以替代@Getter@Setter@ToString@EqualsAndHashCode
public class Dogs {
    // 狗的名字
    private String name;
    // 狗的年龄
    private int age;
    // 狗的种类
    private String variety;
    // 狗的食物
    private String food;

    public void eat() {
        System.out.println(name + "在吃" + food);
    }

    public void sleep() {
        System.out.println(name + "在睡觉...");
    }

    @Override
    public String toString() {
        return "Dogs{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", variety='" + variety + '\'' +
                ", food='" + food + '\'' +
                '}';
    }

}

```

### 构造函数

初始化对象

函数名和类名相同，且没有返回值类型

当有自定义构造函数时，必须同时写出无参构造函数

```java
import lombok.Getter;
import lombok.Setter;
import lombok.ToString;

@Getter
@Setter
@ToString
public class Dogs {
    // 狗的名字
    private String name;
    // 狗的年龄
    private int age;
    // 狗的种类
    private String variety;
    // 狗的食物
    private String food;

    public Dogs() {
    }

    public Dogs(int age) {
        this.age = age;
    }

    public Dogs(String name, int age, String variety, String food) {
        this.name = name;
        this.age = age;
        this.variety = variety;
        this.food = food;
    }

    public void setAge(int age) {
        if (age < 0 || age > 30) {
            System.out.println("输入数据不合法，已自动清零！");
        } else {
            this.age = age;
        }
    }


    public void eat() {
        System.out.println(name + "在吃" + food);
    }

    public void sleep() {
        System.out.println(name + "在睡觉...");
    }

}
```



### 垃圾回收机制

```java
system.gc();  // 手动回收，但在java中可以自动回收，一般不需要人为操作
```

76513

### 静态变量和静态方法 

建立在类的基础之上的，和对象没有关系

``` java
public class Dogs {
    private static String Community = "NanG";

    public static void Injections() {
        System.out.println("所有狗，月底打针！");
    }

    public static String getCommunity() {
        return Community;
    }
}
```

```java
public class ApplicationRun {
    public static void main(String[] args) {

        System.out.println("Dogs.Community = " + Dogs.getCommunity());
      
        Dogs.Injections();
    }
}

```



### static单例设计模式

```java
package com.google.demo;

public class Earth {
    private static Earth earthInstance = new Earth();

    private Earth() {
    }

    public static Earth getEarthInstance() {
        return earthInstance;
    }

    public void hello() {
        System.out.println("hello");
    }
}
```

```java
package com.google.demo;

public class Application {
    public static void main(String[] args) {
        Earth earthInstance = Earth.getEarthInstance();
        earthInstance.hello();
    }
}
```











