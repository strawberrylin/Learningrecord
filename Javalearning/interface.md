# **Java learning---Interface**


## abstract

用来修饰抽象类和抽象方法，有抽象方法的类一定是抽象类，但抽象类不一定有抽象方法。
抽象类不能被实例化，无法通过new来调用构造器来创建一个实例。
抽象类的构造器主要被子类调用。

以下三种情况要定义抽象方法：

	1、类内部有抽象方法
	2、继承一个抽象父类，但没有实现父类的所有方法
	3、实现了一个接口，但没有实现所有的抽象方法
	
抽象类中定义了方法，但没有方法体，由继承的子类实现，这样细节是在子类中，父类并不知道。

## Interface
依靠抽象类实现。是抽象出来的模板，定义了某一批类所需哟遵守的规范。
接口的特点在于将实现和规范分离，让系统的各个组件向接口组合。接口并不关心子类要实现什么，怎么实现。
接口关键字：Interface 接口名 父接口...
接口的内部的变量只能是常量，并且被public static final修饰
接口里的方法被publi abstract 修饰，还可以有默认方法，dafault.

------------------------------------------------------------------------------------------------------

### *Demo*

#### 接口定义

```java 
package cn.strawberry;
/**
 * Created by strawberylin on 2016/4/20.
 */
public interface Output{
    //接口定义的成员变量只能是常量
    int MAX_CACHE_LINE=100;
    //接口定义的普通方法只能是public abstract修饰
    public abstract void out();
    public abstract void getData(String msg);
    //在接口中定义默认方法
    default void print(String... msgs){
        for(String msg : msgs){
            System.out.println(msg);
        }
    }
    default void test(){
        System.out.println("default function");
    }
    static String staticTest(){
        return "function in class";
    }
}
```

#### 接口调用

在另外一个包中调用接口

```java
package cn.lin;

import cn.strawberry.Output;
/**
 * Created by strawberrylin on 2016/4/20.
 */
public class Test {
    public static void main(String[] args) {
        //访问另一个包中的Output接口中的常量
        System.out.println(Output.MAX_CACHE_LINE);
        System.out.println(cn.strawberry.Output.staticTest());
    }
}
```

运行效果截图：

![运行效果](https://raw.githubusercontent.com/strawberrylin/Learningrecord/master/Javalearning/images/interfacetest1.PNG)

---------------------------------------------------------------------------------------------------

#### 接口实现

一个子类可以继承多个父类，用逗号隔开，作为参数  
子类要实现父类的所有抽象方法，除非她也是抽象类

```java
package cn.implementtest;
import cn.strawberry.Output;
/**
 * Created by strawberylin on 2016/4/20.
 */
interface Product {
    int getProduceTime();
}
//让子类Printer 实现Output 和 Product
public class Printer implements Output, Product{
    private String[] printData = new String[MAX_CACHE_LINE];
    //记录需要打印的数目
    private int dataNum = 0;
    public void out(){
        while(dataNum > 0){
            System.out.println("打印机打印："+ printData[0]);
            //把队列前移一位，数目减一
            System.arraycopy(printData,1,printData,0,--dataNum);
        }
    }
    public void getData(String msg) {
        if (dataNum >=MAX_CACHE_LINE) {
            System.out.println("输出队列已满，添加失败");
        }else {
            //添加数据队列，数目加一
            printData[dataNum++] = msg ;
        }
    }
    public int getProduceTime() {
        return 45;
    }
    public static void main(String[] args) {
        //创建一个Printer对象
        Printer o = new Printer();
        o.getData("Hello ,I am coming");
        o.getData("Hi, I am here");
        o.out();
        o.getData("Bye , I am leaving");
        o.print("strawberrlin","帅气","handsome");
        o.test();
    }
}
```

运管效果截图：

[运行效果](https://raw.githubusercontent.com/strawberrylin/Learningrecord/master/Javalearning/images/interfacetest2.PNG)

## Contact

-   [github](https://github.com/strawberrylin)
-   [blog](http://hustwind.cn)

--------------------------------------------------------------------------------------------------

> Written with [StackEdit](https://stackedit.io/).
