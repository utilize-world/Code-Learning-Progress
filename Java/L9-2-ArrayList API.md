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


# 集合

> 集合是一种容器，用来存放数据，相比于数组，数组的长度在创建时即固定，如果需要增加删除，则会显得很麻烦。

> 而集合大小可变，在开发中用的更多。

# ArrayList

> 就是一种容器，从两点入手进行学习，第一是创建ArrayList对象，第二则是对其增删改查的方法

## 构造器

    ArrayList();    //创建一个初始容量为10的空列表
    
    ArrayList(int length);  //构造具有指定初始容量的空列表

## 方法

    public boolean add (E e); //将指定元素添加到该集合的末尾


    public void add(int index, E element); //在集合的指定位置插入该元素


    public E get(int index);    //返回指定索引处的元素


    public int size();  //返回集合中元素的个数


    public E remove(int index);     //删除索引处的元素，返回被删除的元素


    public boolean remove(Object o); //删除指定的元素，返回删除是否成功，默认删除第一次出现的对象
    

    public E set(int index, E element); //修改指定索引处的元素，返回被修改的元素


## 使用方法

    ArrayList<E> name = new ArrayList<E> ();
    ArrayList<E> name = new ArrayList<> ()
    //这里E代表类型，比如String，使用这种泛型可以约束这个容器中元素的类型


从集合中遍历数据，删除元素时，要注意最好从末尾开始remove，如果正向的话要注意下标