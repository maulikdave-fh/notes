## Ways of Inter-thread Comms
### 1. Thread.interrupt()
```mermaid
    sequenceDiagram
        ThreadA -->> ThreadB : Thread.interrupt()
        ThreadB -->> ThreadB : Clean up and Terminate
```
