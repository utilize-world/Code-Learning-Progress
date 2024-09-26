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


# 为什么还要有新的时间API

> 传统的时间API，设计不够合理，使用不方便，而且都是可变对象，修改后会丢失最开始的时间信息

> 线程不安全，只能精确到毫秒

而新设计的JDK8之后的时间API，设计更好，都是不可变对象，修改会返回新的对象，线程安全，能够精确到毫秒，纳秒


## LocalDate, LocalTime, LocalDateTime

> `LocalDate` 代表本地日期(年月日，星期)

> `LocalTime` 代表本地时间(时分秒，纳秒)

>`LocalDateTime` 代表本地日期，时间(年、月、日、星期、时、分、秒、纳秒)

这三种方法均可以通过调用静态方法`now()`，获取当前时间对应的对象
例如：

    LocalDateTime ldt = LocalDateTime.now();




--------------





    public class LocalDateTimeTest {
        public static void main(String[] args) {
            LocalDate ld = LocalDate.now();
            System.out.println(ld);

            int year = ld.getYear();    //年
            int month = ld.getMonthValue(); //月
            int day = ld.getDayOfMonth(); //日

            //2. 直接修改某个日期，用with系列,每次修改都会返回一个新对象
            LocalDate ld2 = ld.withYear(2077);
            System.out.println(ld2);
            System.out.println(ld);

            //3. 把某个信息加多少，用plus系列，减就用minus系列
            LocalDate ld3 = ld.plusDays(23);
            System.out.println(ld3);

            //4. 获得指定日期的LocalDate对象 public static LocalDate of(int year, int month, int day)
            LocalDate ld4 = LocalDate.of(2024,10,9);
            LocalDate ld5 = LocalDate.of(2024,10,9);
            System.out.println(ld4);

            //5.判断两个日期是否相等，在前还是在后，分别用 equals, isBefore, isAfter
            System.out.println(ld4.equals(ld5));
            System.out.println(ld4.isBefore(ld));
            
            
            //LocalTime，LocalDateTime语法与LocalDate类似，只不过年月日变成了时分秒
            
            
        }
    }


--------------------


    //注意LocalDateTime可以转换成LocalDate和LocalTime,甚至后者可以合并为LocalDateTime
        //public LocalDate toLocalDate()

        LocalDate ldd = LocalDateTime.now().toLocalDate();
        LocalTime ltd = LocalDateTime.now().toLocalTime();
        LocalDateTime ldt = LocalDateTime.of(ldd, ltd);




## ZoneID, ZonedDateTime

> 世界各个国家与地区经度不同，各地区的时间也不同，所以就会划分时区

世界标准时间UTC，我国为UTC+8

ZoneID:代表时区ID，用州名/城市，或者国家/城市，例如Asia/Shanghai



    public class ZoneAPITest {
        public static void main(String[] args) {
            //public static ZoneId SystemDefault 获取系统默认时区

            ZoneId zoneId = ZoneId.systemDefault();
            System.out.println(zoneId);

            // public static Set<String> getAvailableZoneIds(); 获取Java支持的所有时区ID
            System.out.println(ZoneId.getAvailableZoneIds());

            // 把某个时区封装成ZoneId对象
            ZoneId zoneId1 = ZoneId.of("America/New_York");

            //使用ZonedDateTime获得带时区的时间
            //public static ZonedDateTime now(ZoneId zone) 获取某个时区的ZonedDateTime对象
            ZonedDateTime now = ZonedDateTime.now(zoneId1);
            System.out.println(now);

            //ZonedDateTime的相关方法与LocalDateTime用法基本一模一样
            ZonedDateTime.now(Clock.systemUTC()); // 世界标准时间

            ZonedDateTime now2 = ZonedDateTime.now(); // 获得默认时区时间
        }
    }

## Instant 时间线上的某个时刻

> Instant对象可以拿到此刻的时间，即从1970-1-1 0.0.0 开始到此刻的`秒数`以及不够一秒的`纳秒`，更好用，可以替代Date

> 相比与LocalDateTime，Instant关键在于可以获取总秒数


## DataTimeFormatter


> 格式化器，对时间进行格式化和解析


    public static void main(String[] args) {
        // 1. create object
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");

        // 2. format
        LocalDateTime ldt = LocalDateTime.now();
        System.out.println(ldt);

        String rs = formatter.format(ldt);  //use formatter to format
        System.out.println(rs);

        //3. another scheme

        String rs2 = ldt.format(formatter); //use time to format
        System.out.println(rs2);

        //4. 解析时间一般通过LocalDateTime提供的解析方法来解析时间
        String data = "2029-12-12 12:12:12";

        LocalDateTime ldt2 = LocalDateTime.parse(data, formatter);
        System.out.println(ldt2);
    }


## Period and Duration

> Period 用来计算日期间隔(年月日)， Duration(时分秒)

> `Period`只能计算两个`LocalDate`对象的相差

    public static void main(String[] args) {
        // create period obj
        LocalDate start = LocalDate.of(2029, 8, 10);
        LocalDate end = LocalDate.of(2029,10 , 15);

        Period period = Period.between(start, end);

        // using period to get info
        System.out.println(period.getYears());
        System.out.println(period.getMonths());
        System.out.println(period.getDays());


    }

-----------

    public static void main(String[] args) {
        //1. create duration obj
        LocalDateTime start = LocalDateTime.of(2025, 11, 11, 11, 11, 11);
        LocalDateTime end = LocalDateTime.of(2025, 10, 10, 10, 10, 10);
        Duration duration = Duration.between(start, end);
        
        //2. get info
        System.out.println(duration.toDays());
        System.out.println(duration.toHours());
        System.out.println(duration.toMillis());
        System.out.println(duration.toSeconds());
        System.out.println(duration.toMinutes());
    }