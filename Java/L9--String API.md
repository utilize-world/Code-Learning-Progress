<link rel="stylesheet" href="style.css">

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

# 包与API

调用别人写好的程序会提高开发效率。

包时分门别类管理程序的

建包的语法:
`package xxxx;`

> 规则
1. 同一包下的程序可以直接访问
2. 访问其他包下的程序需要先`import`,为了方便可以在settings中开启auto import
3. 自己的程序调用java的程序，也需要先导包，比如Scanner等。而java.lang包下可以不用导入，可以直接用。
4. 若访问多个其他包的程序，而程序同名，则需要再类前加上包名，默认只能导入一个程序

## API学习

### 1. `java.lang.String`
> 能对字符串进行处理，非常关键

> 常用String创建对象封装字符串数据的方式
#### 1.1 `String name = "xx";`

此时name就是String 对象

#### 1.2  `String str1 = new String("xxx");` 

调用构造方法得到字符串对象，或者new的时候传入字符数组或者字节数组byte[]。

### 2. String的常用方法

#### 2.1 `public char charAt(int index)`:

返回索引处的字符

#### 2.2 `public int length()`:

返回字符个数

#### 2.3 `public char[] toCharArray()`:

把当前字符串变成字符数组并返回

#### 2.4 `public boolean equals(Object anObject)`:

判断当前字符串与另一个字符串内容是否一样，一样则返回`true`

#### 2.5 `public boolean equalsIgnoreCase(String aString)`:

判断当前字符串与另一个字符串内容是否一样，忽略大小写

#### 2.6 `public String substring(int beginIndex, int endIndex)`:

根据开始索引(包括)和结束索引(不包括)来截取当前字符串，返回新字符串

#### 2.7 `public String substring(int beginIndex)`:

从传入的索引处截取到末尾，得到新的字符串返回

#### 2.8 `public String replace(CharSequence target, CharSequence replacement)`:

使用新值，将字符串中的旧值替换，得到新的字符串

#### 2.9 `public boolean contains(CharSequence s)`

判断字符串中是否包含了某个字符串

#### 2.10 `public boolean startWith(String prefix)`

判断字符串是否以某个字符串内容开头，如果是就返回true

#### 2.11 `public String[] split(String regex)`

把字符串按照某个字符串内容分割，并返回字符串数组回来

注意比较字符串时不能使用 == 来将两个字符串直接比，因为new出来的存储在字符串中的都是地址，得用equals来比。

