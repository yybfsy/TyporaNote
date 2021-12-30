## 1.IO流的概述

- IO：输入/输出(Input/Output)
- 流：是一种抽象概念，是对数据传输的总称。也就是说数据在设备间的传输称为流，流的本质是数据传输
- IO流就是用来处理设备间数据传输问题的

   常见的应用：文件复制；文件上传；文件下载

![IO001](https://gitee.com/yybovo/note-images/raw/master/Typora/IO001.png)

## 2.IO流的分类

- 按照数据流向,以内存作为参照物

  - 往内存中去,叫做输入（Input）。或者叫做读(Read)。
  - 从内存中出来，叫做输出(Output)。或者叫做写(Write)。

- 按照数据类型

  - 按照字节的方式读取数据，一次读取1个字节byte，等同于一次读取8个二进制位。

    这种流是万能的，什么类型的文件都可以读取。包括：文本，图片，声音，视频文件等....

    字节输入流；字节输出流

    ​				假设文件file1.txt，采用字节流的话是这样读的：
    ​					a中国bc张三fe
    ​					第一次读：一个字节，正好读到'a'
    ​					第二次读：一个字节，正好读到'中'字符的一半。
    ​					第三次读：一个字节，正好读到'中'字符的另外一半。

  - 按照字符的方式读取数据的，一次读取一个字符，这种流是为了方便读取普通文本文件而存在的，这种流不能读取：图片、声音、视频等文件。只能读取纯文本文件，连word文件都无法读取。

    字符输入流；字符输出流

    假设文件file1.txt，采用字符流的话是这样读的：
    					a中国bc张三fe
    					第一次读：'a'字符（'a'字符在windows系统中占用1个字节。）
    					第二次读：'中'字符（'中'字符在windows系统中占用2个字节。）

    

     那么这两种流都在什么情况下使用呢？

    如果数据通过Window自带的记事本软件打开，我们还可以读懂里面的内容，就使用字符流，否则使用字节流。如果你不知道该使用哪种类型的流，就使用字节流

    

## 3.IO流的四大家族

`java.io.InputStream` 字节输入流

`java.io.OutputStream` 字节输出流

`java.io.Reader `字符输入流

`java.io.Writer` 字符输出流



都是抽象类。(abstract class)

所有的流都实现了：
			`java.io.Closeable`接口，都是可关闭的，都有close()方法。
			流毕竟是一个管道，这个是内存和硬盘之间的通道，用完之后一定要关闭，
			不然会耗费(占用)很多资源。养成好习惯，用完流一定要关闭。

所有的输出流都实现了：
			`java.io.Flushable`接口，都是可刷新的，都有flush()方法。
			养成一个好习惯，输出流在最终输出之后，一定要记得flush()
			刷新一下。这个刷新表示将通道/管道当中剩余未输出的数据
			强行输出完（清空管道！）刷新的作用就是清空管道。
			注意：如果没有flush()可能会导致丢失数据。

<font color=red>注意：在java中只要“类名”以Stream结尾的都是字节流。以“Reader/Writer”结尾的都是字符流。</font>

## 4.java.io包下需要掌握的流

文件专属

- `java.io.FileInputStream`
- `java.io.FileOutputStream`
- `java.io.FileReader`
- `java.io.FileWriter`

转换流（将字节流转换成字符流）

- `java.io.InputStreamReader`
- `java.io.OutputStreamWriter`

缓冲流专属

- `java.io.BufferedReader`
- `java.io.BufferedWriter`
- `java.io.BufferedInputStream`
- `java.io.BufferedOutputStream`

数据流专属

- `java.io.DataInputStream`
- `java.io.DataoutputStream`

标准输出流

- `java.io.PrintWriter`
- `java.io.PrintStream`

对象专属流

- `java.io.ObjectInputStream`
- `java.io.ObjectOutputStream`





`java.io.FileInputStream`（掌握）



|      |                                                              |
| :--: | :----------------------------------------------------------: |
| int  |        `read()`        从此输入流中读取一个数据字节。        |
| int  | `read(byte[] b)`        从此输入流中将最多 `b.length` 个字节的数据读入一个 byte 数组中。 |
| int  | `read(byte[] b,  int off, int len)`       从此输入流中将最多 `len` 个字节的数据读入一个  byte 数组中。 |
| int  | `available]()`        返回下一次对此输入流调用的方法可以不受阻塞地从此输入流读取（或跳过）的估计剩余字节数。 |
| long | `skip(long n)`        从输入流中跳过并丢弃 `n` 个字节的数据。 |

​                                                                                                                                                                    

```java
//文件test
abcdef


import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;

/*
java.io.FileInputStream:
    1、文件字节输入流，万能的，任何类型的文件都可以采用这个流来读。
    2、字节的方式，完成输入的操作，完成读的操作（硬盘---> 内存）
 */
public class FileInputStreamTest01 {
    public static void main(String[] args) {
        FileInputStream fis = null;
        try {
            // 创建文件字节输入流对象
            // 文件路径：D:\作业\IO\test （IDEA会自动把\编程\\，因为java中\表示转义）
            // 以下都是采用了：绝对路径的方式。
            //FileInputStream fis = new FileInputStream("D:\\作业\\IO\\test");
            // 写成这个/也是可以的。
            fis = new FileInputStream("D:/作业/IO/test");

            // 开始读
            int readData = fis.read(); // read()这个方法的返回值是：读取到的“字节”本身。
            System.out.println(readData); //97

            readData = fis.read();
            System.out.println(readData); //98

            readData = fis.read();
            System.out.println(readData); //99

            readData = fis.read();
            System.out.println(readData); //100

            readData = fis.read();
            System.out.println(readData); //101


            // 已经读到文件的末尾了，再读的时候读取不到任何数据，返回-1.
            readData = fis.read();
            System.out.println(readData);//-1

            readData = fis.read();
            System.out.println(readData);//-1

            readData = fis.read();
            System.out.println(readData);//-1

        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            // 在finally语句块当中确保流一定关闭。
            if (fis != null) { // 避免空指针异常！
                // 关闭流的前提是：流不是空。流是null的时候没必要关闭。
                try {
                    fis.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

```java
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;

/*
对第一个程序进行改进。循环方式。

分析这个程序的缺点：
    一次读取一个字节byte，这样内存和硬盘交互太频繁，基本上时间/资源都耗费
    在交互上面了。能不能一次读取多个字节呢？可以。
 */
public class FileInputStreamTest02 {
    public static void main(String[] args) {
        FileInputStream fis = null;
        try {
            fis = new FileInputStream("D:\\course\\JavaProjects\\02-JavaSE\\temp");

            /*while(true) {
                int readData = fis.read();
                if(readData == -1) {
                    break;
                }
                System.out.println(readData);
            }*/

            // 改造while循环
            int readData = 0;
            while((readData = fis.read()) != -1){
                System.out.println(readData);
            }

        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (fis != null) {
                try {
                    fis.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}

```

```java
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;

/*
int read(byte[] b)
    一次最多读取 b.length 个字节。
    减少硬盘和内存的交互，提高程序的执行效率。
    往byte[]数组当中读。
 */
public class FileInputStreamTest03 {
    public static void main(String[] args) {
        FileInputStream fis = null;
        try {
            // 相对路径的话呢？相对路径一定是从当前所在的位置作为起点开始找！
            // IDEA默认的当前路径是哪里？工程Project的根就是IDEA的默认当前路径。
            //fis = new FileInputStream("tempfile3");
            //fis = new FileInputStream("IO/tempfile2");
            //fis = new FileInputStream("IO/src/tempfile3");
            fis = new FileInputStream("IO\\test");

            // 开始读，采用byte数组，一次读取多个字节。最多读取“数组.length”个字节。
            byte[] bytes = new byte[4]; // 准备一个4个长度的byte数组，一次最多读取4个字节。
            // 这个方法的返回值是：读取到的字节数量。（不是字节本身）
            int readCount = fis.read(bytes);
            System.out.println(readCount); // 第一次读到了4个字节。
            // 将字节数组全部转换成字符串
            //System.out.println(new String(bytes)); // abcd
            // 不应该全部都转换，应该是读取了多少个字节，转换多少个。
            //new String(bytes,offset,length) 数组，起始位置，长度
            System.out.println(new String(bytes,0, readCount));

            readCount = fis.read(bytes); // 第二次只能读取到2个字节。
            System.out.println(readCount); // 2
            // 将字节数组全部转换成字符串
            //System.out.println(new String(bytes)); // efcd
            // 不应该全部都转换，应该是读取了多少个字节，转换多少个。
            System.out.println(new String(bytes,0, readCount));

            readCount = fis.read(bytes); // 1个字节都没有读取到返回-1
            System.out.println(readCount); // -1
            
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (fis != null) {
                try {
                    fis.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}

```

```java
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;

/*
最终版，需要掌握。
 */
public class FileInputStreamTest04 {
    public static void main(String[] args) {
        FileInputStream fis = null;
        try {
            fis = new FileInputStream("IO/test");
            // 准备一个byte数组
            byte[] bytes = new byte[4];
            /*while(true){
                int readCount = fis.read(bytes);
                if(readCount == -1){
                    break;
                }
                // 把byte数组转换成字符串，读到多少个转换多少个。
                System.out.print(new String(bytes, 0, readCount));
            }*/

            int readCount = 0;
            while((readCount = fis.read(bytes)) != -1) {
                System.out.print(new String(bytes, 0, readCount));
            }

        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (fis != null) {
                try {
                    fis.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}

```

```java
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;

/*
FileInputStream类的其它常用方法：
    int available()：返回流当中剩余的没有读到的字节数量
    long skip(long n)：跳过几个字节不读。
 */
public class FileInputStreamTest05 {
    public static void main(String[] args) {
        FileInputStream fis = null;
        try {
            fis = new FileInputStream("IO/test");
            System.out.println("总字节数量：" + fis.available());
            // 读1个字节
            //int readByte = fis.read();
            // 还剩下可以读的字节数量是：5
            //System.out.println("剩下多少个字节没有读：" + fis.available());
            // 这个方法有什么用？
            //byte[] bytes = new byte[fis.available()]; // 这种方式不太适合太大的文件，因为byte[]数组不能太大。
            // 不需要循环了。
            // 直接读一次就行了。
            //int readCount = fis.read(bytes); // 6
            //System.out.println(new String(bytes)); // abcdef

            // skip跳过几个字节不读取，这个方法也可能以后会用！
            fis.skip(3);
            System.out.println(fis.read()); //100

        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (fis != null) {
                try {
                    fis.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

​                                

`java.io.FileOutputStream`（掌握）

|      |                                                              |
| :--: | ------------------------------------------------------------ |
| void | `write(byte[] b)`        将 `b.length` 个字节从指定 byte 数组写入此文件输出流中。 |
| void | `write(byte[] b,  int off, int len)`       将指定 byte 数组中从偏移量 `off` 开始的  `len` 个字节写入此文件输出流。 |
| void | `write(int b)`        将指定字节写入此文件输出流。           |



```java
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;

/**
 * 文件字节输出流，负责写。
 * 从内存到硬盘。
 */
public class FileOutputStreamTest01 {
    public static void main(String[] args) {
        FileOutputStream fos = null;
        try {
            // myfile文件不存在的时候会自动新建！
            // 这种方式谨慎使用，这种方式会先将原文件清空，然后重新写入。
            //fos = new FileOutputStream("test");
            //fos = new FileOutputStream("IO/src/com/test");

            // append:true 以追加的方式在文件末尾写入。不会清空原文件内容。
            fos = new FileOutputStream("IO/test", true);
            // 开始写。
            byte[] bytes = {97, 98, 99, 100};
            // 将byte数组全部写出！
            fos.write(bytes); // abcd
            // 将byte数组的一部分写出！
            fos.write(bytes, 0, 2); // 再写出ab

            // 字符串
            String s = "二次元近在眼前，远在天边";
            // 将字符串转换成byte数组。
            byte[] bs = s.getBytes();
            // 写
            fos.write(bs);

            // 写完之后，最后一定要刷新
            fos.flush();
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (fos != null) {
                try {
                    fos.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

​        

使用FileInputStream + FileOutputStream完成文件的拷贝

```java
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;

/*
使用FileInputStream + FileOutputStream完成文件的拷贝。
拷贝的过程应该是一边读，一边写。
使用以上的字节流拷贝文件的时候，文件类型随意，万能的。什么样的文件都能拷贝。
 */
public class copy01 {
    public static void main(String[] args) {
        FileInputStream fis = null;
        FileOutputStream fos = null;
        try {
            // 创建一个输入流对象
            fis = new FileInputStream("D:\\galgame\\316.mp4");
            // 创建一个输出流对象
            fos = new FileOutputStream("D:/316.mp4");

            // 最核心的：一边读，一边写
            byte[] bytes = new byte[1024 * 1024]; // 1MB（一次最多拷贝1MB。）
            int readCount = 0;
            while((readCount = fis.read(bytes)) != -1) {
                fos.write(bytes, 0, readCount);
            }

            // 刷新，输出流最后要刷新
            fos.flush();
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            // 分开try，不要一起try。
            // 一起try的时候，其中一个出现异常，可能会影响到另一个流的关闭。
            if (fos != null) {
                try {
                    fos.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if (fis != null) {
                try {
                    fis.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

​               

`java.io.FileReader`

```java
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;

/*
FileReader：
    文件字符输入流，只能读取普通文本。
    读取文本内容时，比较方便，快捷。
 */
public class FileReaderTest01 {
    public static void main(String[] args) {
        FileReader reader = null;
        try {
            // 创建文件字符输入流
            reader = new FileReader("IO/test");

            //准备一个char数组
            char[] chars = new char[4];
            // 往char数组中读
            reader.read(chars); // 按照字符的方式读取：第一次e，第二次f，第三次 风....
            for(char c : chars) {
                System.out.println(c);
            }

            /*// 开始读
            char[] chars = new char[4]; // 一次读取4个字符
            int readCount = 0;
            while((readCount = reader.read(chars)) != -1) {
                System.out.print(new String(chars,0,readCount));
            }*/
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (reader != null) {
                try {
                    reader.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

  `java.io.FileWriter`

```java
import java.io.FileWriter;
import java.io.IOException;

/*
FileWriter:
    文件字符输出流。写。
    只能输出普通文本。
 */
public class FileWriterTest {
    public static void main(String[] args) {
        FileWriter out = null;
        try {
            // 创建文件字符输出流对象
           // out = new FileWriter("IO/test");

            out = new FileWriter("IO/test", true);

            // 开始写。
            char[] chars = {'二','次','元'};
            out.write(chars);
            out.write(chars,2,1);

            out.write("近在眼前，远在天边");
            // 写出一个换行符。
            out.write("\n");
            out.write("hello world!");

            // 刷新
            out.flush();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (out != null) {
                try {
                    out.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

 使用FileReader FileWriter进行拷贝的话，只能拷贝“普通文本”文件。

```java
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;

/*
使用FileReader FileWriter进行拷贝的话，只能拷贝“普通文本”文件。
 */
public class copy02 {
    public static void main(String[] args) {
        FileReader in = null;
        FileWriter out = null;
        try {
            // 读
            in = new FileReader("IO/src/com/copy01.java");
            // 写
            out = new FileWriter("Copy01.java");

            // 一边读一边写：
            char[] chars = new char[1024 * 512]; // 1MB
            int readCount = 0;
            while((readCount = in.read(chars)) != -1){
                out.write(chars, 0, readCount);
            }

            // 刷新
            out.flush();
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (in != null) {
                try {
                    in.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if (out != null) {
                try {
                    out.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }

    }
}

```

​      

`java.io.BufferedReader`



|        |                                      |
| :----: | :----------------------------------: |
| String | `readLine()`        读取一个文本行。 |



```java
import java.io.BufferedReader;
import java.io.FileReader;

/*
BufferedReader:
    带有缓冲区的字符输入流。
    使用这个流的时候不需要自定义char数组，或者说不需要自定义byte数组。自带缓冲。
 */
public class BufferedReaderTest01 {
    public static void main(String[] args) throws Exception{

        FileReader reader = new FileReader("IO/src/com/copy01.java");
        // 当一个流的构造方法中需要一个流的时候，这个被传进来的流叫做：节点流。
        // 外部负责包装的这个流，叫做：包装流，还有一个名字叫做：处理流。
        // 像当前这个程序来说：FileReader就是一个节点流。BufferedReader就是包装流/处理流。
        BufferedReader br = new BufferedReader(reader);

        // 读一行
        /*String firstLine = br.readLine();
        System.out.println(firstLine);

        String secondLine = br.readLine();
        System.out.println(secondLine);

        String line3 = br.readLine();
        System.out.println(line3);*/

        // br.readLine()方法读取一个文本行，但不带换行符。
        String s = null;
        while((s = br.readLine()) != null){
            //System.out.println(s);
            System.out.print(s);
        }

        // 关闭流
        // 对于包装流来说，只需要关闭最外层流就行，里面的节点流会自动关闭。（可以看源代码。）
        br.close();
    }
}

```

`java.io.InputStreamReader`

```java
import java.io.BufferedReader;
import java.io.FileInputStream;
import java.io.InputStreamReader;

/*
    转换流：InputStreamReader
 */
public class BufferedReaderTest02 {
    public static void main(String[] args) throws Exception{

        /*// 字节流
        FileInputStream in = new FileInputStream("Copy02.java");

        // 通过转换流转换（InputStreamReader将字节流转换成字符流。）
        // in是节点流。reader是包装流。
        InputStreamReader reader = new InputStreamReader(in);

        // 这个构造方法只能传一个字符流。不能传字节流。
        // reader是节点流。br是包装流。
        BufferedReader br = new BufferedReader(reader);*/

        // 合并
        BufferedReader br = new BufferedReader(new InputStreamReader(new FileInputStream("IO/src/com/copy01.java")));

        String line = null;
        while((line = br.readLine()) != null){
            System.out.println(line);
        }

        // 关闭最外层
        br.close();
    }
}

```

​                                                                                                                                           

`java.io.BufferedWriter`  `java.io.OutputStreamWriter`

```java
import java.io.BufferedWriter;
import java.io.FileOutputStream;
import java.io.FileWriter;
import java.io.OutputStreamWriter;

/*
BufferedWriter：带有缓冲的字符输出流。
OutputStreamWriter：转换流
 */
public class BufferedWriterTest {
    public static void main(String[] args) throws Exception{
        // 带有缓冲区的字符输出流
        //BufferedWriter out = new BufferedWriter(new FileWriter("copy"));

        BufferedWriter out = new BufferedWriter(new OutputStreamWriter(new FileOutputStream("copy", true)));
        // 开始写。
        out.write("hello world!");
        out.write("\n");
        out.write("hello kitty!");
        // 刷新
        out.flush();
        // 关闭最外层
        out.close();
    }
}
```

`java.io.DataInputStream`

```java
import java.io.*;
/*
DataInputStream:数据字节输入流。
DataOutputStream写的文件，只能使用DataInputStream去读。并且读的时候你需要提前知道写入的顺序。
读的顺序需要和写的顺序一致。才可以正常取出数据。
 */
public class DataInputStreamTest {
    public static void main(String[] args) {
        DataInputStream dis = null;
        try {
            dis = new DataInputStream(new FileInputStream("data"));
            // 开始读
            byte b = dis.readByte();
            short s = dis.readShort();
            int i = dis.readInt();
            float f = dis.readFloat();
            double d = dis.readDouble();
            boolean sex = dis.readBoolean();
            char c = dis.readChar();

            System.out.println(b);
            System.out.println(s);
            System.out.println(i + 1000);
            System.out.println(f);
            System.out.println(d);
            System.out.println(sex);
            System.out.println(c);

        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (dis != null){
                try {
                    dis.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```



`java.io.DataoutputStream`

```java
import java.io.DataOutputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;

/*
java.io.DataOutputStream：数据专属的流。
这个流可以将数据连同数据的类型一并写入文件。
注意：这个文件不是普通文本文档。（这个文件使用记事本打不开。）
 */
public class DataOutputStreamTest {
    public static void main(String[] args) {
        DataOutputStream dos = null;
        try {
            // 创建数据专属的字节输出流
            dos = new DataOutputStream(new FileOutputStream("data"));
            // 写数据
            byte b = 100;
            short s = 200;
            int i = 300;
            float f = 3.0F;
            double d = 3.14;
            boolean sex = false;
            char c = 'a';
            // 写
            dos.writeByte(b);// 把数据以及数据的类型一并写入到文件当中。
            dos.writeShort(s);
            dos.writeInt(i);
            dos.writeFloat(f);
            dos.writeDouble(d);
            dos.writeBoolean(sex);
            dos.writeChar(c);

            // 刷新
            dos.flush();
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (dos != null){
                try {
                    // 关闭最外层
                    dos.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}

```

`java.io.PrintStream`（掌握）

```java
import java.io.FileOutputStream;
import java.io.PrintStream;

/*
java.io.PrintStream：标准的字节输出流。默认输出到控制台。
 */
public class PrintStreamtest {
    public static void main(String[] args) throws Exception{

        // 联合起来写
        System.out.println("hello world!");

        // 分开写
        PrintStream ps = System.out;
        ps.println("hello zhangsan");
        ps.println("hello lisi");
        ps.println("hello wangwu");

        // 标准输出流不需要手动close()关闭。
        // 可以改变标准输出流的输出方向吗？ 可以
        /*
        // 这些是之前System类使用过的方法和属性。
        System.gc();  运行垃圾回收器。
        System.currentTimeMillis(); 返回以毫秒为单位的当前时间。
        PrintStream ps2 = System.out;
        System.exit(0);  终止当前正在运行的 Java 虚拟机。
        System.arraycopy(....);  从指定源数组中复制一个数组，复制从指定的位置开始，到目标数组的指定位置结束。
         */

        // 标准输出流不再指向控制台，指向“log”文件。
        PrintStream printStream = new PrintStream(new FileOutputStream("log"));
        // 修改输出方向，将输出方向修改到"log"文件。
        System.setOut(printStream);
        // 再输出
        System.out.println("hello world");
        System.out.println("hello kitty");
        System.out.println("hello zhangsan");


    }
}
```

日志记录小案例

```java
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.PrintStream;
import java.text.SimpleDateFormat;
import java.util.Date;

/*
日志工具
 */
public class logger {
    /*
    记录日志的方法。
     */
    public static void log(String msg) {
        try {
            // 指向一个日志文件
            PrintStream out = new PrintStream(new FileOutputStream("IO/log.txt", true));
            // 改变输出方向
            System.setOut(out);
            // 日期当前时间
            Date nowTime = new Date();
            SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss SSS");
            String strTime = sdf.format(nowTime);

            System.out.println(strTime + ": " + msg);
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
    }
}

public class LogTest {
    public static void main(String[] args) {
        //测试工具类是否好用
        logger.log("调用了System类的gc()方法，建议启动垃圾回收");
        logger.log("调用了UserService的doSome()方法");
        logger.log("用户尝试进行登录，验证失败");
        logger.log("我非常喜欢这个记录日志的工具哦！");
    }
}

//2021-10-27 09:03:07 133: 调用了System类的gc()方法，建议启动垃圾回收
//2021-10-27 09:03:07 164: 调用了UserService的doSome()方法
//2021-10-27 09:03:07 164: 用户尝试进行登录，验证失败
//2021-10-27 09:03:07 164: 我非常喜欢这个记录日志的工具哦！
```



序列化和反序列化的定义：

  Java序列化就是指把Java对象转换为字节序列的过程

  Java反序列化就是指把字节序列恢复为Java对象的过程。

![IO002](https://gitee.com/yybovo/note-images/raw/master/Typora/IO002.png)

`java.io.ObjectInputStream`    `java.io.ObjectOutputStream`



<font color=red>参与序列化和反序列化的对象，必须实现Serializable接口。</font>

java语言中是采用什么机制来区分类的？

- 首先通过类名进行比对，如果类名不一样，肯定不是同一个类。
- 如果类名一样，再怎么进行类的区别？靠序列化版本号进行区分。

自动生成序列化版本号有什么缺陷？

- 这种自动生成的序列化版本号缺点是：一旦代码确定之后，不能进行后续的修改，
- 因为只要修改，必然会重新编译，此时会生成全新的序列化版本号，这个时候java
- 虚拟机会认为这是一个全新的类。（这样就不好了！）

总结

<font color=red>凡是一个类实现了Serializable接口，建议给该类提供一个固定不变的序列化版本号。
这样，以后这个类即使代码修改了，但是版本号不变，java虚拟机会认为是同一个类。</font>





```java
import java.io.Serializable;

public class Student implements Serializable {

    // IDEA工具自动生成序列化版本号。
    //private static final long serialVersionUID = -7998917368642754840L;

    // Java虚拟机看到Serializable接口之后，会自动生成一个序列化版本号。
    // 这里没有手动写出来，java虚拟机会默认提供这个序列化版本号。
    // 建议将序列化版本号手动的写出来。不建议自动生成
    private static final long serialVersionUID = 1L; // java虚拟机识别一个类的时候先通过类名，如果类名一致，再通过序列化版本号。

    private int no;
    //private String name;

    // 过了很久，Student这个类源代码改动了。
    // 源代码改动之后，需要重新编译，编译之后生成了全新的字节码文件。
    // 并且class文件再次运行的时候，java虚拟机生成的序列化版本号也会发生相应的改变。
    private int a;

    private String address;

    public Student() {
    }

    public Student(int no, String name) {
        this.no = no;
        //this.name = name;
    }

    public int getNo() {
        return no;
    }

    public void setNo(int no) {
        this.no = no;
    }

    /*public String getName() {
        return name;
    }*/

    /*public void setName(String name) {
        this.name = name;
    }*/

    /*@Override
    public String toString() {
        return "Student{" +
                "no=" + no +
                ", name='" + name + '\'' +
                '}';
    }*/

    @Override
    public String toString() {
        return "Student{" +
                "no=" + no +
                ", age=" + a +
                ", address='" + address + '\'' +
                '}';
    }
}

import bean.Student;
import java.io.FileOutputStream;
import java.io.ObjectOutputStream;

/*
1、java.io.NotSerializableException:
    Student对象不支持序列化！！！！

2、参与序列化和反序列化的对象，必须实现Serializable接口。

3、注意：通过源代码发现，Serializable接口只是一个标志接口：
    public interface Serializable {
    }
    这个接口当中什么代码都没有。
    那么它起到一个什么作用呢？
        起到标识的作用，标志的作用，java虚拟机看到这个类实现了这个接口，可能会对这个类进行特殊待遇。
        Serializable这个标志接口是给java虚拟机参考的，java虚拟机看到这个接口之后，会为该类自动生成
        一个序列化版本号。

4、序列化版本号有什么用呢？
    java.io.InvalidClassException:
        com.bjpowernode.java.bean.Student;
        local class incompatible:
            stream classdesc serialVersionUID = -684255398724514298（十年后）,
            local class serialVersionUID = -3463447116624555755（十年前）

    java语言中是采用什么机制来区分类的？
        第一：首先通过类名进行比对，如果类名不一样，肯定不是同一个类。
        第二：如果类名一样，再怎么进行类的区别？靠序列化版本号进行区分。

    小鹏编写了一个类：com.bjpowernode.java.bean.Student implements Serializable
    胡浪编写了一个类：com.bjpowernode.java.bean.Student implements Serializable
    不同的人编写了同一个类，但“这两个类确实不是同一个类”。这个时候序列化版本就起上作用了。
    对于java虚拟机来说，java虚拟机是可以区分开这两个类的，因为这两个类都实现了Serializable接口，
    都有默认的序列化版本号，他们的序列化版本号不一样。所以区分开了。（这是自动生成序列化版本号的好处）

    请思考？
        这种自动生成序列化版本号有什么缺陷？
            这种自动生成的序列化版本号缺点是：一旦代码确定之后，不能进行后续的修改，
            因为只要修改，必然会重新编译，此时会生成全新的序列化版本号，这个时候java
            虚拟机会认为这是一个全新的类。（这样就不好了！）

    最终结论：
        凡是一个类实现了Serializable接口，建议给该类提供一个固定不变的序列化版本号。
        这样，以后这个类即使代码修改了，但是版本号不变，java虚拟机会认为是同一个类。

 */
public class ObjectOutputStreamTest01 {
    public static void main(String[] args) throws Exception{
        // 创建java对象
        Student s = new Student(1111, "zhangsan");
        // 序列化
        ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("students"));

        // 序列化对象
        oos.writeObject(s);

        // 刷新
        oos.flush();
        // 关闭
        oos.close();
    }
}

import java.io.FileInputStream;
import java.io.ObjectInputStream;

/*
反序列化
 */
public class ObjectInputStreamTest01 {
    public static void main(String[] args) throws Exception{
        ObjectInputStream ois = new ObjectInputStream(new FileInputStream("students"));
        // 开始反序列化，读
        Object obj = ois.readObject();
        // 反序列化回来是一个学生对象，所以会调用学生对象的toString方法。
        System.out.println(obj);
        ois.close();
    }
}

```



一次序列化多个对象



关键字`instanceof` 二元运算符，左边是对象，右边是类；当对象是右边类或子类所创建对象时，返回true；否则，返回false。

关键字`transient` 用来表示一个成员变量不是该对象序列化的一部分。当一个对象被序列化的时候，transient型变量的值不包括在序列化的结果中。而非transient型的变量是被包括进去的。  <font color=red>注意static修饰的静态变量天然就是不可序列化的。</font>

```java
import java.io.Serializable;

public class User implements Serializable {
    private int no;
    // transient关键字表示游离的，不参与序列化。
    private transient String name; // name不参与序列化操作！

    public User() {
    }

    public User(int no, String name) {
        this.no = no;
        this.name = name;
    }

    @Override
    public String toString() {
        return "User{" +
                "no=" + no +
                ", name='" + name + '\'' +
                '}';
    }

    public int getNo() {
        return no;
    }

    public void setNo(int no) {
        this.no = no;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}


import bean.User;


import java.io.FileOutputStream;
import java.io.ObjectOutputStream;
import java.util.ArrayList;
import java.util.List;

/*
一次序列化多个对象呢？
    可以，可以将对象放到集合当中，序列化集合。
提示：
    参与序列化的ArrayList集合以及集合中的元素User都需要实现 java.io.Serializable接口。
 */
public class ObjectOutputStreamTest02 {
    public static void main(String[] args) throws Exception{
        List<User> userList = new ArrayList<>();
        userList.add(new User(1,"zhangsan"));
        userList.add(new User(2, "lisi"));
        userList.add(new User(3, "wangwu"));
        ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("users"));

        // 序列化一个集合，这个集合对象中放了很多其他对象。
        oos.writeObject(userList);

        oos.flush();
        oos.close();
    }
}

import bean.User;

import java.io.FileInputStream;
import java.io.ObjectInputStream;
import java.util.List;

/*
反序列化集合
 */
public class ObjectInputStreamTest02 {
    public static void main(String[] args) throws Exception{
        ObjectInputStream ois = new ObjectInputStream(new FileInputStream("users"));
        /*Object obj = ois.readObject();
        //关键字instanceof 二元运算符，左边是对象，右边是类；当对象是右边类或子类所创建对象时，返回true；否则，返回false。判断obj是否是List集合
        System.out.println(obj instanceof List);*/
        List<User> userList = (List<User>)ois.readObject();
        for(User user : userList){
            System.out.println(user);
        }
        ois.close();
    }
}
```





## 5.java.io.File类

File：它是文件和目录路径名的抽象表示

- 文件和目录是可以通过File封装成对象的
- 对于File而言，其封装的并不是一个真正存在的文件，仅仅是一个路径名而已。它可以是存在的，也可以是不存在的。将来是要通过具体的操作把这个路径的内容转换为具体存在的

| **方法名**                        | **说明**                                                    |
| :-------------------------------- | :---------------------------------------------------------- |
| File(String pathname)             | 通过将给定的路径名字符串转换为抽象路径名来创建新的 File实例 |
| File(String parent, String child) | 从父路径名字符串和子路径名字符串创建新的 File实例           |
| File(File parent, String child)   | 从父抽象路径名和子路径名字符串创建新的 File实例             |

|         |                                                              |
| :------ | ------------------------------------------------------------ |
| boolean | `isDirectory()`        测试此抽象路径名表示的文件是否是一个目录。 |
| boolean | `isFile()`        测试此抽象路径名表示的文件是否是一个标准文件。 |
| boolean | `createNewFile()`        当且仅当不存在具有此抽象路径名指定名称的文件时，不可分地创建一个新的空文件。 |
| boolean | `mkdir()`        创建此抽象路径名指定的目录。                |
| boolean | `mkdirs()`        创建此抽象路径名指定的目录，包括所有必需但不存在的父目录。 |
| boolean | `exists()`        测试此抽象路径名表示的文件或目录是否存在。 |
| String  | `getAbsolutePath()`        返回此抽象路径名的绝对路径名字符串。 |
| String  | `getParent()`        返回此抽象路径名父目录的路径名字符串；如果此路径名没有指定父目录，则返回 `null`。 |
| String  | `getName()`        返回由此抽象路径名表示的文件或目录的名称。 |
| long    | `lastModified()`        返回此抽象路径名表示的文件最后一次被修改的时间 |
| long    | `length()`        返回由此抽象路径名表示的文件的长度。       |
| File[ ] | `listFiles()`        返回一个抽象路径名数组，这些路径名表示此抽象路径名表示的目录中的文件。 |





```java
import java.io.File;

/*
File
    1、File类和四大家族没有关系，所以File类不能完成文件的读和写。
    2、File对象代表什么？
        文件和目录路径名的抽象表示形式。
        C:\Drivers 这是一个File对象
        C:\Drivers\Lan\Realtek\Readme.txt 也是File对象。
        一个File对象有可能对应的是目录，也可能是文件。
        File只是一个路径名的抽象表示形式。
    3、需要掌握File类中常用的方法
 */
public class FileTest01 {
    public static void main(String[] args) throws Exception {
        // 创建一个File对象
        File f1 = new File("D:\\file");

        // 判断是否存在！
        System.out.println(f1.exists());

        // 如果D:\file不存在，则以文件的形式创建出来
        /*if(!f1.exists()) {
            // 以文件形式新建
            f1.createNewFile();
        }*/

        // 如果D:\file不存在，则以目录的形式创建出来
        /*if(!f1.exists()) {
            // 以目录的形式新建。
            f1.mkdir();
        }*/

        // 可以创建多重目录吗？
        File f2 = new File("D:/a/b/c/d/e/f");
        /*if(!f2.exists()) {
            // 多重目录的形式新建。
            f2.mkdirs();
        }*/

        File f3 = new File("D:\\作业\\IO\\test");
        // 获取文件的父路径
        String parentPath = f3.getParent();
        System.out.println(parentPath); //D:\作业\IO
        File parentFile = f3.getParentFile();
        System.out.println("获取绝对路径：" + parentFile.getAbsolutePath());

        File f4 = new File("copy");
        System.out.println("绝对路径：" + f4.getAbsolutePath()); //绝对路径D:\java program\qwq\IO\test

    }
}
```

```java
import java.io.File;
import java.text.SimpleDateFormat;
import java.util.Date;

/*
File类的常用方法
 */
public class FileTest02 {
    public static void main(String[] args) {

        File f1 = new File("D:\\作业\\IO\\test");
        // 获取文件名
        System.out.println("文件名：" + f1.getName());

        // 判断是否是一个目录
        System.out.println(f1.isDirectory()); // false

        // 判断是否是一个文件
        System.out.println(f1.isFile()); // true

        // 获取文件最后一次修改时间
        long haoMiao = f1.lastModified(); // 这个毫秒是从1970年到现在的总毫秒数。
        // 将总毫秒数转换成日期?????
        Date time = new Date(haoMiao);
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss SSS");
        String strTime = sdf.format(time);
        System.out.println(strTime);

        // 获取文件大小
        System.out.println(f1.length()); //216064字节。
    }
}
```

```java
import java.io.File;

/*
File中的listFiles方法。
 */
public class FileTest03 {
    public static void main(String[] args) {
        // File[] listFiles()
        // 获取当前目录下所有的子文件。
        File f = new File("D:\\course\\01-开课");
        File[] files = f.listFiles();
        // foreach
        for(File file : files){
            //System.out.println(file.getAbsolutePath());
            System.out.println(file.getName());
        }
    }
}

```

拷贝文件夹

```java
import java.io.*;

/*
* 拷贝目录
* */
public class CopyAlll {
    public static void main(String[] args) {
        //拷贝源
        File srcFile = new File("D:/lwq");
        //拷贝目标
        File destFile = new File("D:/作业/IO");
        //调用方法拷贝
        copyDir(srcFile,destFile);
    }

    /**
     * 拷贝方法
     * @param srcFile 拷贝源
     * @param destFile 拷贝目标
     */
    private static void copyDir(File srcFile, File destFile) {
        if (srcFile.isFile()){
            //srcFile如果是一个文件的话，递归结束
            //是文件的时候需要拷贝
            //......一边读一边写
            FileInputStream in = null;
            FileOutputStream out = null;
            try {
                // 读这个文件
                // D:\lwq
                in = new FileInputStream(srcFile);
                // 写到这个文件中
                // D:\作业\IO\lwq\...
                String path = (destFile.getAbsolutePath().endsWith("/") ? destFile.getAbsolutePath() : destFile.getAbsolutePath() +"\\")+ srcFile.getAbsolutePath().substring(3);
                out = new FileOutputStream(path);
                byte[] bytes = new byte[1024 * 1024];// 一次复制1MB
                int readCount = 0;
                while ((readCount = in.read(bytes)) != -1){
                    //一边读一边写
                    out.write(bytes,0,readCount);
                }
                out.flush();

            } catch (FileNotFoundException e) {
                e.printStackTrace();
            } catch (IOException e) {
                e.printStackTrace();
            } finally {
                if(in != null){
                    try {
                        in.close();
                    } catch (IOException e) {
                        e.printStackTrace();
                    }
                }
                if (out != null){
                    try {
                        out.close();
                    } catch (IOException e) {
                        e.printStackTrace();
                    }
                }
            }

            return;
        }

        //获取数据源下的子目录
        File[] files = srcFile.listFiles();
        for(File file : files){
            //获取所有文件的（包括目录和文件）绝对路径
            //System.out.println(file.getAbsolutePath());
            if (file.isDirectory()){
                //新建对应的目录
                //System.out.println(file.getAbsolutePath());
                //D:\lwq       源目录
                //D:\lwq\作业\IO\lwq      目标目录
                String srcDir = file.getAbsolutePath();
                //去掉拷贝源目录路径的前三位（好和拷贝目标路径拼接）
                //System.out.println(srcDir.substring(3));
                //三元运算符判断源目录与拷贝目录拼接时是否去掉'/'
                String destDir =(destFile.getAbsolutePath().endsWith("/") ? destFile.getAbsolutePath() : destFile.getAbsolutePath() +"\\")+ srcDir.substring(3);
                //System.out.println(destDir);
                File newFile = new File(destDir);
                //判断拷贝目录是否存在源目录拷贝过来的目录，不存在就新建
                if( !newFile.exists() ){
                    newFile.mkdirs();
                }
            }
            //递归调用
            copyDir(file,destFile);
        }
    }
}

```



## 6.IO + Properties联合使用



IO流：文件的读和写。
Properties:是一个Map集合，key和value都是String类型。

并且当配置文件中的内容格式是：
        key1=value
        key2=value
的时候，我们把这种配置文件叫做属性配置文件。
java规范中有要求：属性配置文件建议以.properties结尾，但这不是必须的。
这种以.properties结尾的文件在java中被称为：属性配置文件。
其中Properties是专门存放属性配置文件内容的一个类。



```properties
userinfo.properties
#建议key和value之间使用=的方式。
#=左边是key，=右边是value
########################在属性配置文件中井号是注释#############################
#属性配置文件的key重复的话，value会自动覆盖！
#password=admin123
#最好不要有空格
data                   =     abc
#不建议使用:
#usernamex:admin

username=yyb
password=123
```

```java
import java.io.FileReader;
import java.util.Properties;

/*
IO+Properties的联合应用。
非常好的一个设计理念：
    以后经常改变的数据，可以单独写到一个文件中，使用程序动态读取。
    将来只需要修改这个文件的内容，java代码不需要改动，不需要重新
    编译，服务器也不需要重启。就可以拿到动态的信息。

    类似于以上机制的这种文件被称为配置文件。
    并且当配置文件中的内容格式是：
        key1=value
        key2=value
    的时候，我们把这种配置文件叫做属性配置文件。

    java规范中有要求：属性配置文件建议以.properties结尾，但这不是必须的。
    这种以.properties结尾的文件在java中被称为：属性配置文件。
    其中Properties是专门存放属性配置文件内容的一个类。
 */
public class IoPropertiesTest {
    public static void main(String[] args) throws Exception{
        /*
        Properties是一个Map集合，key和value都是String类型。
        想将userinfo文件中的数据加载到Properties对象当中。
         */
        // 新建一个输入流对象
        FileReader reader = new FileReader("IO/userinfo");

        // 新建一个Map集合
        Properties pro = new Properties();

        // 调用Properties对象的load方法将文件中的数据加载到Map集合中。
        //load(Reader reader) 按简单的面向行的格式从输入字符流中读取属性列表（键和元素对）。
        pro.load(reader); // 文件中的数据顺着管道加载到Map集合中，其中等号=左边做key，右边做value

        // 通过key来获取value呢？
        //getProperty(String key) 用指定的键在此属性列表中搜索属性。
        String username = pro.getProperty("username");
        System.out.println(username);

        String password = pro.getProperty("password");
        System.out.println(password);

    }
}
```



