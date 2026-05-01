# Lexor Programming Language

Lexor is a strictly-typed, asynchronous-ready programming language designed for clarity, modularity, and expressive logic. It features a unique reverse-assignment system and a streamlined flow control syntax.

## Technical Specifications
- Reverse Assignment: Operations flow from left to right (x + y = z).
- Symmetric Control Flow: Streamlined else() logic for conditional branching.
- Native Asynchrony: Built-in async support for non-blocking execution.
- Saturation Arithmetic: The max operator for automatic cyclic indexing.

---

## Language Reference

### 1. Variables and Types
Lexor requires explicit type declaration for safety and performance.

```lx
[include::system::basic]

lx main() {
    int age = 25;
    string name = "Lexor User";
    var frames = "/", "-", "\\", "|";
}
```

### 2. Reverse Assignment
Mathematical operations flow into the target variable.

```lx
int x = 10;
int y = 20;
int result;

x + y = result; $ Stores 30 in result
```

### 3. The max Operator
Used for automatic reset of counters. When the value exceeds the specified limit, it returns to 0.

```lx
i = i + 1 max 4; $ If i reaches 4, it resets to 0
```

### 4. Control Flow
The else statement can accept conditions or act as a final catch-all.

```lx
if (score == 100) {
    system.out("Perfect");
} 
else (score > 50) {
    system.out("Passed");
} 
else () {
    system.out("Failed");
}
```

### 5. Loops
The for loop iterates based on the integer value provided.

```lx
int i = 5;
for <i> {
    system.out("Looping");
    i - 1;
}
```

### 6. Functions and Concurrency
Functions use the lx keyword. Visibility and execution mode can be modified with pub and async.

```lx
async pub lx fetchData(string url) {
    $ Asynchronous operation
}

lx main() {
    fetchData("https://lexor.dev");
}
```

### 7. Module System
Lexor uses headers to link functions between files.

**helloworld.lxh**
```lx
pub lx hello() {
    system.out("hello world");
}
```

**program.lx**
```lx
[include::helloworld::hello]

lx main() {
    hello();
}
```

---

## Progress Indicator Example
This example demonstrates the use of the carriage return (/r) flag for terminal animations.

```lx
[include::system::basic]
[include::system::time]
[include::system::math]

lx main() {
    var frames = "/", "-", "\\", "|";
    int i = 0;

    while (true) {
        system.out(frames[i], /r);
        system.wait(100, ms);
        i = i + 1 max 4;
    }
}
```
