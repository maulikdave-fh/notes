## wait(), notify() and notifyAll()
1. The Object class contains following methods;

```
    public final void wait() throws InterruptedException
    public final void notify()
    public final void notifyAll()
```

2. Every Java Class inherits from the Object Class - we can use any object as a condition variable and a lock (using the ```synchronized``` keyword)

3. ```wait()``` method on a shared object causes the current thread to wait until another thread wakes it up
- In the wait state, the thread is not consuming any CPU

4. Two ways to wake up the waiting thread;
- notify() - Wakes up a single thread waiting on that object. If there are multiple threads are waiting on that object, only one of them is going to be chosen arbitrarily
- notifyAll() - wakes up all the threads waiting on that object

5. To call wait(), notify() or notifyAll() on the object, we need to acquire the monitor of that object (use ```synchronized``` on that object)

## How to Use?
```
    public class MySharedClass {
        private boolean isComplete = false;
        
        // The first thread waits until isComplete is true
        public void waitUntilComplete() {
            synchronized(this) {
                while (!isComplete) {
                    this.wait();    
                }
            }
        }
       
        // Another thread can complete the task and wake up othe thread
        public void complete() {
            synchronized(this) {
                isComplete = true;
                this.notify();
            }
        }
    }    
```

## Back-Pressure on Queue - Practical Use case
Whenever using a queue to decouple multi-threaded components, apply back-pressure and limit the size of the queue 

## Note
Using ReentrantLock and the Condition variable allows more flexibility as the Condition class has methods like ```awaitUninterruptibly()``` and ```awaitUnit(Date deadline)``` which the class Object doesn't have
