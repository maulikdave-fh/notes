## AtomicReference<T>
1. ```AtomicRefernce(V initialValue)```
2. ```V get()``` - returns the current value of the reference
3. ```void set(V newValue)``` - Sets the value to newValue
4. ```boolean compareAndSet(V expectedValue, V newValue)``` 
- assigns new value if currentValue == expectedValue
- ignores a new value of currentValue != expectedValue

### Example
```
    String oldName = "old name";
    String newName = "new name";
    
    AtomicReference<String> atomicReference = new AtomicReference<>(oldName); 
    
    if (atomicReference.compareAndSet(oldValue, newValue)) {
        System.out.println("New value is " + atomicReference.get());
    } else {
        System.out.println("Nothing changed");
    }
```

## CAS (Compare and Set)
1. ```boolean compareAndSet(V expectedValue, V newValue)``` is available for all atomic classes in ```java.util.concurrent.atomic`` package
2. It compiles into an atomic hardware operation
3. Many other atomic methods are internally implemented using CAS 
