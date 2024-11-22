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

# Collections

一个用来操作集合的工具类

        //1. ps <T> boolean addAll(Collection<? super T> c, T...elements): 为集合批量添加数据
        //2. ps <T> void shuffle(List<?> list) 打乱List集合中的元素顺序
        //3. ps <T> void sort(List<?> list) 对List集合中的元素升序排序，如果自定义类型对象，同样需要实现比较规则compareTo
        //3. ps <T> void sort(List<?> list, Comparator<? super T> c) 对List集合中的元素自定排序