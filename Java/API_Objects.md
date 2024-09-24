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

# java.base/java.utils.Objects

包含了一些静态方法，是一个工具类，不能被继承

## static boolean equals(Object a, Object b)

> 先作非空判断，再比较两个对象，更加安全，源码如下

        public static boolean equals(Object a, Object b) {
        return (a == b) || (a != null && a.equals(b));
    }


## static boolean isNull(Object obj)

> 判断对象是否为null，为null则true

## static boolean nonNull(Object obj)

> 判断对象是否不为null，不为null返回true

