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


# Math, System, Runtime



## Math

> Math是一个工具类，里面提供的都是对数据进行操作的静态方法

### Methods(public static)

1. `int abs(int n)`
2. `double ceil(double a)`:向上取整
3. `double floor(double a)`: 下取整
4. `int round(float a)`: 四舍五入
5. `int max(int a, int b)`: 获取两个int中的较大值
6. `double pow(double a, double b)`: 返回a的b次幂
7. `double random()`: 返回double的随机值[0,1]



## System

> 工具类，代表程序所在的系统

### Methods(public static)

1. `void exit(int status)`: 终止当前运行的Java虚拟机
2. `long currentTimeMillis()`: 返回当前系统的时间毫秒值(是从1970-1-1 0:0:0开始走到此刻的毫秒值)， 可以用来分析代码性能


## Runtime

> 代表程序所在的运行环境，是第一个单例类


### Methods

1. `public static Runtime getRuntime()`：返回与当前java应用程序关联的运行时对象
2. `public void exit(int status)`: 终止当前运行的虚拟机,status表示状态码，非零状态码表示异常终止
3. `public int availableProcessors()`: 返回Java虚拟机中可用的处理器数。
4. `public long totalMemory()`: 返回Java虚拟机中的内存总量
5. `public long freeMemory()`:返回Java虚拟机中的可用内存
6. `public Process exec(String command)`:启动某个程序，并返回代表该程序的对象
