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

# java.base / java.lang.Object

Object是Java中所有类的祖宗类，所有类的对象都可以直接使用Object类中提供的一些方法


## protected Object clone() 

> 创建并返回此对象的副本，当某个对象调用这个方法时，会复制一个一模一样的新对象返回，这里的克隆实际上还是浅克隆

> 如果要实现深克隆，可以在clone方法中先浅克隆一次，得到了一个浅克隆的对象，再把对象中的引用数据进行克隆，并重新赋值给clone后的对象，最后返回克隆对象，就得到了一个深克隆

> 由于`protected`属性，如果自己定义了一个类，而在主程序类中进行对象创建并调用clone会报错，因为主类不是定义类的子类，而不能使用定义类的对象来调用clone， 所以此时只能在子类中进行重写。(同样自动重写)


> 重写完后，还需对子类进行标记，`implements Cloneable`

> 所谓标记接口就是接口里面什么都没，就是一种规则

    @Override
        protected Object clone() throws CloneNotSupportedException {
            return super.clone();
        }

## 深浅克隆

### 浅克隆

拷贝出的新对象，与原对象中的数据一模一样(引用类型拷贝的仅仅是地址)，
也就是说，源对象改变，复制的对象也会改变

### 深拷贝

对象中的基本类型的数据直接拷贝，字符串数据拷贝的还是地址(字符串常量池)，其他对象会创建新对象，不会拷贝地址


## boolean equals(Object obj)

> 比较两者是否`相等` (默认比较`地址`)(而这也是没有意义的，因为如果要比较地址，我们可以使用`==`,所以其存在意义也是用来重写，直接equals然后再回车自动生成)

    @Override
        public boolean equals(Object o) {
            // 首先判断两者对象是否地址都一样，是的话直接返回true
            if (this == o) return true;
            // 如果传入的对象时null，直接错，如果两者的类型都不一样，直接错，getClass也是object的方法之一
            if (o == null || getClass() != o.getClass()) return false;
            // o不是null，且o一定是学生类型，可以开始比较内容，因为传入时是一个Object类型，所以在这里需要进行强制转换
            Student student = (Student) o;
            return age == student.age && Objects.equals(name, student.name);
        }

## String toString()

> 返回对象的字符串表示形式(使用toS进行重写，因为对象的地址一般不是我们想要的结果，而`print(对象)`通常会默认调用`toString()`方法)
