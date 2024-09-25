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

# StringBuilder

> StringBuilder 表示可变字符串对象，相当于是一个容器，里面存储的字符串是可以改变的，就是用来操作字符串的。

> 相比于String更适合做字符串的修改操作，效率更高

## Usage

### 构造器

1. `public StringBuilder()`: 创建一个空白的字符串对象，不包含任何内容

2. `public StringBuilder(Stirng str)`: 创建一个指定字符串内容的可变字符串对象

### 方法

1. `public StringBuilder append(any type)`: 添加数据并返回StringBuilder对象本身

2. `public StringBuilder reverse()`:将对象内容反转

3. `public int length()`:返回对象长度

4. `public String toString()`:将StringBuilder类型转换为String


## 为什么不用String而使用StringBuilder

String操作字符串进行频繁修改，非常慢


# StringBuffer

> 和StringBuilder是一模一样的，但是StringBuilder线程不安全，StringBuffer线程安全。所谓线程不安全，就是很多用户一起使用StringBuilder的时候，可能出bug

# StringJoiner

> 使用StringBuilder进行拼接有点麻烦，而StringJoiner和SB类似，其不仅能提高字符串的操作效率，在有些场景下操作字符串更加简洁

## Usage

### 构造器

1. `public StringJoiner(间隔符号)`: 创建一个对象，指定拼接时的间隔符号

2. `public StringJoiner(间隔符号，开始符号，结束符号)`：...

### 方法

1. `public StringJoiner add(内容)`: 添加字符串数据(StringBuilder对象好像也有用)，并返回对象本身

2. `public int length()`:返回对象长度

3. `public String toString`: 返回一个字符串(也就是拼接后的结果)