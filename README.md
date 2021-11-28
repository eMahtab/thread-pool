# Thread Pool & ExecutorService

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
            System.out.println("Executing : " + name);
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
Executing : Task 4
Executing : Task 3
Executing : Task 1
Executing : Task 2
Executing : Task 5
Executing : Task 6
Executing : Task 7
Executing : Task 8
Executing : Task 9
Executing : Task 10
```


# References :
1. https://howtodoinjava.com/java/multi-threading/java-thread-pool-executor-example
2. https://www.baeldung.com/java-executor-service-tutorial
