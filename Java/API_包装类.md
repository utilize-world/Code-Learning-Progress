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

# 包装类

> 就是把基本类型的数据包成对象

int -> Integer

char -> Character

byte -> Byte


例如Integer:

    Integer a = Integer.valueOf(10);


> 然而在Java中存在`自动装箱`机制,可以不需要写以上代码就自动进行转换

    Integer a = 12;

> 当然也存在`自动拆箱`，可以自动把对象类型赋给基本数据类型的变量

    int b = a;

## 有什么用?

> 之前的泛型中不支持基本数据类型，如int，但如果非要添加，则可以使用`Integer`这种包装类，并且之后的`add`都可以是`int`类型，而`get`的对象也可以传给`int`，这就是`自动装箱`和`自动拆箱`


## 包装类提供的有用方法

1. static toString()可以把基本类型数据转换成字符串

        Integer a = 23;
        String rs = Integer.toString(a);
        // a.toString();
        // 还可以直接
        String rs2 = a + "2";
        System.out.println(rs2);


2. static int parseInt(String s)，static Integer valueOf(String s)也可以把字符串变成基本数据类型


        int b = Integer.parseInt(rs2);
        System.out.println(b+1);

        String rs3 = "99.5";

        // System.out.println(Double.parseDouble(rs3)+0.5);
        System.out.println(Double.valueOf(rs3)+0.5);

        //如果转换，字符串必须是数值，而且字符串如果是小数，是不能转换成Integer的