# test
chendou's test

sleep(long millis)     //参数为毫秒


sleep(long millis,int nanoseconds)    //第一参数为毫秒，第二个参数为纳秒


sleep相当于让线程睡眠，交出CPU，让CPU去执行其他的任务。


但是有一点要非常注意，sleep方法不会释放锁，也就是说如果当前线程持有对某个对象的锁，则即使调用sleep方法，其他线程也无法访问这个对象。


``` java
public class Test {
     
    private int i = 10;
    private Object object = new Object();
     
    public static void main(String[] args) throws IOException  {
        Test test = new Test();
        MyThread thread1 = test.new MyThread();//实例化线程0
        MyThread thread2 = test.new MyThread();//实例化线程1
        thread1.start();线程0开始执行   start（）方法来自父类Thread
        thread2.start();
    } 
     
     
    class MyThread extends Thread{
        @Override
        public void run() {
            synchronized (object) {
                i++;
                System.out.println("i:"+i);
                try {
                    System.out.println("线程"+Thread.currentThread().getName()+"进入睡眠状态");
                    Thread.currentThread().getName(); //得到当前线程的名字
                   Thread.currentThread().sleep(10000);//让当前线程休息，（则即使调用sleep方法，其他线程也无法访问这个对象。）
                } catch (InterruptedException e) {
                    // TODO: handle exception
                }
                System.out.println("线程"+Thread.currentThread().getName()+"睡眠结束");
                i++;
                System.out.println("i:"+i);
            }
        }
    }
}
```
