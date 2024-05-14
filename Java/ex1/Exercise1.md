![alt text](exercise1.png)
> Java implementation
   

    package dailyEx;/*
    @Create 2024/5/14
    @Author Wang
    给定一个整数x,如果x是回文,打印 True,否则返回 False
    所谓回文,就是正过来反过来都一样的整数。如121
    */
    import java.util.Scanner;

    import java.util.ArrayList;

    public class ex1 {
        public static void main(String[] args) {
            Scanner sc = new Scanner(System.in);
            System.out.println("input an integer");
            int x = sc.nextInt();
            ex1 test = new ex1();
            boolean result = test.judge(x);
            System.out.println(result);
        }

        public boolean judge(int x){
            boolean flag = false;
            ArrayList<Integer> list = new ArrayList<Integer>();
            int temp = 0;
            int temp_x = x;
            int ac = 0;
            for (;temp_x / 10 !=0; temp_x = temp_x / 10) {
                ac = temp_x % 10;
                list.add(ac);
                temp += ac;
                temp *= 10;

            }
            list.add(temp_x);
            temp += temp_x;
            if (temp==x){
                flag = true;

            }
            System.out.println(temp);
            System.out.println(list);

            return  flag;
        }
    }


