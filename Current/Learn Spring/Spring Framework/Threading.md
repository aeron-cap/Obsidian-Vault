- Run multiple tasks simultaneously. Helps performance with time consuming operations (File I/O, network comms, or any background tasks).
1. Extend Thread Class 
2. Implement the Runnable Interface
 ```java
  // class that will run with the main thread
public class MyRunnable implements Runnable{
   
   @Override
   public void run(){
      for (int i = 1; i <= 5; i++) {
         try {
            Thread.sleep(1000); //refers to the current thread
         }
         catch (InterruptedException e) {
            //print error
            System.exit(0); //force exit the program
         }
      }
   }
}

//main.java
MyRunnable myRunnable = new MyRunnable(); //create new object
Thread thread = new Thread(myRunnable);
thread.setDaemon(true); //setDaemon will exit if the main thread exits
thread.start();
```
