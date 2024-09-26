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

# Lambda 表达式

> 是JDK8开始新增的一种语法形式，用于简化匿名内部类的代码写法

    (被重写方法的形参列表)->{
        重写方法的方法体
    }

lambda表达式不能简化全部匿名内部类，只能简化函数式接口的匿名内部类

所谓函数式接口，就是一个接口，内部只能有一个方法


        Swimming s = new Swimming(){
    //
    //            @Override
    //            public void swim() {
    //                System.out.println("swim!");
    //            }
    //        };
            Swimming s = () -> {
                System.out.println("swim!");
            };
            s.swim();


将来见到的大部分函数式接口，上面都会有一个@FunctionalInterface 注解


## Lambda表达式的省略规则

1. 参数类型可以省略

2. 如果只有一个参数，参数类型可以省略，()也可以省略

3. 如果方法体只有一行代码，可以不写{}，分号也要省略， 如果是return，return也必须不写