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

# Stream 流

Stream 流是jdk8开始新增的一套API，可以用于操作集合或者数组的数据

> 优势在于，其结合了Lambda的语法风格来编程，提供了一种更加强大，简单的方式操作数据，代码简洁

就相当于一条流水线，先要将集合与这条流水线连接，并对数据处理，然后再输出处理后的结果

## 获取Stream流

利用集合(`Collection`)自带的stream方法


    Stream<T> stream = names.stream();


然而map无法直接调用`stream`，可以利用`entrySet`方法转换为`Set`然后再利用`stream`

而数组可以借助`Arrays`类提供的`stream`方法，或者`Stream`类本身的`of`方法

## 中间方法

操作完数据后可以继续返回为Stream流，可以继续使用


