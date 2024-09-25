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


# Date

> 代表系统的当前日期和时间


## Constructor

1. `public Date()`: 创建一个Date对象，代表的是系统当前此刻的日期和时间

2. `public Date(long time)`: 把时间毫秒值转换成Date日期对象

## Methods

1. `public long getTime()`    返回从1970.1.1 0.0.0走到此刻的毫秒数

2. `public void setTime(long time)`   设置日期对象的时间为当前时间毫秒值对应的时间


# SimpleDateFormat

> date的形式不够好看，需要格式化

## Constructor

1. `public SimpleDateFormat(String pattern)`:创建简单日期格式化对象，并封装时间格式


## Methods

1. `public final String format(Date date)`: 将日期格式化成日期/时间字符串

2. `public final String format(Object time)`:将时间毫秒值格式化成日期/时间字符串



        public class SimpleDateFormatTest {
            public static void main(String[] args) throws ParseException {
                Date d = new Date();
                System.out.println(d);

                long time  = d.getTime();
                System.out.println(time);

                SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss EEE a");   //这里面的pattern实际上就指定了格式
                String rs = sdf.format(d);
                String rs2 = sdf.format(time);
                System.out.println(rs);
                System.out.println(rs2);

                System.out.println("-----------------");

                String dateStr = "2024-12-12 12:12:11";
                //创建sdf,指定的时间格式与被解析的时间格式一模一样
                SimpleDateFormat sdf2 = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
                Date d2 = sdf2.parse(dateStr);
                System.out.println(d2);
            }
        }


> 还有一种功能，是将字符串时间解析成日期对象

> 使用`public Date parse(String source)`来实现


# Calendar

> Calendar是一个抽象类，但是可以通过调用其静态方法得到日历对象

> Calendar.getInstance();

> 代表系统此刻时间对应的日历

> 通过它可以单独获取，修改时间中的年、月、日、时、分、秒等


## methods

1. `public static Calendar getInstance()`: 获取当前日历对象
2. `public int get(int field)`: 获取日历中的某个信息
3. `public final Date getTime()`: 获取日期对象
4. `public long getTimeInMillis()`: 获取时间毫秒值
5. `public void set(int field, int value)`:修改日历的某个信息
6. `public void add(int field, int amount)`:为某个信息增加/减少指定的值




        public class CalendarTest {
            public static void main(String[] args) {
                Calendar now = Calendar.getInstance();  //记录时刻信息
                System.out.println(now);

                int year = now.get(Calendar.YEAR); //取日历中的信息，可以直接用Calendar调用其静态变量

                Date date = now.getTime();
                System.out.println(date);

                System.out.println(now.getTimeInMillis());

                now.set(Calendar.MONTH, 9);     //月份从0开始，所以记得减1
                System.out.println(now.get(Calendar.MONTH));

                now.add(Calendar.HOUR_OF_DAY, 10);
                now.add(Calendar.HOUR_OF_DAY, -10);
            }
        }

    
Calendar是可变对象