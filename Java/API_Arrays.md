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

# Arrays

> 用来操作数组的工具类

    public static void main(String[] args) {
            int[] arr = {10, 20, 30};
            //1. pbs(public static) String toString(type[] arr): return the content of arr
            System.out.println(Arrays.toString(arr));



            //2. pbs int[] copyOfRange(type[] arr, startIndex, endIndex): copy the array from start(include) to end(exclude)
            System.out.println(Arrays.toString(Arrays.copyOfRange(arr, 0, 2)));



            //3. pbs copyOf(type[] arr, int newLen): copy the arr with designated length, if not full, fill with 0, if overfilled, cut
            System.out.println(Arrays.toString(Arrays.copyOf(arr, 10)));



            //4.pbs setAll(double[] arr, IntToDoubleFunction generator): change the original data into new type data and store
            double[] price = {11.0, 99.8, 110, 2};
            Arrays.setAll(price, new IntToDoubleFunction() {
                @Override
                public double applyAsDouble(int value) {
                    // the value is the index
                    // using BigDecimal to cal is better!!
                    return price[value] * 0.8;
                }
            });
            System.out.println(Arrays.toString(price));



            //5. pbs void sort(type[] arr): sort the arr, ascend default
            Arrays.sort(price);
            System.out.println(Arrays.toString(price));
        }

------

> 如果数组存储的是对象，排序又是怎么排？

> 如果直接排序，则会报错


        Student[] students = new Student[4];

        students[0] = new Student("yuki", 170.8, 23);
        students[1] = new Student("yuyuz", 152, 600);
        students[2] = new Student("haki", 173, 50);
        students[3] = new Student("leimu", 160, 123);

        Arrays.sort(students);  //error


> 所以为了比较，需要自己指定比较规则

1. 让该对象的类实现Comparable接口，重写compareTo方法，并自己指定比较规则

        public class Student implements Comparable<Student>


            @Override
            public int compareTo(Student o) {
            //给sort方法内部进行比较，是this和传入对象比较
            // 约定，如果this大于o，则返回正整数
            // 小于就返回负整数
            // 等于就返回0
            // 按照年龄升序
            if(this.age > o.age){
                return 1;
            }
            else if(this.age < o.age){
                return -1;
            }
            return 0;
        }
            //  还可以直接return this.age - o.age

    
2. 使用sort的额外参数完成：


        Arrays.sort(students, new Comparator<Student>() {
            @Override
            public int compare(Student o1, Student o2) {
                //指定比较规则
                // if o1 > o2, return positive value
                // 要注意数据类型， 还是使用if判断更好
                if (o1.getHeight() > o2.getHeight()){
                    return 1;
                }
                else if (o1.getHeight() < o2.getHeight()){
                    return -1;
                }
                return 0;
                // 还可以return Double.compare(o1.getHeight(), o2.getHeight())，和上面效果一样
            }
        });