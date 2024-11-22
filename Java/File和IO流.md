<style>
h1 {
    color: aqua;
}
h2{
    color: rgb(0, 181, 201);
}
h3,h4 {
    color: #FF70DB93;
}
</style>

# File

> File是java.io包下的文件，File类的对象，用于代表当前操作系统的文件(既可以是文件，也可以是文件夹)

> File只能对文件本身进行操作，不能读写文件中的存储的数据

IO流可以用来读写文件中的数据，也可以读写网络中的数据

## 创建file对象

使用文件路径时，可以使用File.separator作为`\\`或者`/`分隔符，实现跨平台

> 在记录路径时，最好使用相对路径(从模块名开始找)，可以直接从工程检索，在不同的设备上就不需要重新配置路径了。

        public static void main(String[] args) {
        //1. 创建file对象
        File file = new File("C:\\Users\\12493\\Desktop\\test.txt");
        System.out.println(file.getName());
        long length = file.length();    //获取文件大小
        System.out.println(length);

        // 也可以指代一个路径不存在的文件，此时的length就是0，也可以利用.exists()方法来判断是否存在该文件
        System.out.println(file.exists());

        // isFile判断当前指代对象是否是文件,isDirectory判断当前对象指代是否是文件夹
        System.out.println(file.isFile());

        //getName()获取文件的名称(包含后缀)
        System.out.println(file.getName());

        //public long lastModified() 获取文件的最后修改时间
        long time = file.lastModified();
        DateTimeFormatter dtf = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
        //将毫秒值转换为LocalDateTime
        LocalDateTime ldt = LocalDateTime.ofEpochSecond(time/1000, 0, ZoneOffset.ofHours(8));
        System.out.println(dtf.format(ldt));

        //getPath()获取创建文件对象时，使用的路径(即创建file时的pathname，可能是相对也可能是绝对)
        //getAbsolutePath()获取绝对路径


    }

## file相关操作


     File f1 = new File("C:\\Users\\12493\\Desktop\\FileCreatedTest.txt");
        // 创建文件，如果文件存储，则不会创建，并返回False
        System.out.println(f1.createNewFile());
        // public boolean mkdir(): 用于创建文件夹，然而只能创建1级文件夹
        // public boolean mkdirs(): 用于创建文件夹，可以创建多级文件夹
        // public boolean delete(): 删除文件，或者空文件，不能删除非空文件夹，删除后的文件不会进入回收站


        // public String[] list(), 获取当前目录下所有的“一级文件名称”当一个字符串数组中返回
        // public File[] listFiles(), 获取当前目录下所有一级文件对象到一个文件对象数组中去返回，但是如果没有权限访问该文件，会返回null
        
## 文件搜索(利用递归多级遍历)

利用递归时，要注意三要素，递归的公式，终结点，和递归的方向

如果想要在整个盘符这样大的空间中找到某个程序，

> 先找出盘下所有一级文件对象，遍历全部一级文件对象判断

> 如果是文件夹，则再进去重复过程 


# IO 流

## 字符集

>标准ASCII使用1个字节存储一个字符，首尾是0，总共可表示128个字符

> GBK 汉字编码字符集，包含了2万多汉字字符，一个中文字符编码成两个字节的形式存储，并兼容ASCII字符集

> GBK规定，汉字的第一个字节的第一位必须是1

> Unicode字符集，由国际组织制定，可以容纳世界上的所有文字和符号的字符集

`UTF-8`,采取可变长编码方案，分为四个长度区，1个字节，2个字节，3个字节，4个字节

英文字符和数字占一个字节，汉字占3个字节

然而怎么区分呢？制定了规则，ASCII码可以直接存储，而其他带有2个字节，3字节等其他字符，则需要有一定的规则，例如
3字节要求，  1110xxxx 10xxxxxx 10xxxxxx的格式

在开发时应该使用UTF-8编码！！


## Java代码对字符的编码

byte[] getBytes() 使用默认字符集将String编码为一系列字节，并将结果存储到新的字节数组中

byte[] getBytes(String charsetName) 指定字符集

String(byte[] bytes) 通过使用平台的默认字符集解码指定的字节数组来构造新的String

String(byte[] bytes, String charsetName)


## IO 流


输入流：负责把数据从网络或者硬盘中读到内存区，而输出流负责写数据出去到网络或者磁盘

也就是用来读写数据

IO流可以分为 字节流和字符流

字节流-> 适合操作所有类型的文件，例如音频，视频，图片，文本文件复制等

字符流-> 只适合操作纯文本文件，比如读写txt，java文件等
 

 又可以根据输入流和输出流进一步分

 所以

 字节输入流和字节输出流： `InputStream`和`OutputStream`

 字符输入流和输出流为 `Reader` 和 `Writer`

 注意，这四种都是`抽象类`

 上面对应的实现类是`FileInputStream`和`FileOutputStream`

 下面对应的实现类为 `FileReader`和 `FileWriter`

> FileInputStream 能够从文件中把数据一个字节一个字节读到内存中去 

        InputStream is = new FileInputStream(("oop2\\src\\IOtest.txt"));

        //2.开始读取文件的字节数据,每次读取一个字节返回，如果没有数据，返回-1
       // int b1 = is.read();
     //   System.out.println((char)b1);
        //
        //        int b2 = is.read();
        //        System.out.println((char)b2);

        //3. 使用循环来读取
        //        int b;
        //        while ((b = is.read()) != -1){
        //            System.out.print((char)b);
        //        }
        //        is.close();



        //读取性能很差，应当尽量减少调用硬件资源；而且读取汉字会乱码，因为每次只读取一个字节
        //流使用完毕后必须关闭，释放系统资源

        //也可以用byte[]来存储读取的多个字节，同样，若没有内容也会返回-1

        byte[] buffer = new byte[2];
        int read = is.read(buffer);
        String s = new String(buffer);
        System.out.println(s + "当次读取的字符数" + read);

        // 如果buffer没有读满，再次读取时会覆盖旧内容，但是如果最后如果没有完全覆盖完，就会剩余上次的部分内容在后面,所以可以加上读到哪儿
        int read1 = is.read(buffer);
        String s1 = new String(buffer, 0, read1);
        System.out.println(s1 + "当次读取的字符数"+ read1);

        //以上使用循环来做
       // int len;
      //  while ((len = is.read(buffer))!=-1){
     //       String s2 = new String(buffer, 0, len);
       //     System.out.println(s2);
     //   }
        is.close();


> 而关于输出流 FileOutputStream 可以写字节数据到文件去

其用法和FileInputStream 类似



    OutputStream os = new FileOutputStream("oop2\\src\\IOtest2.txt"); //这里不一定需要文件存在，如果不存在就会新建
        os.write(97);
        os.write('b'); //'b' -> 98
        byte[] bytes = "中国".getBytes();
        os.write(bytes);
        os.close();

> 然而这样操作会清空原文件的内容，再写入新内容，要想追加内容，可以在new FileOutputStream时参数中添加一个true，表示追加


> 复制文件


    String sourcePath = "oop2\\src\\IOtest.txt";
        String desPath = "oop2\\src\\IOtestCopy.txt";

        FileInputStream is = new FileInputStream(sourcePath);
        FileOutputStream os = new FileOutputStream(desPath);

        byte[] buffer = new byte[1024]; // 1KB
        int len;
        while ((len = is.read(buffer))!=-1){
            os.write(buffer, 0, len);
        }
        os.close();
        is.close();


> 字节流非常适合做一切文本的复制操作，任何文件的底层都是字节，字节流做复制，是一字不漏的转移完所有字节，只要复制后的文件格式一致就没问题


## 释放资源

 > 调用close释放资源通常在末尾，然而中间代码若出现异常，系统占用资源不会被释放，就会影响系统性能

> `try-catch-finally`

    try{

    } catch (IOException e) {
        e.printStackTrace();
    } finally{

    }

无论`try`中的程序是否出现异常，最终都会执行`finally`区，`除非JVM终止`.
即使try中有return操作，finally中的代码也会执行。除非try中使用了`System.exit()`

所以finally的作用在于，在程序执行完成后进行资源的释放

可以使用CTRL+alt+T来快速添加这种结构


> `try-with-resource`

    try(定义资源1;定义资源2;...){

    }catch(){

    }

可以自动释放try中定义的资源，也就是使用完后会自动调用close，就不需要finally了


    try (
                FileInputStream is = new FileInputStream(sourcePath);
              FileOutputStream os = new FileOutputStream(desPath);
              ){

            byte[] buffer = new byte[1024]; // 1KB
            int len;
            while ((len = is.read(buffer))!=-1){
                os.write(buffer, 0, len);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }

> 注意try中只能放资源对象，而资源都是会实现一个接口，叫做AutoCloseable接口
，资源都会有一个close方法。所以要想自定义资源，就可以新建实现类来实现AutoCloseable接口

## 字符流

也是通过创建管道来连接源文件

例如FileReader类，就是通过new FileReader(String pathName)来连接

同样也有read()和read(char[] buffer)方法，不过是按字符来读，而不是byte了


FileWriter也是类似，写入字符或者字符串或者字符数组到目标文件中
    
     try (
                Reader rd = new FileReader("oop2\\src\\IOtest2.txt");
                Writer wd = new FileWriter("oop2\\src\\IOtest2.txt",true);
                ){
    //            // 一个个读
    //            int c; //记录每次读取的字符编号,其实就是内容
    //            while((c = rd.read()) != -1){
    //                System.out.print((char)c);
    //            }
                    char[] buffer = new char[3];
                int len;
                while((len = rd.read(buffer))!=-1){
                    System.out.print(new String(buffer, 0, len));
                }
                wd.write('c');
        } catch (IOException e) {
            e.printStackTrace();
        }

不过要注意，字符输出流写出数据后，必须刷新流(flush())或者关闭，否则不会生效


## 缓冲流

BufferedInputStream，BufferedOutputStream等

BufferedReader, BufferedWriter

对原始流进行包装，以提高原始流读写数据的性能


BufferedReader新增了功能，`String readLine()`可以读取一行数据返回，如果没有数据了就返回null

注意调用时，不要用多态写法，因为要使用其本身的新增功能

BufferedWriter也新增了功能，void newLine()可以完成换行


## 不同编码读取出现乱码的问题

如果代码编码和被读取的文本文件的编码是一致的，使用字符流读取文本文件时不会出现乱码

如果不一致，使用字符流就会出现乱码


>InputStreamReader(字符输入转换流)

解决不同编码时，字符流读取文本内容乱码的问题

原理就是先获取文件的原始字节流，再按照真实的字符集编码转换成字符输入流，

    public InputStreamReader(InputStream is, String charset)

>OutputStreamWriter(字符输出转换流)

可以控制写出去的字符是用什么字符集编码

    public OutputStreamWriter(OutputStream os, String charset)


## 打印流

PrintStream(字节)和PrintWriter(字符)

作用是 更方便，更高效的打印数据,然而不能直接加参数作追加，除非在低级流中指定

>构造器

    PrintStream(OutputStream/File/String) 可以通向字节输出流/文件或者文件路径
    PrintStream(String fileName, charset charset) 指定字符编码
    PrintStream(OutputStream out, boolean autoFlush, String encoding) 指定字符编码以及自动刷新

>方法

    void println(Xxx xx) 可以打印任意类型数据
    void write(int/byte[]/byte[]部分) 支持写字节数据出去

### 输出重定向

可以通过System.setOut(PrintStream out)来改变系统默认的打印流(System.out)
经过改变后，之后的system.out语句都将由指定的打印流处理


## 数据流

DataInputStream和DataOutputStream  数据输入流和数据输出流

允许把数据和其类型一同写入或读取

        try (
                DataOutputStream dos =
                        new DataOutputStream(new FileOutputStream("oop2\\src\\IOtest2.txt"));
                DataInputStream dis =
                        new DataInputStream(new FileInputStream("oop2\\src\\IOtest2.txt"));
                ){
            dos.writeInt(97);
            dos.writeBoolean(true);
            dos.writeUTF("ttttest");
        } catch (Exception e) {
            e.printStackTrace();
        }



        try (
                DataInputStream dis =
                        new DataInputStream(new FileInputStream("oop2\\src\\IOtest2.txt"));
        ){
            int i = dis.readInt();
            System.out.println(i);
            boolean b = dis.readBoolean();
            System.out.println(b);
            String s = dis.readUTF();
            System.out.println(s);
        } catch (Exception e) {
            e.printStackTrace();
        }


## 序列化

对对象进行序列化或反序列化，即把对象写入文件或者从文件中读取对象

ObjectInputStream 反序列化，从文件中读取对象

ObjectOutputStream 序列化对象，把Java对象存入某个文件

注意，如果要对某个自定义对象进行序列化，该对象必须实现Serializable接口

     writeObject();
        readObj();
    
    private static void readObj(){
        try (
                ObjectInputStream ois = new ObjectInputStream(new FileInputStream("oop2\\src\\ObjectIOtest.txt"));
        ){

            User u = (User) ois.readObject();
            System.out.println(u);

        } catch (Exception e) {
            e.printStackTrace();
        }
    }


    private static void writeObject() {
        try (
                ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("oop2\\src\\ObjectIOtest.txt"));
                ){
            User u = new User("admin", "yuki", 32, "123456");
            oos.writeObject(u);
            System.out.println("success serialize");

        } catch (Exception e) {
            e.printStackTrace();
        }
    }


如果有些情况下，对象中的内容不希望序列化，则可以在对应的私有变量前加上
`transient`修饰符，这就意味着其不参加序列化

> 如果要一次性序列化多个对象，可以用一个ArrayList集合存储多个对象，然后对集合进行序列化即可，
而且ArrayList已经实现了序列化接口


## IO框架

框架是指解决某类问题，编写的一套类，接口等，半成品

框架的形式，一般是把类，接口等编译成class形式，再压缩成一个.jar结尾的文件发行出去

如Commons-io

使用别人的jar，复制到自己的module目录下， 新建一个lib文件夹并放入jar
，将lib文件夹add as library

Java中也自带，如Files


