# Lexor Programming Language - Full Documentation
**Version:** 1.0.0  
**Author:** [team-fox-real]

## 1. Introduction
Lexor is a strictly-typed, asynchronous-capable programming language. It is characterized by its unique "Reverse-Assignment" logic, saturation-based arithmetic, and a highly modular system architecture.

---

## 2. Standard Modules
Lexor uses a modular system to include core functionalities.

- `[include::system::basic]`: Core I/O operations (input, output).
- `[include::system::time]`: Precision delays and time management.
- `[include::system::math]`: Advanced arithmetic and the `max` operator.
- `[include::system::advance]`: File system management (create, open, close).
- `[include::system::async]`: Concurrency and non-blocking execution.
- `[include::system::calls]`: Low-level kernel interactions and process control.

---

## 3. Data Types
Lexor enforces strict typing to ensure memory safety and predictable execution.


| Type | Description |
| :--- | :--- |
| `int` | Signed 64-bit integer. |
| `string` | UTF-8 character sequence. |
| `var` | Array or list of elements separated by commas. |
| `lx` | Function declaration type. |

---

## 4. Syntax and Formatting
- **Statements:** Every instruction must end with a semicolon `;`.
- **Comments:** Use the `$` symbol for single-line comments.
- **Variable Injection:** To reference a variable's value within a string or function, use angle brackets: `<variable_name>`.
- **Entry Point:** All executable programs must contain an `lx main()` function.

---

## 5. Operators and Logic

### 5.1 Reverse Assignment
Unlike standard languages, Lexor processes mathematical operations from left to right, assigning the result to the final variable in the expression.
```lx
int x = 5;
int y = 10;
int z;
x + y = z; $ z now holds 15
```

### 5.2 Saturation Operator (`max`)
The `max` operator is used for cyclic counters. When a value reaches the limit, it resets to zero.
```lx
i = i + 1 max 4; $ If i + 1 equals 4, i becomes 0
```

---

## 6. Control Flow

### 6.1 Conditionals (`if` / `else`)
The `else` statement is symmetric and can take optional conditions.
```lx
if (condition) {
    $ logic
} else (condition) {
    $ alternative logic
} else () {
    $ catch-all logic
}
```

### 6.2 Loops (`for`)
The `for` loop in Lexor is value-based, iterating as many times as the integer value provided.
```lx
int i = 3;
for <i> {
    system.out("Iteration");
    i - 1;
}
```

---

## 7. Functions and Concurrency
Functions can be modified to change their visibility and execution behavior.

- **Standard:** `lx name() { ... }`
- **Public:** `pub lx name() { ... }` (Accessible from external imports).
- **Asynchronous:** `async lx name() { ... }` (Executes in a non-blocking thread).

---

## 8. File System (system::advance)
Lexor provides direct methods for file manipulation.
```lx
system.create.file("name.txt", "content");
string data = system.open.file("name.txt");
system.close.file("name.txt");
```

---

## 9. System Calls (system::calls)
Used for direct communication with the operating system.
- `system.call.exit();`: Terminates the current process.
- `system.call.process(<name>);`: Invokes an external system process.

---

## 10. Library Development
To create a library, use the `.lxh` (Lexor Header) extension. Functions intended for external use must be marked with the `pub` keyword.

**Example Import:**
`[include::library_name::function_name]`

## 11. Reserved Keywords

The following keywords are reserved by the Lexor compiler. Using these as identifiers for variables, functions, or libraries will result in a Syntax Error.


| Keyword | Category | Description |
| :--- | :--- | :--- |
| `lx` | Declaration | Defines a function or executable block. |
| `main` | Execution | Reserved name for the program entry point. |
| `pub` | Visibility | Marks a function as accessible from external files. |
| `async` | Concurrency | Defines a non-blocking asynchronous function. |
| `int` | Type | Data type for 64-bit integers. |
| `string` | Type | Data type for UTF-8 strings. |
| `var` | Type | Data type for arrays and lists. |
| `if` | Control Flow | Starts a conditional block. |
| `else` | Control Flow | Defines alternative or final conditional branches. |
| `while` | Control Flow | Starts a conditional loop. |
| `for` | Control Flow | Starts a value-based iterator loop. |
| `max` | Operator | Saturation/reset operator for cyclic logic. |
| `ms` | Unit | Time unit for milliseconds (used in system.wait). |
| `s` | Unit | Time unit for seconds (used in system.wait). |
| `/r` | Flag | Output flag for Carriage Return (cursor reset). |
| `system` | Namespace | Root namespace for all built-in modules. |

## 12. Known Limitations

As of the current version, Lexor has the following limitations that developers should consider during implementation:

- **Single-line Comments Only:** Lexor currently only supports single-line comments using the `$ ` symbol. Block comments (multi-line) are not yet implemented.
- **Fixed Array Size:** Variables declared as `var` have a static length once initialized. Dynamic resizing (push/pop) is not supported in the current version.
- **Integer Precision:** The `int` type is strictly 64-bit. Lexor does not currently support floating-point numbers (decimals) or 32-bit integers.
- **Synchronous File I/O:** While the language supports `async lx`, the `system::advance` file operations currently block the thread until the operation is completed.
- **Nested Logic in max:** The `max` operator can only be used in simple assignment expressions and cannot be nested within complex conditional headers.
- **Unit Specificity:** The `system.wait` function only accepts `ms` and `s` as valid time units. Other units must be converted manually by the user.
- **Recursive Depth:** Deep recursion in `lx` functions is limited by the system stack size; there is no tail-call optimization in the current compiler version.
