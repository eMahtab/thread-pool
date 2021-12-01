# Thread Pool & ExecutorService

A thread pool is a pool threads that can be "reused" to execute tasks, so that each thread may execute more than one task. A thread pool is an alternative to creating a new thread for each task you need to execute.

Creating a new thread comes with a performance overhead compared to **reusing a thread** that is already created. That is why **reusing an existing thread to execute a task can result in a higher total throughput** than creating a new thread per task.

### Why ThreadPool
A thread pool helps mitigate the issue of performance by reducing the number of threads needed and managing their lifecycle.

Essentially, threads are kept in the thread pool until they’re needed, after which they execute the task and return the pool to be reused later. 

# Implementation :
```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
 
class Task implements Runnable {
    private String name;
 
    public Task(String name) {
        this.name = name;
    }
 
    public String getName() {
        return name;
    }
 
    public void run() {
        try {
            Long duration = (long) (Math.random() * 1000);
            System.out.println(Thread.currentThread().getName() + " Executing : " + name);
            Thread.sleep(duration);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}

public class Main 
{
    public static void main(String[] args) 
    {
        ExecutorService executor = Executors.newFixedThreadPool(4);
         
        for (int i = 1; i <= 10; i++) 
        {
            Task task = new Task("Task " + i);
            System.out.println("Created : " + task.getName());
 
            executor.execute(task);
        }
        executor.shutdown();
    }
}


```

## Output :
```
Created : Task 1
Created : Task 2
Created : Task 3
Created : Task 4
Created : Task 5
Created : Task 6
Created : Task 7
Created : Task 8
Created : Task 9
Created : Task 10
pool-1-thread-4 Executing : Task 4
pool-1-thread-2 Executing : Task 2
pool-1-thread-3 Executing : Task 3
pool-1-thread-1 Executing : Task 1
pool-1-thread-4 Executing : Task 5
pool-1-thread-2 Executing : Task 6
pool-1-thread-1 Executing : Task 7
pool-1-thread-1 Executing : Task 8
pool-1-thread-3 Executing : Task 9
pool-1-thread-4 Executing : Task 10
```


# References :
1. https://howtodoinjava.com/java/multi-threading/java-thread-pool-executor-example
2. https://www.baeldung.com/java-executor-service-tutorial
