## ReentrantLock
1. Works just like the ```synchronized``` keyword applied on an object
2. Unlike synchronized lock, Requires explicit locking and unlocking

**synchronized** block
```
    Object lock = new Object();
    Resource resource = new Resource();
    ...
    ...
    public void method() {
        synchronized(lock) { //locked
        ...
        use(resource);
        ...
        } //unlocked
    }
```

Same logic using **ReentrantLock**
```
    Lock lockObj = new ReentrantLock();
    Resource resource = new Resource();
    ...
    ...
    public void method() {
        lockObj.lock();  //explicit locking
        ...
        use(resource);
        ...
        lockObj.unlock(); //explicit unlocking
    }
```

### Disadvantage
If we forget to unlock or a method throws an exception before lockObj.unlock() is called, the lockObj will be locked forever causing bugs and deadlocks.

### Solution Pattern
This pattern allows us to guarantee that the unlock() will be called no matter what - even if there is a return statement in the try block.
```
    Lock lockObj = new ReentrantLock();
    Resource resource = new Resource();
    ...
    ...
    public void method() {
        lockObj.lock();  //explicit locking
        try{ // put critical section in try block
            someOperations(resource);
            return value;
        } finally{ // put unlocking in the finally block
            lockObj.unlock(); //explicit unlocking
        }
    }
```

### Why use ReentrantLock?
For this added complexity we get better control over locks and some advanced operations.
#### 1. Query methods - for testing
- ```getQueuedThreads()``` - returns a list of threads waiting to acquire a lock
- ```getOwner()``` - returns the thread that currently owns the lock
- ```isHeldByCurrentThread()``` - queries if the lock is held by the current thread
- ```isLocked()``` - tells if the lock is held by any thread

#### 2. Control over lock's fairness - this helps avoid thread starvation
Enable lock fairness by ```Lock lockObj = new ReentrantLock(true);```

Note that maintaining fairness may reduce the throughput of the app.

#### 3. lockInterruptibly() Motivation
In following case, calling ```somethread.interrupt()``` will not do anything.
```
    public class SomeThread extends Thread {
        @Override
        public void run() {
            while(true) {
                lockObj.lock(); //if the lock is already acquired by other thread, this will suspend the current thread and not
                                // wake up until the lock is released
                ...
                if (Thread.currentThread().isInterrupted()) {
                    cleanUpAndExit();
                }
            }
        }
    }
```

But instead of calling ```lock()``` if we call ```lockInterruptibly()```, we can get out of the above situation. We have to surround ```lockObj.lockInterruptibly()``` with try-catch and handle InterruptedException.

Here, when we call ```somethread.interrupt()```, the suspended thread will wake up and go to the catch block. Inside the catch block, we can do necessary cleanup and shutdown the thread gracefully.
```
    public class SomeThread extends Thread {
        @Override
        public void run() {
            while(true) {
                try {
                    lockObj.lockInterruptibly(); 
                    ...
                } catch (InterruptedException ex) {
                    cleanUpAndExit();
                }
            }
        }
    }
```

##### Use Cases
1. Watchdog for deadlock detection and recovery
2. Waking up threads to do cleanup and close the application

#### 4. tryLock()
The most powerful feature of the ReentrantLock
1. ```boolean tryLock()```
2. ```boolean tryLock(long timeout, TimeUnit unit)```
- Returns true and acquires a lock if available
- Returns false and doesn't get suspended, if the lock is unavailable

```
    Lock lockObj = new ReentrantLock();
    Resource resource = new Resource();
    ...
    ...
    public void method() {
        if (lockObj.tryLock()) {
            try{ 
                someOperations(resource);
                return value;
            } finally{ 
                lockObj.unlock(); //explicit unlocking
            }
        else {
            // This code will never be blocked even if the lock is not available
            ...
        }
    }
```

##### Notes
1. Under no circumstances does the tryLock() method block
2. Regardless of the state of the lock, it always return immediately

##### Use Cases
1. Real time applications where suspending a thread on a lock() method is unacceptable. Examples; Video/Image processing, High speed /low latency trading systems, User interface applications

## ReentrantReadWriteLock
It is two locks in one - Read Lock and Write Lock.

### Motivation
1. Race Conditions require
- Multiple threads sharing a resource
- At least one thread modifying the resource
2. Solution - Complete mutual exclusion
- Regardless of operation (read/write/both)
- Lock and allow only one thread to critical section

But what if we have a workload that mostly includes reading and very little writing.

**Example**
We need to lock the resource, cache here, when writing.
![Advanced Locking!](images/alock1.png)

But it also blocks multiple threads from reading the cache - this reduces a throughput
![Advanced Locking!](images/alock2.png)

**Synchronized and ReentrantLock do not allow multiple readers to access a shared resource concurrently.** When read operations are predominant or when read operations are not as fast, multiple exclusion of reading threads negatively impacts the performance.

### How to Use?
Only single thread is allowed to have a write lock.
```
    ReentrantReadWriteLock rwLock = new ReentractReadWriteLock();
    Lock readLock = rwLock.readLock();
    Lock writeLock = rwLock.writeLock();
    
    writeLock.lock();
    try {
        modifySharedResources();
    } finally {
        writeLock.unlock();
    }
```
To read, we can use a read lock as below. Multiple threads can acquire the readLock.
```
    ReentrantReadWriteLock rwLock = new ReentractReadWriteLock();
    Lock readLock = rwLock.readLock();
    Lock writeLock = rwLock.writeLock();
    
    readLock.lock();
    try {
        readFromSharedResources();
    } finally {
        readLock.unlock();
    }
```

There is a mutual exclusion between reader and writers. 
- **If a write lock is acquired, no thread can acquire a read lock**
- **If at least one thread is holding a read lock, no thread can acquire a write lock**

**Use ReentrantReadWriteLock only for read heavy jobs**.



