### 常用的方法

1. length():字符串的长度

   ```java
   String a = "Hello World!";
   System.out.println(a.length());
   ```

   输出结果为11

2. charAt():截取一个字符

   ```java
   String str = new String("Hello World");
   System.out.println(str.charAt(1));
   ```

   输出结果为e

3. getBytes():将字符串变为一个byte数组

   ```java
   String a = "Hello Word";
   byte b[] = a.getBytes();
   System.out.println(new String(b));
   ```

4. getChars():截取多个字符并且由另一个char数组接收

   ```java
   String a = "Hello World";
   char[] b = new char[10];
   a.getChars(0, 5, b, 0);
   System.out.println(b);
   ```

   输出结果为Hello

5. toCharArray():将字符串变为一个char数组

   ```java
   String a = "Hello World";
   char[]b = a.toCharArray();
   System.out.println(b);  
   ```

6. equals()和equalsIgnoreCase()比较两个字符串是否相等，前者区分大小写，后者不区分

   ```java
   String a = "Hello World";
   String b = "hello world";
   System.out.println(a.equals(b));
   System.out.println(a.equalsIgnoreCase(b));  
   ```

7. startsWith()和endsWith()判断字符串是不是以特定的字符开头或结束

   ```java
   String a = "Hello Word";
   System.out.println(a.startsWith("ee"));  
   System.out.println(a.endsWith("ld"));
   ```

8. toUpperCase()和toLowerCase()将字符串转换为大写或小写

   ```java
   String a = "Hello World";
   System.out.println(a.toUpperCase());
   System.out.println(a.toLowerCase());
   ```

9.  concat() 连接两个字符串

   ```java
   String str = new String("Hello World");
   String str1 = " Lee";
   System.out.println(str.concat(str1));
   ```

   输出为“Hello World Lee”l

10. trim():去掉开始与结束的空格

    ```java
    String a = "    Hello World   ";
    System.out.println(a.trim());
    ```

    输出为Hello World

11. substring（）截取字符串

    ```java
    String str = new String("Hello World");
    System.out.println(str.substring(0, 5));//输出为Hello
    System.out.println(str.substring(6));//输出为World
    ```

12. indexOf()和lastIndexOf()前者是查找字符或字符串第一次出现的地方，后者是查找字符或字符串最后一次出现的地方

    ```java
    String a = "Hello World";
    System.out.println(a.indexOf("o"));//输出为4
    System.out.println(a.lastIndexOf("o"));//输出为7
    ```

13. replace()替换

    ```java
    String a = "Hello World";
    String b = "你好";
    System.out.println(a.replace(a, b));//你好
    System.out.println(a.replace(a, "HELLO WORLD"));//HELLO WORLD
    System.out.println(b.replace("你", "大家"));//大家好
    ```

### 注意点

1. **概览**

   * String被声明为final，因此String不可被继承（Integer等包装类也不能被继承）

   * 在Java 8中，String内部使用char数组来存储数据

     ```java
     public final class String
         implements java.io.Serializable, Comparable<String>, CharSequence {
         /** The value is used for character storage. */
         private final char value[];
     }
     ```

   * 在Java 9之后，String类的实现改用byte数组存储字符串，同时使用coder来标识使用了哪种编码

     ```java
     public final class String
         implements java.io.Serializable, Comparable<String>, CharSequence {
         /** The value is used for character storage. */
         private final byte[] value;
     
         /** The identifier of the encoding used to encode the bytes in {@code value}. */
         private final byte coder;
     }
     ```

   *  value 数组被声明为 final，这意味着 value 数组初始化之后就不能再引用其它数组。并且 String 内部没有改变 value 数组的方法，因此可以保证 String 不可变。 

2. String不可变的好处

   * **可以缓存hash值**。因为String的Hash值经常被使用，例如String用于HashMap的key。不可变的特性可以是hash值也不可变，因此只需要进行一次计算就可反复使用
   * **String Pool的需要**。如果一个String对象已经被创建过了，那么就会从String Pool中取得引用。只有String是不可变的，才能使用String Pool
   * **安全性**。String经常被作为参数，String不可变保证参数不可变。
   * **线程安全**。String不可变天生具备线程安全，可以在多个线程中安全的使用

3. String Pool(String常量池)

   * String类是使用频率非常高的一种对象类型，JVM为了提升性能和减少内存开销，避免字符串重复创建，就维护了一块特殊的内存空间，即字符串常量池。由String类私有的维护

   * 两种字符串对象创建方式

     + 采用字面方式赋值，例如：

       ```java
       String str1 = "aaa";
       String str2 = "aaa";
       System.out.println(str1==str2);//true
       ```

       采用字面值的方式创建一个字符串时，JVM首先会区字符串池中查找是否存在“aaa”这个对象，如果不存，则在字符串池中创建“aaa”这个对象，然后将常量池中“aaa”这个对象的引用地址返回给字符串常量str，这样str会指向池中“aaa”这个字符串对象；如果已经存在，则不会创建任何对象，直接将池中“aaa”这个对象的地址返回，赋给字符串常量；

       因此，在上述例子中，结果为true（都指向字符串常量池中的“aaa”对象）

     + 采用new关键字创建一个新的字符串对象，例如：

       ```java
       String str1 = new String("aaa");
       String str2 = new String("aaa");
       System.out.println(str1==str2);//false
       ```

       采用new关键字新建一个字符串对象时，JVM首先在字符串池中查找有没有"aaa"这个字符串对象，如果有，则不在池中再去创建"aaa"这个对象了，直接在堆中创建一个"aaa"字符串对象，然后将堆中的这个"aaa"对象的地址返回赋给引用str3，这样，str3就指向了堆中创建的这个"aaa"字符串对象；如果没有，则首先在字符串池中创建一个"aaa"字符串对象，然后再在堆中创建一个"aaa"字符串对象，然后将堆中这个"aaa"字符串对象的地址返回赋给str3引用，这样，str3指向了堆中创建的这个"aaa"字符串对象。

       在上述例子中，结果为false；因为每次采用new关键字来创建对象时，每次new出来的都是一个新对象。

   * **优缺点**：优点就是避免了相同内容的字符串的创建，节省了内存，节省了创建相同字符串的时间，同时提升了性能；缺点是牺牲了JVM在常量池中遍历对象所需要的时间，但时间成本并不高。

4. String，StringBuffer，StringBuilder

   * 继承结构

     ![img](https://img-blog.csdn.net/20180411092328691?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MTEwMTE3Mw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

   * 区别：

     + 从能否修改方面，String类、值都为final类型，无法被继承，value无法被修改，StringBuilder、StringBuffer都是可以修改的
     + 从效率方面，String效率最低，StringBuilder的效率优于StringBuffer
     + 从线程安全方面，StringBuffer中在用于存放数据的char数组中加入了transient关键字，方法中加上了synchronized关键字，线程安全；String、StringBuilder线程不安全

   * 使用场景：

     + 当处理定长字符串时，建议用String；
     + 当处理变长字符串时，并且是单线程环境时，建议用StringBuilder；
     + 当处理变长字符串时，并且是多线程环境时，建议用StringBuffer。

5. 
