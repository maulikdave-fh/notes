## Creating Threads
1. ```Thread``` class encapsulates all thread related functionality
2. Two ways to run code on a new thread
- Implement ```Runnable``` interface, and pass to a new Thread object
- Extend ```Thread``` class and create an object of that class

### Using Runnable
Consider Thread as a worker. Worker would execute tasks. Tasks implement ```Runnable``` interface
```
        Thread worker = new Thread(new Task());
        worker.start();
```

```
        class Task implements Runnable {
            @Override
            public void run() {
                System.out.println(Thread.currentThread().getName());
            }            
        }
```

### Extending Thread class
```
    Thread thread = new TaskThread();
    thread.start();
```

```
    class TaskThread extends Thread {
        @Override
        public void run() {
            System.out.println(this.getName());
        }
    }
```
