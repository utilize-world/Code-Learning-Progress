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

# BigDecimal

> 解决浮点型运算时，结果失真的问题

例如直接使用 0.1+0.2，不一定能得到0.3

## Usage

### 构造器

1. `public BigDecimal (String val)`: 把String转成BigDecimal


### Methods

1. `public static BigDecimal valueOf(double val)` : 把一个double转换成BigDecimal
2. `public BigDecimal add(BigDecimal b)`: 加法
3. ................  `substract(BigDecimal b)`；
4. `multiply(b)`
5. `devide(b)`
6. `divide(另一个BigDecimal对象，精确位数，舍入模式)`:能够控制小数几位的除法

7. `public double doubleValue()`： 将BigDecimal转换为double

如果实在不知道怎么写，就利用提示

ctrl+alt+space