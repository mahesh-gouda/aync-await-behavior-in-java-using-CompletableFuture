# aync-await-behavior-in-java-using-CompletableFuture

## Bellow Example shows how we can achive Async await behaviour in java with the help of `CompletableFuture`

```
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.TimeUnit;
public class AsyncAwaitBehaviourInJavaExample{
    public static void main(String[] args) {
       CompletableFuture<String> future = new CompletableFuture<>();
        // Start an asynchronous task in a different function (maybe api call or something, after api call is completed we can mark future object as completed with the response)
        startAsyncTask(future);

        // Perform other tasks while waiting for the update
        System.out.println("Doing something else...");

        // Wait for the result of the CompletableFuture using join()
        String result = future.join();

        // Now, you can safely use the result
        System.out.println("Received: " + result);


        //we can repeat the same to call an different api or to make more asynchronomus operations
        CompletableFuture<String> future2 = new CompletableFuture<>();
        startAsyncTask2(future2);
        String result2 = future2.join();
        System.out.println("Received result 2: " + result2);

       System.out.println("!---- Execuition Completed ----!");
    }

 

    private static void startAsyncTask(CompletableFuture<String> future) {
        // Simulate an asynchronous API call and then update the CompletableFuture
        new Thread(() -> {
            try {
                TimeUnit.SECONDS.sleep(2);
                String apiResponse = "Updated API response";
                future.complete(apiResponse); // Update the CompletableFuture
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }).start();
    }

    private static void startAsyncTask2(CompletableFuture<String> future) {
        // Simulate an asynchronous API call and then update the CompletableFuture
        new Thread(() -> {
            try {
                TimeUnit.SECONDS.sleep(2);
                String apiResponse = "Updated API response 2";
                future.complete(apiResponse); // Update the CompletableFuture
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }).start();
    }
    
}
```


## Explanations 
Here CompletableFuture creates a new CompletableFuture object of type String (can be changed based on requirement)

```CompletableFuture<String> future = new CompletableFuture<>();```  

 A CompletableFuture is a class that represents an asynchronous computation. It can be used to run a task on a separate thread and get notified when the task is completed.

The next line of code, String ```result = future.join()```, gets the result of the asynchronous computation. The join() method blocks the current thread until the computation is completed.
