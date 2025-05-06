## Why we need Thread Coordination?
1. Different threads run independently
2. Order of execution is out of our control

**What if one thread depends on another thread?**
![Threads!](tj1.png)

How thread B would know that thread A is complete and is not accessing some intermediate value / partial result? 

### Naive Solution
Thread B runs in a loop and keeps checking if Thread A's result is ready. But that would burn CPU cycles
```
    void waitForThreadA() {
        while(!threadA.isFinished()) {
            // burns CPU cycles
        }
    }
```
![Threads!](tj2.png)

### Desired Solution
We want Thread B to sleep until Thread A is done. Then Thread B should wake up and carry on with its work based on Thread A's output.
![Threads!](tj3.png)

We can achieve this using - ```Thread.join()```
```public final void join()```
```public final void join(long millis, int nanos)```
```public final void join(long millis)```

```Thread.join()``` can be used
- to run tasks in parallel
- safely and correctly aggregate the results from multiple threads

```
public class JoinDemo {
	public static void main(String... strings) {
		List<Long> inputNumbers = Arrays.asList(100000L, 3435L, 35435L, 2324L, 4656L, 23L, 2435L, 5566L);
		// We want to calculate factorial for each list item. !0, !3435, etc.

		List<FactorialThread> threads = new ArrayList<>();
		for (Long inputNumber : inputNumbers) {
			threads.add(new FactorialThread(inputNumber));
		}

		for (Thread thread : threads) {
		    // Option 1. To stop long running thread when main thread has terminated
			//thread.setDaemon(true);
			thread.start();
		}

		for (Thread thread : threads) {
			try {
				thread.join(2000);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}

		for (int i = 0; i < inputNumbers.size(); i++) {
			FactorialThread thread = threads.get(i);
			if (thread.isFinished()) {
				System.out.println("Factorial of " + inputNumbers.get(i) + " is " + thread.getResult());
			} else {
				System.out.println("Calculation for " + inputNumbers.get(i) + " is still in progress.");
				// Option 2. Interrupt thread so the app can be closed
				thread.interrupt();
			}
		}
	}

	public static class FactorialThread extends Thread {
		private long inputNumber;
		private BigInteger result = BigInteger.ZERO;
		private boolean isFinished = false;

		public FactorialThread(long inputNumber) {
			this.inputNumber = inputNumber;
		}

		@Override
		public void run() {
			this.result = factorial(this.inputNumber);
			this.isFinished = true;
		}

		private BigInteger factorial(long n) {
			BigInteger tempResult = BigInteger.ONE;

			for (long i = n; i > 0; i--) {
				if (this.isInterrupted()) {
					System.out.println("Thread took too long to run. Interrupted.");
					return BigInteger.ZERO;
				}
				tempResult = tempResult.multiply(BigInteger.valueOf(i));
			}
			return tempResult;
		}

		public BigInteger getResult() {
			return result;
		}

		public boolean isFinished() {
			return isFinished;
		}
	}
}

```
