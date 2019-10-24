#### 常用的方法

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

#### 注意点

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

2. 

