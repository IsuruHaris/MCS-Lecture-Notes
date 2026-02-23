---

---

# Object Names and Variables

## Names (Identifiers)

Names are **labels** used to refer to entities in a program (like variables, functions, types). Instead of remembering memory addresses, we use meaningful names such as `userAge` or `totalSalary`.

### Key Design Questions

* What characters are allowed?
* Is the language case-sensitive?
* Is there a maximum length?
* Are reserved words allowed as names?

---

## Variables

A **variable** is a **named storage location** in memory.

```
Name: count
Value: 10
Address: (memory location)
```

### Main Attributes of a Variable

1. **Name** – Identifier of the variable
2. **Type** – Kind of data it holds (int, float, string, etc.)
3. **Address** – Memory location
4. **Value** – Current stored data
5. **Lifetime** – When it exists in memory
6. **Scope** – Where it can be accessed

### Binding

Binding means attaching attributes to a variable.
Example: `int score = 100;`

* `score` → bound to a memory location
* Type → `int`
* Initial value → `100`

Some bindings happen at compile time (static), others during execution (dynamic).

### Type Checking & Compatibility

* **Type checking** ensures operations match variable types.
* **Compatibility** decides if one type can be assigned to another.

  * `int → float` ✔
  * `string → int` ✖ (without conversion)

### Declaration vs Initialization

* **Declaration:** Introduces the variable (`int x;`)
* **Initialization:** Assigns first value (`int x = 5;`)

**Key Idea:** A variable is a **named, typed memory location**.

---

---

# Why Names?

Names make programs readable and maintainable by acting as **human-friendly references** to program elements.

## What Can Be Named?

* **Variables** (`count`)
* **Parameters** (`radius`)
* **Functions** (`calculateTotal()`)
* **Types** (`Person`)
* **Constants** (`MAX_USERS`)
* **Exceptions, labels, operators, literals**, etc.

---

# Simple vs Composite Names

### Simple Name

Refers directly to an entity.
Example: `a`, `total`

### Composite Name

Refers to a part of a structure using a selector.

Examples:

* `a[1]` → element of an array
* `user.name` → object property

Structure:

```
SimpleName + Selector
```

---

# Names: Compile Time vs Runtime

### Compiled Languages (C, C++)

* Names mainly exist at **compile time**.
* At runtime, programs use memory addresses.
* Debug mode may keep names.

### Interpreted Languages (Python, JavaScript)

* Names are stored and managed **during runtime**.
* Interpreter maintains name-to-value mappings.

---

# Naming Considerations

When naming entities, consider:

1. **Syntax rules** (allowed characters, case sensitivity)
2. **Conventions** (camelCase, snake_case, etc.)
3. **Meaning** (use descriptive names)
4. **Scope** (where it’s visible)
5. **Lifetime** (how long it exists)
6. **Binding time** (when name connects to entity)

Good naming improves readability and maintainability.

---

---

# Primary Design Issues for Names

Language designers decide:

1. **Maximum Length** – Modern languages allow long, descriptive names.
2. **Case Sensitivity** –

   * Case-sensitive: `count` ≠ `Count` (C, Java, Python)
   * Increases flexibility but may cause confusion.
3. **Reserved Words** – Keywords like `if`, `while` cannot be used as identifiers.
4. **Allowed Characters** – Letters, digits, underscores, etc.

---

## Naming Conventions

Common styles:

* **snake_case** → `total_price`
* **camelCase** → `totalPrice`
* **PascalCase** → `TotalPrice`
* **UPPER_SNAKE_CASE** → `MAX_SIZE`

Always follow the language/project convention.

---

## Namespaces

A **namespace** groups names and prevents conflicts.

Example:

* `Car.model`
* `Bike.model`

Each context (file, class, module) acts as a namespace.
Fully qualified names specify exact location (like file paths).

Namespaces allow reuse of common names like `count` safely.

---

---

# Variables: Need and Attributes

## Why Variables?

1. Provide readable access to memory
2. Store results for reuse
3. Transfer data between program parts (parameters, globals)

---

## What Is a Variable?

A variable is an **identifier bound to a value**.

In imperative languages, it represents a memory cell.
In functional languages, it often represents an immutable value.

---

## Core Attributes

1. **Name**
2. **Type**
3. **Address**
4. **Value**
5. **Lifetime**
6. **Scope**

Example:

```c
int globalCount = 100;

void myFunction() {
    int localTemp = 50;
}
```

* `globalCount` → exists entire program (global scope)
* `localTemp` → exists only inside function

Understanding scope and lifetime prevents common bugs.

---

---

# Names, Aliases, and Unions

## Aliasing

**Aliasing** occurs when multiple names refer to the **same memory location**.

If `score` and `points` are aliases:

* Changing one changes the other.

### Problem with Aliasing

It introduces hidden dependencies.
Changing execution order can change results because variables share storage.

---

## Unions (C Language)

A **union** is a structure where all members share the same memory.

```c
union Data {
    int i;
    float f;
    char c;
};
```

* Size = size of largest member
* Writing to one member overwrites others

### Uses

* Memory efficiency
* Low-level data manipulation
* Variant data representation

### Risk

* Programmer must track active member
* Reading inactive member gives garbage
* Reduces type safety

**Key Idea:** Aliasing and unions are powerful but risky. Use carefully.

---

---

# Addresses, Types, and Values of Variables

## Addresses of Variables

A variable’s **address** is its memory location.
However, the same variable name can refer to **different addresses** depending on scope or execution time.

### 1. Same Name, Different Scope

```c
void functionA() {
    int count = 5;
}

void functionB() {
    int count = 10;
}
```

Both use `count`, but they are **different variables** stored at different memory locations.

### 2. Recursive Calls (Different Times)

Each recursive call creates a **new set of local variables** at new memory addresses.

```python
def factorial(n):
    if n == 1:
        return 1
    result = n * factorial(n - 1)
    return result
```

Every call has its own `n` and `result` in separate memory locations.

**Key Idea:** The **name stays the same**, but the **address can change** across scopes or calls.

---

## Type of Variables

The **type** defines:

1. What values a variable can hold
2. What operations are allowed

Examples:

* `int` → whole numbers, arithmetic allowed
* `float` → decimals
* `string` → text operations
* `boolean` → true/false

Types prevent invalid operations and help allocate correct memory.

---

## Value of Variables

The **value** is the actual data stored in memory.

### 1. Primitive Types (Direct Value)

For simple types (int, float, boolean), the variable stores the **actual value**.

```
int age = 30;
```

The memory cell directly contains `30`.

### 2. Reference Types (Address of Data)

For arrays/objects, the variable stores a **reference (address)** to where the real data lives.

```
let grades = [90, 85, 77];
```

`grades` holds a pointer to the array in memory.

If:

```
let backup = grades;
backup[0] = 100;
```

Both variables refer to the same array, so changes affect both.

### Special Reference: `null`

A reference variable can hold `null` (no object).
Using it before assigning a real object causes errors.

**Key Idea:**

* Primitive → stores the value itself
* Reference → stores the address of the value

---

---

# Variable Interpolation

## What Is Variable Interpolation?

Variable interpolation is when a language **automatically replaces a variable inside a string with its value**.

Example (PHP):

```php
$name = "someone";
print "Hello $name";
```

Output:

```
Hello someone
```

The variable inside the string is replaced automatically.

---

## Quotes Matter (PHP Example)

```php
print "Hello $name";   // Interpolation works
print 'Hello $name';   // No interpolation
print 'Hello ' . $name; // Manual concatenation
```

* **Double quotes (`"`)** → Variables are replaced
* **Single quotes (`'`)** → Treated as literal text

Other languages have different syntax (e.g., JavaScript uses backticks).

**Key Idea:** Interpolation is syntactic sugar for building dynamic strings more easily.

---

---

# L-Values, R-Values, and Dereferencing

## L-Value vs R-Value

In assignment:

```
X := X + 1
```

* **Left X (L-value)** → Address (where to store result)
* **Right X (R-value)** → Current value (used in calculation)

Process:

1. Get X’s value
2. Add 1
3. Store result back at X’s address

This is why the statement is not contradictory.

---

## Dereferencing

**Dereferencing** means getting the value stored at an address.

In most languages:

```c
int x = 5;
x = x + 1;   // Dereferencing happens automatically
```

With pointers (C example):

```c
int *x;
*x = 5;
*x = *x + 1;   // *x means dereference
```

**Key Idea:**

* L-value → location
* R-value → content
* Dereferencing → accessing the content via its address

---

---

# Scope of Variables

## What Is Scope?

**Scope** is the region of code where a variable can be accessed.

If used outside its scope → error.

---

## Types of Scope

### 1. Global Variables

* Declared outside functions
* Accessible everywhere
* Use carefully

### 2. Local Variables

* Declared inside a function/block
* Accessible only there

```python
def calculate():
    rate = 0.15  # Local variable
```

### 3. Free (Non-local) Variables

Used in a block but defined in an **outer scope**.

```javascript
let s = 10;

function temp(x) {
    return x * s;  // 's' is a free variable
}
```

The function looks outward to find `s`.

---

## Scope Resolution (Lexical Scoping)

Most languages:

1. Check local scope
2. Then enclosing scope
3. Then global scope
4. Error if not found

---

## Closures Example

```javascript
function createCounter() {
    let count = 0;
    return function() {
        count = count + 1;
        return count;
    };
}
```

The inner function remembers `count` even after the outer function ends.

---

## Key Points

* Scope determines visibility.
* Keep scope narrow to avoid bugs.
* Minimize global variables.
* Free variables come from enclosing scopes.

---

---

---

# Static vs Dynamic Scoping

When a program uses a **free variable**, how does it decide which one to use? There are two rules:

1. **Static (Lexical) Scoping**
2. **Dynamic Scoping**

---

## Static (Lexical) Scoping

### What It Means

Scope is determined by the **structure of the code** (where functions are written).
You can know which variable is used just by reading the code.

### Lookup Rule (Look Outward in Code)

1. Check current block
2. Check enclosing block
3. Continue outward
4. If not found → error

### Example

```javascript
let x = "global";

function outer() {
    let x = "outer";
    function inner() {
        console.log(x);
    }
    inner();
}
outer();
```

`inner()` prints `"outer"` because it looks at where it is **defined**, not who called it.

### Key Properties

* **Shadowing:** Inner variables hide outer ones.
* **Compile-time resolution**
* **Predictable and easier to debug**
* Supports **closures**

Most modern languages (C, Java, Python, JavaScript) use static scoping.

---

## Dynamic Scoping

### What It Means

Scope is determined by the **call chain at runtime** (who called whom).
You must run the program to know which variable is used.

### Lookup Rule (Look Backward in Call Stack)

1. Check current function
2. Check caller
3. Continue up call chain
4. Then global

### Example Concept

If:

* `main` defines `x`
* `p2` defines another `x`
* `p2` calls `p1`
* `p1` uses `x`

Then under **dynamic scoping**, `p1` uses `p2`’s `x` (because `p2` called it).

### Consequences

* Behavior depends on call history
* Harder to predict and debug
* More runtime overhead
* Rare in modern languages

---

## Quick Comparison

| Aspect         | Static Scoping        | Dynamic Scoping          |
| -------------- | --------------------- | ------------------------ |
| Determined by  | Code structure        | Call stack               |
| When resolved  | Compile time          | Runtime                  |
| Lookup         | Look outward in code  | Look backward in calls   |
| Predictability | High                  | Lower                    |
| Used in        | Most modern languages | Rare / specialized cases |

**Memory Tip:**

* Static → “Where was I defined?”
* Dynamic → “Who called me?”

---

---

# Binding

## What Is Binding?

**Binding** is linking two things together in a program.

Examples:

* Name → variable
* Type → variable
* Value → variable
* Operator (`+`) → addition operation

---

## Binding Times

Binding can happen at different stages:

### 1. Compile Time

* Name binding
* Type binding
* Errors caught early

### 2. Load Time

* Global variables get memory addresses

### 3. Run Time

* Local variables get memory
* Values are assigned

---

## Address Binding

| Variable Type | When Address is Bound              |
| ------------- | ---------------------------------- |
| Global        | Load time                          |
| Local         | Run time (when function is called) |

---

## Early vs Late Binding

* **Early (compile/load time):**

  * Faster
  * Safer
  * Less flexible

* **Late (run time):**

  * More flexible
  * Slower
  * Errors appear later

---

## Key Idea

Declaring a variable creates multiple bindings:

* Name → variable
* Type → variable
* Address → memory
* Value → data

These bindings occur at different times.

---

---

# Type Binding and Value Binding

## Type Binding

Type binding links a **data type** to a variable.

### 1. Static Type Binding

* Happens at **compile time**
* Types cannot change
* Used in C, Java, C#, Go

```java
int age = 25;
// age = "text";  // Compile-time error
```

**Advantages:**

* Early error detection
* Better performance
* Clearer code

---

### 2. Dynamic Type Binding

* Happens at **runtime**
* Variable type can change
* Used in Python, JavaScript, Ruby

```python
x = 10
x = "hello"   # Allowed
```

**Advantages:**

* Flexible
* Less code

**Disadvantages:**

* Runtime errors
* Harder debugging

---

## Type Inference

Compiler automatically determines type.

```kotlin
val age = 25   // Inferred as Int
```

Gives static safety with less verbosity.

---

## Value Binding

Value binding is assigning a **value** to a variable.

* Happens at runtime
* Can occur multiple times

```java
int count;
count = 10;          // Initialization
count = count + 1;   // Reassignment
```

---

## Summary

* **Type binding** → When a variable gets its type

  * Static (compile time)
  * Dynamic (runtime)
  * Inference (compiler decides)

* **Value binding** → When a variable gets its value (runtime)

Static typing = safer, faster
Dynamic typing = flexible
Type inference = balanced approach

---

---

---

# Type Binding, Declarations, and Dynamic Typing

## Type Binding Basics

Before using a variable, it must be **bound to a type**. Two key questions:

1. **How** is the type specified? (Declaration or convention)
2. **When** is it bound? (Compile time or runtime)

---

## Variable Declarations

A **declaration** tells the compiler about a variable’s type.
It does not directly allocate storage—that depends on scope and lifetime.

### 1. Explicit Declaration

Type is clearly stated.

```c
int age;
float salary;
```

* Type fixed at compile time
* Clear and safe

### 2. Implicit Declaration

Type determined by naming conventions or symbols.

Examples:

* **FORTRAN:** Names starting with I–N → integer
* **Perl:** `$` (scalar), `@` (array), `%` (hash)

Both create **static type bindings**.

---

## Declaration Placement and Lifetime

Where a variable is declared affects how long it exists:

```c
int global_var;     // Entire program

void function() {
    int local_var;  // Only during function call
    
    for (int i = 0; i < 10; i++) {
        // i exists only in loop
    }
}
```

---

## Dynamic Type Binding

No explicit type declarations.
Type is bound **when a value is assigned**.

```python
x = 10        # int
x = "hello"   # now string
x = [1,2,3]   # now list
```

### Advantages

* Flexible
* Less code
* Generic functions

### Disadvantages

* Errors appear at runtime
* Extra runtime overhead
* Harder debugging

Dynamic typing requires runtime type checking and extra metadata.

---

## Initialization

**Initialization** = assigning the first value at declaration.

```c
int x = 5;   // Declared and initialized
int y;       // Declared only (may contain garbage)
```

Always initialize to avoid undefined behavior.

---

## Static vs Dynamic Type Checking

| Feature         | Static Typing | Dynamic Typing |
| --------------- | ------------- | -------------- |
| Type bound      | Compile time  | Runtime        |
| Error detection | Early         | Late           |
| Flexibility     | Lower         | Higher         |
| Performance     | Faster        | Slower         |

Type inference (e.g., Kotlin, TypeScript) gives static safety with less verbosity.

---

## Key Points

* **Explicit declarations** improve clarity and safety
* **Dynamic typing** increases flexibility but delays errors
* Initialization is important
* Choice of typing style is a trade-off

---

---

# Constants and Literals

## Constant

A **constant** is a named value that cannot change.

```c
const int MAX_USERS = 100;
```

* Has a name
* Value fixed for its lifetime

Benefits:

* Readability
* Maintainability
* Fewer errors

---

## Literal

A **literal** is a value written directly in code.

Examples:

* `21` (integer)
* `3.14` (float)
* `'A'` (character)
* `"Hello"` (string)
* `true` (boolean)

---

## Written Form vs Stored Form

When you write:

```c
int x = 21;
```

* `"21"` → character sequence in source code
* Stored in memory → binary representation

Programmer sees digits; computer uses binary.

---

## Constant vs Literal

| Constant      | Literal            |
| ------------- | ------------------ |
| Has a name    | No name            |
| Reusable      | Written each time  |
| Example: `PI` | Example: `3.14159` |

Use constants instead of repeating literals for cleaner code.

---

## Key Idea

* **Constant** = named, fixed value
* **Literal** = direct value in code
* Literals are converted to binary for execution

---

---

# Storage Binding and Lifetime

## Storage Binding

Storage binding is assigning **memory space** to a variable.

* **Allocation** → Get memory
* **Deallocation** → Release memory

---

## Lifetime

**Lifetime** = Time between allocation and deallocation.

* Begins when memory is allocated
* Ends when memory is freed

---

## Types of Lifetime

### 1. Static Lifetime

* Allocated once
* Exists entire program
* Example: global variables

### 2. Automatic (Stack) Lifetime

* Allocated when function/block starts
* Removed when it ends
* Example: local variables

### 3. Dynamic (Heap) Lifetime

* Allocated manually (`malloc`, `new`)
* Deallocated manually (`free`, `delete`)
* Used for dynamic data structures

---

## Why Lifetime Matters

* Prevent memory leaks
* Avoid using variables after deallocation
* Improve performance

---

## Summary

* **Storage binding** → Assign memory
* **Lifetime** → How long memory is held
* Three main types: static, automatic, dynamic
* Proper memory management prevents bugs and inefficiency

---

---

---

# Runtime Memory Structure

When a program runs, memory is divided into sections with specific roles.

## Main Memory Areas

### 1. Static / Global Area

* Stores global and static variables
* Allocated at program start, freed at program end
* Fixed size

Example:

```c
int global_count = 0;
```

---

### 2. Stack

* Stores function calls and local variables
* Grows and shrinks automatically (LIFO)
* Very fast

Example:

```c
void func() {
    int local_var = 5;  // On stack
}
```

Each function call creates a **stack frame** containing:

* Local variables
* Parameters
* Return address

---

### 3. Heap

* Stores dynamically allocated memory
* Managed manually (`malloc/free`, `new/delete`) or by GC
* Flexible but slower than stack

Example:

```c
int* arr = malloc(100 * sizeof(int));
free(arr);
```

---

### 4. Registers

* Small, ultra-fast CPU storage
* Used for temporary computations

---

### 5. Read-Only Area (Code & Constants)

* Stores program instructions and literals
* Cannot be modified at runtime

Example:

```c
char* msg = "Hello";  // String literal
```

---

## Simplified Layout

```
High Memory
+-------------------+
|       Stack       |  (grows downward)
+-------------------+
|       Heap        |  (grows upward)
+-------------------+
|   Static/Global   |
+-------------------+
|  Read-Only / Code |
+-------------------+
Low Memory
```

---

## Stack vs Heap

| Stack             | Heap         |
| ----------------- | ------------ |
| Fast              | Slower       |
| Automatic         | Manual / GC  |
| Small             | Larger       |
| No fragmentation  | Can fragment |
| Function lifetime | Until freed  |

---

## Common Problems

* **Stack overflow** → Deep recursion
* **Memory leak** → Forgot to free heap memory
* **Dangling pointer** → Using freed memory

---

## Key Idea

* **Static** → Entire program life
* **Stack** → Function/block lifetime
* **Heap** → Dynamic lifetime
* **Registers** → Temporary CPU use
* **Read-only** → Code and constants

Understanding memory layout helps prevent crashes and improve performance.

---

---

# Variable Lifetime Types

Variables differ by **when memory is allocated and released**.

## 1. Static Variables

* Allocated once (program start)
* Exist until program ends
* Stored in static area

```c
int global_var;
static int counter;
```

**Pros:** Efficient, persistent
**Cons:** Always occupy memory

---

## 2. Stack-Dynamic Variables

* Allocated when block/function starts
* Freed when block/function ends
* Stored on stack

```c
void func() {
    int x = 5;
}
```

**Pros:** Supports recursion, fast
**Cons:** Limited size, no persistence

---

## 3. Explicit Heap-Dynamic Variables

* Allocated manually (`malloc`, `new`)
* Freed manually (`free`, `delete`)
* Stored on heap

```c
int* p = malloc(sizeof(int));
free(p);
```

**Pros:** Flexible size, long lifetime
**Cons:** Risk of leaks, slower

---

## 4. Implicit Heap-Dynamic Variables

* Allocated automatically on assignment
* Managed by runtime/GC
* Type and size may change

```python
x = 10
x = "hello"
```

**Pros:** Flexible, simple syntax
**Cons:** Runtime overhead, late errors

---

## Comparison

| Type          | Allocated      | Freed           | Location    |
| ------------- | -------------- | --------------- | ----------- |
| Static        | Program start  | Program end     | Static area |
| Stack         | Function entry | Function exit   | Stack       |
| Explicit Heap | `malloc/new`   | `free/delete`   | Heap        |
| Implicit Heap | Assignment     | GC/reassignment | Heap        |

---

## Persistence

Persistence means data survives **after program ends** (files, databases).
Variables themselves only live during execution.

---

## Final Summary

* **Static** → Whole program
* **Stack** → Temporary (per function)
* **Explicit heap** → Manual control
* **Implicit heap** → Automatic, flexible

Choose based on lifetime needs and performance considerations.

# Principles of Programming Languages – Introduction

## What Is Programming Language Theory (PLT)?

PLT studies **how programming languages are designed, implemented, analyzed, and classified**.

Instead of just learning how to code in one language, it asks:

* How are languages built (compiler/interpreter)?
* What design choices affect safety, speed, and usability?
* How can we compare and classify languages?

It builds a **mental framework** to understand any language.

---

## Course Objectives

1. **Understand core language concepts**
   Variables, types, control flow, functions.

2. **Understand design decisions and trade-offs**
   Example: Garbage collection → easier coding, more runtime complexity.

3. **Study features independently of languages**
   Learn concepts like OOP or functional programming beyond specific syntax.

**Goal:** Learn principles, not just syntax.

---

## Key Questions About Programming Languages

* **Why do we need them?**
  Computers understand binary; languages act as a bridge.

* **What is a programming language?**
  A formal system (syntax + semantics) for describing algorithms and data.

* **Why so many languages?**
  Different problems require different tools.

* **What makes a language “good”?**
  Depends on goals: speed, safety, readability, scalability.

* **How are languages classified?**

  * Paradigm: Imperative, OOP, Functional, Logic
  * Execution: Compiled, Interpreted, Hybrid
  * Typing: Static vs Dynamic

* **Is a universal language possible?**
  Unlikely—no single tool fits all problems.

---

## Benefits of Studying PLT

* Write better, more efficient programs
* Understand internal behavior of features
* Learn new languages faster
* Choose the right language for projects
* Gain skills to design your own language

It turns you from just a “coder” into a **language-aware problem solver**.

---

# Why Programming Languages?

Computers cannot understand natural language.
Programming languages are **structured artificial languages** that:

* Humans can write
* Machines can execute

They are **problem-solving tools**.

---

# Dijkstra’s Insight

> As computers grew more powerful, programming became more complex.

Powerful hardware enables bigger systems, which increases:

* System complexity
* Design difficulty
* Maintenance challenges

More power → Bigger problems → Greater programming complexity.

---

# What Is a Programming Language?

A programming language is:

* A **notational system** for algorithms and data structures
* Both **human-readable and machine-executable**
* An artificial language to control machine behavior

It must serve two masters:

* Humans (clarity)
* Machines (precision)

---

# What Programming Languages Allow

### 1. Human → Machine

Programmers write instructions; computers execute them.

### 2. Machine → Machine

Programs generate code for other devices.
Example: PostScript controlling printers.

---

## What Is NOT a Programming Language?

**Markup languages (HTML, XML)** are generally not programming languages because they describe structure/layout, not computation.

* Programming language → Specifies process
* Markup language → Specifies structure

---

# What Is Programming?

Programming is not limited to writing Java or Python.

Using:

* Excel formulas
* Word macros
* CSS rules

is also programming—because you're instructing a machine using structured notation.

Programming = **Formulating instructions for machines**.

---

# What Is a Programmer?

A programmer is more like an:

* Architect
* Composer
* Writer

They:

1. Form an outline
2. Design structure (data + algorithms)
3. Refine iteratively

Programming is creative, structured problem solving.

---

# The Programmer’s Core Challenge

For any problem, there are multiple solutions.
Each choice (e.g., array vs linked list vs hash table) affects:

* Performance
* Memory usage
* Maintainability
* Future extensibility

Poor decisions lead to **ad hoc designs**.
Good programmers evaluate trade-offs before committing.

---

# Evolution of Programming Languages

As problems grew, languages evolved.

| Era   | Main Concern          | Innovation                  |
| ----- | --------------------- | --------------------------- |
| 1950s | Machine efficiency    | Assembly, FORTRAN           |
| 1960s | Programmer efficiency | Structured programming      |
| 1970s | Managing complexity   | Data abstraction            |
| 1980s | Modeling real world   | Object-Oriented Programming |
| 1995+ | Networking & scale    | Web & distributed systems   |

Modern systems are too large for one person to fully understand.
Languages help us work at higher abstraction levels.

---

# The Literal Nature of Computers

Computers follow instructions exactly—no intuition, no guessing.

Program behavior depends only on:

```
Program Code + Language Rules + Input Data
```

If something goes wrong, the cause is in:

* The code
* The input
* (Rarely) the language implementation

Programming requires **precision and logical correctness**.

---

# Final Summary

Studying Principles of Programming Languages helps you:

* Understand how languages work internally
* Evaluate design trade-offs
* Manage complexity
* Think abstractly about computation
* Become adaptable to new technologies

It transforms you from someone who **uses languages** into someone who **understands languages**.

# Why So Many Programming Languages?

## The Reality

* There are **hundreds** of languages.
* Programmers use **multiple languages** in their careers.
* Learning a language deeply requires time (syntax, tools, ecosystem).
* Languages shape how you think (procedural, functional, object-oriented).

Mastering one paradigm can make switching to another challenging.

---

## There Is No “Best” Language

Each language serves a **community and purpose**.

* Python → Data science, AI
* JavaScript → Web development
* SQL → Databases
* C → Systems programming

A language is only **“best for a specific job.”**

Like vehicles:

* Racing → Formula 1
* Heavy transport → Truck
* City travel → Compact car

No single tool fits all needs.

---

# Different Domains, Different Needs

Different problem domains require different features.

Example trade-off:

* Maximum speed & control → C, Rust
* Simplicity & rapid development → Python, JavaScript

You usually cannot maximize both at once.

Because requirements conflict, we get **specialized language families**.

---

# Example: Scientific Domain

Scientific computing requires:

* Heavy floating-point math
* Large multi-dimensional arrays
* Parallel computation

Languages built for this:

* FORTRAN
* MATLAB
* Python (NumPy/SciPy)
* Julia

Domain needs drive language design.

---

# Business Applications Domain

Business systems need:

1. **Persistent data** (databases)
2. **Report generation**
3. **Data analysis & aggregation**

Common languages:

* COBOL (legacy finance systems)
* SQL (database queries)
* Java, C# (enterprise systems)

Focus: reliability, transactions, data processing.

---

# Systems Programming Domain

Systems programming builds foundational software (OS, drivers, firmware).

Needs:

* Direct hardware control
* Precise memory management
* Real-time performance

Languages:

* C
* C++
* Rust

Trade-off: High control, harder to use.

---

# Why New Languages Appear

Established languages are hard to change due to:

* Backward compatibility
* Large ecosystems
* Community inertia

New languages emerge when:

* New paradigms arise
* Old languages become too complex
* A pain point needs solving

Examples:

* Go → Simple concurrency
* Rust → Memory safety in systems

Innovation happens when new needs arise.

---

# Why a Universal Language Is Impossible

Programming needs vary across:

1. Program size (small scripts vs OS kernels)
2. Programmer expertise (novice vs expert)
3. Hardware targets (microcontrollers vs supercomputers)
4. Change frequency (rapid startups vs satellite software)

These requirements often conflict.

Therefore, we will always need a **portfolio of languages**, not one universal solution.

---

# Language Components

Every programming language has three core parts:

1. **Vocabulary** – Keywords, operators, identifiers, literals
2. **Syntax** – Rules for forming valid programs
3. **Semantics** – Meaning and behavior of code

Compiler flow:

```
Vocabulary → Structured by Syntax → Given Meaning by Semantics
```

---

# Language Levels (Abstraction Stack)

From lowest to highest:

1. **Machine Language** – Binary instructions
2. **Operating System** – Manages hardware
3. **Compiler/Interpreter** – Translates code
4. **Programming Language** – Code you write
5. **Application Systems** – Final software

Each layer hides complexity of the one below.

---

# Machine-Level Languages

* Pure binary instructions
* Directly executed by CPU
* Extremely hard to write
* CPU uses internal microcode to execute instructions

Rarely written by humans today.

---

# Low-Level vs High-Level Languages

## Low-Level (Assembly)

* Close to hardware
* One instruction ≈ one machine instruction
* High control, low portability

## High-Level (Python, Java, C++)

* Abstract and readable
* One line = many machine instructions
* Portable and productive

Trade-off:

* High-level → Productivity & readability
* Low-level → Control & performance

---

# Features of Good Programming Languages

## 1. Clarity & Simplicity

* Easy to read, write, learn
* Small set of primitives
* Consistent rules
* Different things look different

Too many features reduce readability.

---

## Threats to Readability

* Too many constructs
* Multiple ways to do the same thing
* Excessive operator overloading

Consistency improves maintainability.

---

## 2. Reliability

A reliable language:

* Produces consistent results
* Behaves the same across platforms
* Prevents common errors

Minimizes ambiguity and incompatibility.

---

## 3. Orthogonality

Features combine freely without restrictions.

If a language supports:

* Functions
* Structured types

It should allow functions returning structured types.

Orthogonality reduces special cases.

---

## 4. Efficient Implementation

A language must be implementable efficiently.

Overly complex features can make compilers slow and impractical.

Balance: expressive power vs performance.

---

## 5. Uniformity

Similar constructs should look similar.

Consistency in structure improves learning and readability.

---

## 6. Cost

Language design affects total cost:

1. Training cost
2. Development cost
3. Compilation cost
4. Execution cost
5. Maintenance cost

High-level languages reduce development cost.
Low-level languages reduce execution cost.

Design is always about trade-offs.

---

# Final Summary

* Many languages exist because problems differ.
* No language is universally best.
* Domains shape language features.
* Good languages balance clarity, reliability, orthogonality, efficiency, and cost.
* Understanding principles helps you choose the right tool for the job.

# Language Paradigms

## What Is a Programming Paradigm?

A **paradigm** is a fundamental style of programming—a way of thinking about problems.

### Three Main Paradigms

1. **Imperative** – *How to do it* (step-by-step commands)
2. **Functional** – *What to compute* (functions and transformations)
3. **Logic** – *What is true* (facts and rules)

**OOP is orthogonal**: it can combine with any of these (e.g., Java = OOP + Imperative, Scala = OOP + Functional).

---

## Imperative Paradigm

Based on changing the **machine state** (memory values).

* Program = sequence of commands
* Each command modifies variables
* Final result = final state of memory

Example:

```c
int x = 5;
x = x + 1;
```

Here, `x` changes state.

**Idea:** Do this, then that (like a recipe).
**Languages:** C, C++, Java, Python.

---

## Functional Paradigm

Computation = evaluation of **mathematical functions**.

Core ideas:

* **Immutability** (no changing data)
* **Pure functions** (same input → same output, no side effects)
* Functions are first-class values

Example:

```python
def addOne(x):
    return x + 1
```

`x` is not modified; a new value is returned.

**Idea:** Transform inputs into outputs.
**Languages:** Haskell, Lisp, ML (functional features in many modern languages).

---

## Logic Paradigm

Based on **facts, rules, and queries**.

Program = knowledge base.
Execution = logical deduction.

Example (Prolog-style):

```prolog
fatherOf(john, bob).
grandFatherOf(X, Y) :- fatherOf(X, Z), fatherOf(Z, Y).
```

You ask:

```
?- grandFatherOf(john, Who).
```

The system finds answers logically.

**Idea:** Declare truths; system finds solutions.
**Language:** Prolog.

---

## Object-Oriented Programming (OOP)

Organizes code around **objects** (data + behavior).

Key principles:

* Encapsulation
* Inheritance
* Polymorphism

Example:

```java
class Car {
    int speed;
    void accelerate(int amount) {
        speed += amount;
    }
}
```

OOP is structural and can combine with other paradigms.

---

## Markup Languages

* Describe structure, not computation
* No algorithms or state changes
* Examples: HTML, XML

They specify *what something looks like*, not *how to compute it*.

---

## Paradigm Comparison

| Paradigm   | Core Idea                    | Focus             |
| ---------- | ---------------------------- | ----------------- |
| Imperative | Change state                 | Commands          |
| Functional | Evaluate functions           | Transformations   |
| Logic      | Deduction from facts         | Truth & inference |
| OOP        | Objects with data & behavior | Structure         |
| Markup     | Describe structure           | Presentation      |

Most modern languages are **multi-paradigm**.

---

# Basic Operations of a Computer

## What a CPU Natively Understands

1. **Basic Data Types**

   * Integers
   * Floating-point numbers
   * Basic characters

2. **Primitive Operations**

   * Hard-wired machine instructions

Everything software does reduces to simple operations on basic data.

---

## Instruction Set

The **instruction set** is the CPU’s vocabulary.

Categories:

* **Arithmetic:** ADD, SUB
* **Logic:** AND, OR, NOT
* **Data Movement:** LOAD, STORE, MOVE
* **Control Flow:** JUMP, CALL, RETURN

Different CPUs (x86, ARM) have different instruction sets.

---

## Instruction Compatibility

Different processors can share the same instruction set.

Result:

* Software runs on multiple hardware vendors
* Enables competition and portability

---

## Structure of a Machine Instruction

Each instruction has:

1. **Opcode** – What to do
2. **Operands** – What to operate on

Execution cycle:

1. Fetch
2. Decode
3. Execute
4. Move to next instruction

---

## Why Not High-Level Machine Language?

CPUs don’t directly run Python/Java because:

* High-level operations are too complex for hardware
* It would make CPUs expensive and inflexible
* Software translation (compiler/interpreter) is more practical

Better model:

```
High-Level Code → Translator → Machine Code → Hardware
```

---

# Language Implementation

## Purpose

Implementation systems (compiler/interpreter) translate human-readable code into machine-executable instructions.

Without them, source code cannot run.

---

## Key Implementation Issues

Design choices affect:

* Compiler complexity
* Translation speed
* Execution speed
* Portability
* Code size
* Debugging ease

There are always trade-offs.

---

## Implementation Methods

### 1. Compilation

Entire program → machine code before execution.

* Fast execution
* Platform-specific
  Example: C, C++

### 2. Interpretation

Executed line-by-line at runtime.

* Fast startup
* Slower execution
  Example: Python, JavaScript

### 3. Hybrid

Compile to intermediate code → run on virtual machine.

* Portable
* Balanced speed
  Example: Java, C#

---

## The Virtual Computer

When running a program, you often use a **virtual machine**.

Example:

* Java runs on JVM
* Python runs on Python interpreter

Layered view:

```
Program
↓
Virtual Machine
↓
Operating System
↓
Hardware
```

This provides portability and abstraction.

---

# Programs and Data

## Traditional View (C, FORTRAN)

* Code and data are separate
* Code is read-only
* Data is read-write

Improves safety.

---

## Code as Data (LISP, Prolog)

Programs can manipulate code as data.

Example (conceptually):

```lisp
(eval '(+ 1 2))
```

This enables metaprogramming.

---

## Key Insight

At the lowest level, everything is bits.
The distinction between **program** and **data** depends on the language and implementation design.

---

# Final Summary

* Paradigms shape how we think about programming.
* CPUs understand only simple instructions.
* Compilers and interpreters bridge human code and hardware.
* Implementation choices involve trade-offs.
* Some languages separate code and data strictly; others treat them interchangeably.

Understanding these foundations helps you see how high-level programming connects to the machine level.

# Notion of Computability

## The Core Question

Computability asks:

> **Which problems can be solved by an algorithm?**

A problem is **computable** if a finite, step-by-step mechanical procedure exists to solve it.

Examples:

* Sorting numbers → computable
* Halting Problem (will a program stop?) → non-computable

This defines the **limits of computation**.

---

## Church–Turing Thesis

Church and Turing (1930s) independently formalized computation.

### Core Claim

Anything that is **algorithmically solvable** can be computed by:

* **Lambda calculus** (Church)
* **Turing Machine** (Turing)
* **Recursive functions**

All define the **same class of computable functions**.

This is not formally provable (because “effectively calculable” is intuitive), but it is universally accepted.

---

## Turing Machine (Concept)

A Turing Machine has:

* Infinite tape (memory)
* Read/write head
* Finite set of states
* Transition rules

Despite its simplicity, it can compute anything modern computers can.

If a language can simulate a Turing Machine, it is **Turing-complete**.

---

## Big Picture

Computable problems:

* Can be expressed in lambda calculus
* Can be computed by Turing Machines
* Can be implemented in any Turing-complete language

Non-computable problems:

* No algorithm exists (e.g., Halting Problem)

This defines both the **power and limits** of programming.

---

# Von Neumann Architecture

## Key Idea: Stored-Program Concept

John von Neumann formalized modern computer architecture:

* **Program and data stored in the same memory**
* Machine is general-purpose and reprogrammable

---

## Main Components

* **Memory** – stores data and instructions
* **CPU**

  * Control Unit (directs execution)
  * ALU (performs arithmetic/logic)
* **Input/Output** – external communication

Most modern computers follow this model.

---

## Fetch–Execute Cycle

The CPU repeatedly:

1. Fetch instruction from memory
2. Decode it
3. Fetch operands
4. Execute operation
5. Store result
6. Repeat

The **Program Counter (PC)** tracks the next instruction.

Branch instructions modify the PC → enables loops and function calls.

---

## Imperative Languages Mirror Hardware

Imperative languages map directly to this architecture:

| Hardware Concept     | Language Concept |
| -------------------- | ---------------- |
| Memory cells         | Variables        |
| ALU operations       | Expressions      |
| PC changes           | If, loops, goto  |
| Sequential execution | Statement order  |

Example:

```c
x = y + z;
```

Fetch `y` and `z` → compute → store in `x`.

---

## Von Neumann Bottleneck

CPU is very fast.
Memory access is slower.

The data bus between CPU and memory becomes a **bottleneck**.

Consequences:

* Sequential execution limits parallelism
* Modern solutions: caches, multicore CPUs, parallel models

Functional programming helps parallelization because it avoids shared mutable state.

---

# Program Environments

Programs run in different environments, which influence design.

---

## 1. Batch Processing

* Input from files
* Output to files
* No user interaction
* Errors stop execution
* Time not critical

Examples:

* Payroll processing
* Monthly reports

Structure: Large monolithic program.

---

## 2. Interactive Environment

* Continuous user interaction
* Must respond quickly
* Errors handled gracefully
* Event-driven structure

Examples:

* Websites
* Games
* Word processors

Response time is critical (milliseconds matter).

---

## 3. Embedded Systems

Computers inside devices.

Characteristics:

* Direct hardware control (sensors/actuators)
* Real-time constraints
* High reliability required
* Limited resources
* Often concurrent components

Examples:

* Car control systems
* Medical devices
* Satellites

Languages: C, Ada, Rust.

---

## Environment Comparison

| Feature          | Batch          | Interactive       | Embedded                 |
| ---------------- | -------------- | ----------------- | ------------------------ |
| User Interaction | None           | Continuous        | None                     |
| Timing           | Flexible       | Fast response     | Often real-time          |
| Error Handling   | Stop & restart | Graceful recovery | Autonomous recovery      |
| I/O              | Files          | User devices      | Sensors & hardware       |
| Structure        | Monolithic     | Event-driven      | Distributed & concurrent |

---

# Final Insight

* **Computability** defines what can be solved by algorithms.
* **Church–Turing Thesis** defines the boundary of computation.
* **Von Neumann architecture** shaped imperative programming.
* **Program environments** influence language and system design.

Understanding these foundations explains both the power and limits of modern computing.

# Programming Environments & Debugging

## Programming (Host) Environment

A **programming environment** is the toolkit used to develop software.

Core components:

* **Editor** – Write and edit code
* **Debugger** – Inspect and fix bugs
* **Build tools** – Compile/package programs
* **Version control** – Track changes
* **Testing tools** – Run automated tests
* **Libraries/APIs** – Reusable code

A well-integrated environment (IDE) improves productivity.

---

## Debugging Techniques

### 1. Execution Trace

Automatically logs changes to selected variables or lines.

Best for:

* Tracking how values evolve
* Debugging loops or state changes

Example:

```python
total = 0
total += 100
total += 50
```

Trace shows: 0 → 100 → 150

---

### 2. Breakpoints

Pause execution at a specific line.

Allows you to:

* Inspect variables
* Step through code
* Modify values
* Continue execution

Best for interactive exploration of program state.

---

### 3. Assertions

Assertions check that certain conditions **must be true**.

Example:

```python
assert time > 0, "Time must be positive"
```

If condition is false → program stops immediately.

Uses:

* Check preconditions
* Check postconditions
* Validate invariants

During development → enabled
In production → often disabled for performance

Assertions make code self-checking and self-documenting.

---

## Debugging Summary

| Tool       | Purpose                       |
| ---------- | ----------------------------- |
| Trace      | Monitor changes automatically |
| Breakpoint | Pause and inspect program     |
| Assertion  | Validate assumptions          |

These tools balance **safety and performance**.

---

# Formal Languages

## What Is a Formal Language?

A **formal language** is a precisely defined system of symbols and rules.

It requires:

1. **Alphabet** – Basic symbols
2. **Syntax** – Rules for forming valid structures
3. **Semantics** – Meaning of those structures

A formal language is defined using a **meta-language** (a language used to describe another language).

The meta-language must be **unambiguous**.

---

# Alphabet, Syntax, and Semantics

## Alphabet (Σ)

A finite set of basic symbols.

Example (C language):

* Letters: a–z
* Digits: 0–9
* Operators: +, -, *
* Keywords: if, while

Symbols alone have no meaning—meaning comes from structure.

---

## Syntax

### 1. Lexical Syntax

Defines **tokens** (smallest meaningful units).

Example:

```
<token> ::= <identifier> | <numeral> | <reserved word>
```

### 2. Phrase-Structure Syntax

Defines how tokens form valid programs.

Example:

```
<program> ::= program <identifier> <block>
<block> ::= <declaration seq> begin <command seq> end
```

Syntax ensures structural correctness.

---

## Semantics

Semantics defines **meaning**.

Example:

```c
x = 5;
```

Semantics: store value 5 in variable x.

A statement can be:

* **Syntactically correct but semantically wrong**
* Example: infinite loop due to wrong logic

Syntax = structure
Semantics = behavior

---

# Abstract vs. Concrete Syntax

## Concrete Syntax

Actual written form of code.

Example (C):

```c
while (i < n) {
    i = i + 1;
}
```

## Abstract Syntax

Logical structure without punctuation details.

Example representation:

```
WhileLoop
 ├── Condition: i < n
 └── Body: i = i + 1
```

Compilers convert concrete syntax → **Abstract Syntax Tree (AST)**.

Abstract syntax captures core structure independent of notation.

---

# Strings in Formal Languages

## String (Word)

A **string** is a sequence of symbols from an alphabet.

Example:
Σ = {a, b}

Valid strings:

* "a"
* "ab"
* "abab"
* ε (empty string)

Order matters:

* "ab" ≠ "ba"

---

## Notation

* Symbols: a, b, c
* Strings: u, v, w

Example:

```
Σ = {0,1}
w = 0101
```

---

# String Operations

## 1. Concatenation

Combine strings end-to-end.

If w = "ab", v = "cd"
wv = "abcd"

---

## 2. Reverse

Flip string.

If w = "abc"
wᴿ = "cba"

---

## 3. Length

Number of symbols.

|w| = 3 if w = "abc"
|ε| = 0

---

## 4. Empty String (ε)

* Length 0
* Identity for concatenation

εw = wε = w

---

## Prefix and Suffix

If w = uv:

* u is a **prefix**
* v is a **suffix**

Example: w = "abbab"

Prefixes:
ε, a, ab, abb, abba, abbab

Suffixes:
ε, b, ab, bab, bbab, abbab

---

## Power of a String

wⁿ = string repeated n times

Example: w = "ab"

* w⁰ = ε
* w¹ = "ab"
* w² = "abab"
* w³ = "ababab"

w⁰ = ε because ε is the identity for concatenation.

---

# Final Summary

* Programming environments provide tools for development and debugging.
* Debugging relies on traces, breakpoints, and assertions.
* Formal languages require alphabet, syntax, and semantics.
* Abstract syntax captures logical structure independent of notation.
* Strings and string operations form the foundation of formal language theory.

# String Sets, Kleene Closure, and Languages

## String Sets (Σᵏ)

* **Σᵏ** = all strings of length exactly *k* over alphabet Σ.
* **Σ⁰ = {ε}** (only the empty string).

Example: Σ = {0,1}

```
Σ⁰ = {ε}
Σ¹ = {0,1}
Σ² = {00,01,10,11}
Σ³ = {000,001,010,011,100,101,110,111}
```

---

## Kleene Closure (Σ*)

* **Σ*** = all finite strings over Σ (length 0,1,2,...).
* **Σ⁺** = all non-empty strings (Σ* − {ε}).

Example: Σ = {a}

```
Σ* = {ε, a, aa, aaa, ...}
Σ⁺ = {a, aa, aaa, ...}
```

Σ* is **closed under concatenation**.

---

## What Is a Language?

A **language** is any subset of Σ*.

* **Finite**: L₁ = {a, aa, abb}
* **Infinite**: L₂ = {aⁿbⁿ | n ≥ 0} = {ε, ab, aabb, aaabbb, ...}

Programming analogy:

* Σ* = all possible text.
* Programming language = syntactically valid subset.

---

## Same Kleene Closure from Different Sets

If a set contains enough basic pieces, its closure may equal another's.

Example:

* S = {a, b, ab}
* T = {a, b, bb}

Both give: **{a,b}***

Extra elements don’t add power if single symbols already exist.

---

## Theorem: S* = S**

Applying Kleene star twice adds nothing new.

* S* = all concatenations of S.
* S** = concatenations of elements already in S*.

Thus: **S* = S****.

Example: S = {ab}

```
S* = {ε, ab, abab, ababab, ...}
S** = same set
```

---

# Operations on Languages

Since languages are sets:

* **Union (L₁ ∪ L₂)**
* **Intersection (L₁ ∩ L₂)**
* **Difference (L₁ − L₂)**
* **Complement (Σ* − L)**

## Concatenation

L₁L₂ = {xy | x ∈ L₁, y ∈ L₂}

Example:

```
L₁ = {a, ab}
L₂ = {b, ba}

L₁L₂ = {ab, aba, abb, abba}
```

---

## Powers and Closures of a Language

### Lⁿ

* L⁰ = {ε}
* L¹ = L
* L² = LL
* Lⁿ = L concatenated n times

Example: L = {ab, c}

```
L² = {abab, abc, cab, cc}
```

### Star Closure (L*)

All strings from concatenating L zero or more times.

L* = L⁰ ∪ L¹ ∪ L² ∪ ...

### Positive Closure (L⁺)

One or more concatenations.

L⁺ = L* − {ε}

---

# Language Definition Mechanisms & BNF

## Two Ways to Define a Language

1. **Recognition rules** – Check if a string belongs.
2. **Generation rules** – Produce valid strings.

Listing strings works only for finite languages. Infinite languages need rule-based definitions.

---

# BNF (Backus–Naur Form)

A **metalanguage** for defining syntax precisely.

## Components

1. **Terminals (Σ)** – Actual symbols (`if`, `+`, `a`).
2. **Non-terminals (N)** – Categories (`<expression>`).
3. **Productions (ρ)** – Replacement rules.
4. **Start symbol (S)** – Entry point.

### Example

```
<assignment> ::= <variable> = <expression> ;
```

`|` means OR.

---

## Signed Integer Example (Classic BNF)

```
<signed integer> ::= <integer> | + <integer> | - <integer>
<integer> ::= <digit> | <integer> <digit>
<digit> ::= 0 | 1 | ... | 9
```

Recursion allows arbitrary length numbers.

---

## Extended BNF (EBNF)

Adds shorthand:

* `[x]` → optional
* `{x}` → repeat 0 or more times

Example:

```
<signed integer> ::= [+ | -] <digit> {<digit>}
```

More readable, no explicit recursion.

---

# BNF Recursion and Derivations

## Recursive Lists

Right recursion:

```
<list> ::= item | item , <list>
```

Left recursion:

```
<expr> ::= <expr> + term | term
```

Recursion enables repetition and nesting.

---

## Grammar for a Small Language

Structure:

```
<program> ::= begin <stmt_list> end
<stmt_list> ::= <stmt> | <stmt> ; <stmt_list>
<stmt> ::= <var> := <expression>
<var> ::= A | B | C
<expression> ::= <var> + <var> | <var> - <var> | <var>
```

Valid example:

```
begin A := B + C; B := C end
```

---

## Derivation

A **derivation** replaces non-terminals step by step until only terminals remain.

Intermediate strings are **sentential forms**.

Final string with only terminals = valid program.

Derivations can be:

* Leftmost
* Rightmost
* Mixed

All produce the same language.

---

# Valid Programs

A valid program must:

1. Contain only terminals
2. Be derivable from the start symbol
3. Satisfy semantic rules

BNF ensures syntax only.

---

# Limitations of BNF

BNF **cannot** express:

* Duplicate declarations
* Declaration-before-use
* Type checking
* Context-sensitive constraints

These are handled in **semantic analysis**, not parsing.

Compilation flow:

```
Source → Lexical → Parsing (BNF) → Semantic Analysis → Code Generation
```

---

# Syntax Diagrams

Visual alternative to BNF.

Example (identifier):

EBNF:

```
<identifier> ::= <letter> {<letter> | <digit>}
```

Diagram shows:

* One mandatory letter
* Loop of letters or digits

Pros:

* Visual and intuitive
* Clear repetition

Cons:

* Complex for large grammars
* Less formal than BNF

---

# Final Summary

* **Σᵏ**: Strings of fixed length.
* **Σ***: All finite strings.
* **Language**: Subset of Σ*.
* **Lⁿ, L*, L⁺**: Language repetition operations.
* **BNF/EBNF**: Formal tools to define syntax.
* **Recursion**: Enables lists and repetition.
* **Derivations**: Show how strings are generated.
* **BNF limits**: Syntax only, not semantics.

## Formal Grammar and Derivations

### Lexical vs Phrase Structure

Programming language grammars are usually split into:

1. **Lexical structure (micro-syntax)**

   * Defines how characters form **tokens** (identifiers, numbers, keywords).
   * Example: `<identifier> ::= <letter> {<letter>|<digit>}`

2. **Phrase structure (macro-syntax)**

   * Defines how tokens form expressions and statements.
   * Example: `<if-statement> ::= if ( <condition> ) <statement>`

**Why split?**

* Clear separation of concerns.
* Faster lexical analysis before parsing.
* Easier maintenance.

Pipeline:
`Source Code → Scanner → Tokens → Parser → Parse Tree`

---

## Formal Definition of a Grammar

A grammar is written as:

**G = (N, Σ, P, S)**

* **N**: Non-terminals (syntactic categories)
* **Σ**: Terminals (actual symbols)
* **P**: Productions (rules)
* **S**: Start symbol
* Constraint: **N ∩ Σ = ∅**

Example:

```
N = {S, A}
Σ = {a, b}
P = {S → aA, A → b}
S = S
```

---

## How Strings Are Generated

1. Start from **S**.
2. Replace non-terminals using productions.
3. Stop when only terminals remain.

A **derivation** is the sequence of these steps.

Different grammars can define the same language (e.g., `S → aS | a` and `S → a | Sa` both generate `{a⁺}`).

---

## Productions and Notation

General form:
`α → β`

For **context-free grammars (CFGs)**:

* Left side is a single non-terminal: `A → β`

Shorthand:

```
A → a | b | c
```

---

## Derivation Notation

* One step: `w₁ ⇒ w₂`
* Zero or more steps: `⇒*`
* One or more steps: `⇒+`

Example:

```
S → 0S1 | ε

S ⇒ 0S1 ⇒ 00S11 ⇒ 0011
```

So `S ⇒* 0011`.

A **sentential form** is any intermediate string.
The **language** is:

**L(G) = { w | S ⇒* w and w contains only terminals }**

---

## Example: Balanced 0s and 1s

Grammar:

```
S → 0S1 | ε
```

Generates:

```
ε, 01, 0011, 000111, ...
```

Language: `{0ⁿ1ⁿ | n ≥ 0}` (balanced pairs).
This is **context-free but not regular**.

---

## ε-Productions

An **ε-production** replaces a non-terminal with the empty string.

Uses:

* End recursion
* Optional elements
* Base cases

Example:

```
S → aS | ε
```

Deriving "aa":

```
S ⇒ aS ⇒ aaS ⇒ aa
```

ε is not a terminal; it means “nothing”.

---

# Chomsky Hierarchy

Grammars are classified by rule restrictions:

## Type 0 – Unrestricted

* No restrictions on productions.
* Equivalent to Turing machines.
* Very powerful but impractical for programming languages.

## Type 1 – Context-Sensitive

* Replacements cannot shorten strings (except possibly start symbol).
* More restricted than Type 0.
* Recognized by linear bounded automata.

## Type 2 – Context-Free (CFG)

* Left side is a single non-terminal.
* Used for programming language syntax.
* Recognized by pushdown automata.
* Written using **BNF**.

Example:

```
<if> → if ( <cond> ) <stmt> else <stmt>
```

## Type 3 – Regular

* Right-linear or left-linear rules.
* Recognized by finite automata.
* Used for lexical analysis.

Example:

```
S → 0S | 1S | 0 | 1
```

Hierarchy (inclusion):

```
Regular ⊆ Context-Free ⊆ Context-Sensitive ⊆ Type 0
```

More restrictions → easier recognizers.

---

## Example Grammars

### G₁

```
S → 0S1 | ε
```

Language: `{0ⁿ1ⁿ}`
Context-free, not regular.

### G₂

```
S → ZU
Z → 0Z | ε
U → 1U | ε
```

Language: `0*1*`
Context-free (language is actually regular).

### G₃

```
S → 0S | 0 | 1 | 1R | ε
R → 1 | 1R
```

Right-linear → **regular**.
Language: `0*1*`.

---

## BNF and CFG Equivalence

BNF and formal CFG notation describe the same class of languages.
Only the symbols differ (`::=` vs `→`, angle brackets vs capital letters).

---

# Equivalence, Proofs, and Ambiguity

## Language of a Grammar

For grammar **G = (N, Σ, P, S)**:

**L(G)** = all terminal strings derivable from S.

Two grammars are **equivalent** if they generate the same language.

Example:

```
G1: S → aSb | ε
G2: S → aAb | ε
    A → aAb | ε
```

Both generate `{aⁿbⁿ}` → equivalent.

---

## Proving a String Belongs to a Language

Two methods:

1. **Parse tree**
2. **Derivation sequence**

Example:

```
Integer → Digit | Integer Digit
Digit → 0 | ... | 9
```

Deriving "352":

```
Integer ⇒ Integer Digit
⇒ Integer Digit Digit
⇒ Digit Digit Digit
⇒ 3 5 2
```

---

## Canonical Derivations

To avoid confusion:

* **Leftmost derivation**: always expand leftmost non-terminal.
* **Rightmost derivation**: always expand rightmost.

Both produce the same parse tree if the grammar is unambiguous.

---

## Ambiguous Grammars

A grammar is **ambiguous** if a string has more than one parse tree.

Example:

```
E → E - E
  | E * E
  | a | b | c
```

String: `a - b * c`

Two interpretations:

* `(a - b) * c`
* `a - (b * c)`

Ambiguity occurs because precedence isn’t enforced.

---

## Removing Ambiguity

Rewrite grammar to encode precedence:

```
Expression → Expression - Term | Term
Term → Term * Factor | Factor
Factor → a | b | c
```

Now `a - b * c` parses only as:

```
a - (b * c)
```

---

## Key Takeaways

* **Grammar**: G = (N, Σ, P, S)
* **L(G)**: all strings derivable from S
* **Regular grammars** → finite automata (lexical level)
* **Context-free grammars** → pushdown automata (syntax level)
* **Equivalent grammars** generate the same language
* **Ambiguity** means multiple parse trees for one string
* Ambiguity is removed by encoding precedence and structure in the grammar

# Language Elements

## Keywords & Reserved Words

### 1. Syntactic Elements

Syntactic elements are the structural building blocks of a programming language.
**Keywords** and **Reserved Words** define how code is written and understood.

---

## 2. Keywords

### Definition

A **keyword** has a special meaning **in specific contexts**, but may sometimes be used as an identifier (if the language allows it).

### Example (FORTRAN)

```
REAL APPLE
REAL = 3.4
```

* `REAL APPLE` → `REAL` is a type keyword.
* `REAL = 3.4` → `REAL` is a variable name.

Here, `REAL` is a keyword but **not reserved**.

### Purpose of Keywords

* Define actions (`if`, `while`, `print`)
* Improve readability
* Help the compiler identify program structure

---

## 3. Reserved Words

### Definition

A **reserved word** always has a special meaning and **cannot** be used as a variable or function name.

**Rule:** If a word is reserved, it is completely off-limits as an identifier.

### Reserved Words in Languages

| Language    | Reserved Words |
| ----------- | -------------- |
| C           | ~25            |
| COBOL       | ~400           |
| Pure PROLOG | None           |

### Implications

* **Few reserved words (C):** More flexibility, compact syntax.
* **Many reserved words (COBOL):** Very structured, English-like, more verbose.
* **No reserved words (PROLOG):** Maximum flexibility but fewer built-in cues.

---

## 4. Keyword vs Reserved Word

| Concept       | Meaning                    | Can Be Variable Name? |
| ------------- | -------------------------- | --------------------- |
| Keyword       | Special meaning in context | Sometimes             |
| Reserved Word | Special meaning always     | Never                 |

**All reserved words are keywords, but not all keywords are reserved.**
Modern languages usually prefer reserved words for clarity.

---

# Reserved Words – Design Implications

## C vs COBOL Example

**C (compact):**

```c
if (salary)
    amount = 40 * payrate;
else
    amount = hours * payrate;
```

**COBOL (English-like):**

```
IF Salary THEN
    MULTIPLY Payrate BY 40 GIVING Amount
ELSE
    MULTIPLY Payrate BY Hours GIVING Amount
END-IF.
```

### Observations

* C: Short, symbolic, fewer reserved words.
* COBOL: Verbose, readable English-style, many reserved words.

### Problems with Many Reserved Words

* Hard to remember all of them
* Difficult to extend language (new reserved words may break old code)
* Number of reserved words does **not** determine language power

---

## Keywords That Are Not Reserved (PL/I)

Example:

```
IF THEN THEN THEN = ELSE; ELSE ELSE = THEN;
```

Here, `IF`, `THEN`, and `ELSE` are keywords but also valid variable names.
This causes:

* Readability problems
* Confusion between identifiers and keywords
* Harder parsing

---

# Why Modern Languages Prefer Reserved Words

Example (FORTRAN):

```
INTEGER REAL
REAL INTEGER
```

* `INTEGER REAL` → variable `REAL` of type `INTEGER`
* `REAL INTEGER` → variable `INTEGER` of type `REAL`

This creates confusion and cognitive overload.

### Modern Approach

Languages like Java, Python, and C# reserve core words (`if`, `class`, `return`) to:

* Prevent ambiguity
* Improve readability
* Simplify compilation

**Clarity is preferred over flexibility.**

---

# Comments

## What Are Comments?

Comments are explanatory text ignored by the compiler.
They serve as **internal documentation**.

> If code needs heavy explanation, it may be too complex.

### Good Comment Principles

* Explain **why**, not **what**
* Document assumptions
* Mark TODOs
* Clarify complex logic

Example:

```python
# Use binary search for O(log n) performance
def find(sorted_list, target):
    ...
```

Bad example:

```python
# Increment x
x = x + 1
```

---

## Comment Styles

| Language   | Syntax              |
| ---------- | ------------------- |
| C/Java/C++ | `//` or `/* ... */` |
| Python     | `#`                 |
| HTML       | `<!-- ... -->`      |
| SQL        | `--` or `/* ... */` |

Some comments (e.g., JavaDoc, Python docstrings) generate documentation automatically.

---

# Comment Design Issues

Language designers must decide:

### 1. Where Comments Start

* Early languages: fixed columns (FORTRAN: `C` in column 1)
* Modern languages: anywhere on a line

### 2. How Comments End

* Line-based: `//`, `#`
* Block-based: `/* ... */`

### 3. Nested Comments

Most languages **do not** allow nested block comments, which can cause issues when commenting out large code blocks.

---

# Historical Comment Examples

| Language | Comment Rule        |
| -------- | ------------------- |
| FORTRAN  | `C` in column 1     |
| BASIC    | `REM` at line start |
| COBOL    | `*` in column 7     |

These restrictions came from punch-card formatting.

---

# Modern Improvements

* Flexible comment placement
* Both line and block comments
* IDE shortcuts for block commenting
* Alternatives like conditional compilation (`#if 0` in C)

---

# Key Takeaways

* **Reserved words improve clarity and reduce ambiguity.**
* Many vs few reserved words reflect language design philosophy.
* Keywords that aren’t reserved can cause confusion.
* Comments document intent, not obvious actions.
* Modern comment systems are flexible compared to early fixed-format languages.

Understanding these design choices helps explain how programming languages balance **readability, flexibility, and maintainability**.

## Comment Syntax Across Programming Languages

Programming languages support two main comment types: **single-line** and **block (multi-line)** comments.

---

### 1. End-of-Line (Single-Line) Comments

These start anywhere on a line and end automatically at the line break.

| Language            | Syntax | Example                        |
| ------------------- | ------ | ------------------------------ |
| ALGOL 60, Assembly  | `;`    | `x := 5; ; comment`            |
| Ada, mySQL          | `--`   | `total := x; -- compute total` |
| C++/Java/C#         | `//`   | `int x = 5; // init`           |
| FORTRAN 90          | `!`    | `x = 5 ! assign`               |
| Python, Shell, Perl | `#`    | `x = 5 # set x`                |

**Features:**

* Simple and common
* Good for short notes
* Cannot span multiple lines

---

### 2. Block (Multi-Line) Comments

These span multiple lines and require explicit start and end markers.

| Language         | Syntax                   |
| ---------------- | ------------------------ |
| Pascal           | `(* ... *)` or `{ ... }` |
| C, C++, Java, JS | `/* ... */`              |
| HTML/XML         | `<!-- ... -->`           |
| ALGOL            | `comment ... ;`          |

Example (C-style):

```c
/* Multi-line
   comment */
```

Block comments are useful for longer explanations or disabling code sections.

---

### 3. Languages with Multiple Comment Styles

Many modern languages support both types.

Example (C++/Java):

```cpp
// Single-line comment

/*
 Multi-line comment
*/

/** Documentation comment */
```

PHP supports `//`, `#`, and `/* ... */`.

This flexibility allows short notes, long explanations, and documentation generation (e.g., Javadoc).

---

### 4. Comment Nesting

**Nested comments** mean putting one block comment inside another.

Most languages (C, Java, JavaScript) **do not allow nesting**:

```java
/* Outer comment
   /* Inner comment */
   Error occurs here
*/
```

The first `*/` closes the comment, causing errors.

Some languages (e.g., MATLAB, D) support nested comments, but this increases compiler complexity.

---

### 5. Practical Usage Patterns

**Documentation comments:**

```java
/**
 * Calculates factorial.
 * @param n >= 0
 */
```

**Temporarily disabling code:**

```python
# old_function()
```

**Section headers:**

```javascript
// =====================
// AUTH MODULE
// =====================
```

---

### 6. Evolution of Comment Syntax

| Era                        | Characteristics                       |
| -------------------------- | ------------------------------------- |
| Early (FORTRAN, COBOL)     | Fixed column comments                 |
| Middle (Pascal, C)         | Block comments                        |
| Modern (C++, Java, Python) | Line + block + documentation comments |

Modern languages prioritize flexibility and readability over fixed formatting.

---

### Key Points on Comments

* Line comments → simple and widely used
* Block comments → span multiple lines but may cause nesting issues
* Most languages avoid nested comments
* Documentation comments generate API docs
* Consistent commenting improves readability

---

# Tokens and White Spaces

## 1. Tokens

A **token** is the smallest meaningful unit in a program — like a word in English.

Examples:

| Category    | Examples                |
| ----------- | ----------------------- |
| Keywords    | `if`, `while`, `return` |
| Operators   | `+`, `-`, `==`          |
| Identifiers | `count`, `totalSum`     |
| Literals    | `42`, `3.14`, `"hello"` |
| Separators  | `;`, `()`, `{}`         |

During **lexical analysis**, the compiler converts source code into tokens.

---

## 2. White Spaces

White spaces improve readability and separate tokens.

Common types:

* Space (` `)
* Tab (`\t`)
* Newline (`\n`)
* Carriage return (`\r`)

Most white space is ignored by compilers, except where syntax requires it.

---

## 3. Blank Space Treatment

Languages differ in how they treat spaces.

### Blanks Not Significant (e.g., early Fortran)

* Multiple spaces collapsed
* Spaces inside identifiers allowed
* Can cause ambiguity

### Blanks Significant (most modern languages)

* Required to separate tokens
* `xy` ≠ `x y`
* Clearer parsing

---

## 4. Classic Fortran Example

```
DO 5 I = 1.25
DO 5 I = 1, 25
```

Though similar, they mean different things.

* `DO 5 I = 1.25` → Assignment to variable `DO5I`
* `DO 5 I = 1, 25` → Loop from 1 to 25

Because spaces were ignored, the compiler had to read ahead to detect whether it was a decimal (`.`) or a comma (`,`).

This made parsing complex and error-prone.

---

## 5. Modern Language Design

Most modern languages:

* Treat spaces as token separators
* Collapse multiple spaces into one
* Avoid ambiguity

### Python (Whitespace-Sensitive)

```python
if x > 0:
    print("Positive")
```

Indentation defines blocks — white space is syntactically meaningful.

### C/Java

```c
int x = 1 + 2;
```

Spaces improve readability but don’t affect logic (except separating tokens).

---

## Key Takeaways

* **Tokens** are the basic lexical units of programs.
* **White space** separates tokens and improves readability.
* Early languages often ignored spaces, causing ambiguity.
* Modern languages use clearer, consistent spacing rules.
* Python makes indentation part of syntax.

Understanding tokens and white space helps you:

* Write clearer code
* Debug syntax errors
* Understand compiler behavior
* Appreciate language design decisions

---

## Noise Words, Delimiters, and Format Styles

### 1. Noise Words

**Noise words** are optional words added for readability without changing meaning.

**COBOL Example:**

```cobol
GO TO PROCEDURE-NAME.
GO PROCEDURE-NAME.
```

Both are equivalent; `TO` is optional.

**Purpose:**

* Improve readability
* Make code more English-like

**Trade-off:**

* ✔ More readable
* ✘ More verbose and potentially inconsistent

Modern languages generally avoid noise words to keep syntax concise.

---

## 2. Delimiters

**Delimiters** mark boundaries in code (like punctuation in English).

### Example (PHP)

```php
<?php
$x = 5;          // ; ends statement
if ($x > 0) {    // { starts block
    echo "OK";
}                // } ends block
?>
```

Types of delimiters:

* **Statement:** `;`
* **Block:** `{ }`
* **Grouping:** `( )`, `[ ]`, `{ }`
* **Structural:** `:`, `.`

### Python Examples

```
( )  function calls
[ ]  lists
{ }  dictionaries
:    start of block
=    assignment
+=   compound assignment
```

**Why delimiters matter:**

* Define structure and scope
* Help parsing
* Improve readability

---

## 3. Format Styles

### A. Free Format

Position on the line does not matter.

Example (C):

```c
int main(){int x=5;return x;}
```

Characteristics:

* Flexible layout
* Indentation optional (but recommended)
* Most modern languages follow this style

---

### B. Fixed Format

Specific columns have meaning.

Example (COBOL):

```
000700     DISPLAY 'HELLO'.
```

Characteristics:

* Strict column rules
* Originated in punch-card era
* Rigid but consistent

---

### C. Relative Position

Indentation is syntactically significant.

Example (Python):

```python
if x > 0:
    print("Positive")
```

Incorrect indentation causes errors.

---

## Format Comparison

| Feature              | Free    | Fixed | Relative |
| -------------------- | ------- | ----- | -------- |
| Column rules         | No      | Yes   | No       |
| Indentation required | No      | No    | Yes      |
| Flexibility          | High    | Low   | Moderate |
| Examples             | C, Java | COBOL | Python   |

**Evolution:**
Fixed → Free → Relative indentation-based systems.

---

# Data Types

## Why Data Types?

Memory stores only bits:

```
100...101
```

This could represent:

* A number
* A character
* An instruction

Without a **data type**, we cannot interpret the bits correctly.

---

## What is a Data Type?

A data type consists of:

1. **A set of values**
2. **A set of operations**

Example:

* `boolean` → values: `true`, `false`
* operations: `AND`, `OR`, `NOT`

Different languages vary in:

* Available types
* Allowed operations
* Storage and enforcement rules

---

## Language Classification (By Type Checking)

### Untyped

* Machine code, Assembly
* No type checking

### Statically Typed

* C, Java
* Type checking at compile time

### Dynamically Typed

* Python, PHP, Scheme
* Type checking at runtime

**Difference:**
Static → checked before running
Dynamic → checked while running

---

# Types of Data and Operations

## Sources of Types/Operations

1. **Hardware**

   * Basic integer arithmetic

2. **Language Built-in**

   * Primitive types, basic operators

3. **Standard Libraries**

   * `Math.sqrt()`

4. **Third-party libraries**

   * External modules

---

## Programmer-Constructed Elements

### Operations

* As functions
* As inline code

### Data Organization

* **Primitive types:** `int`, `float`, `char`
* **Collections:** arrays, lists

---

## Type Conversion

### Type Promotion (Automatic)

```
2 + 3.0 → 5.0
```

`2` becomes `2.0` automatically.

### Type Casting (Explicit)

```
(int)3.7 → 3
```

Manual conversion; may lose information.

---

## Function Signatures

Example:

```c
float sub(int x, float y)
```

Signature notation:

```
sub: int × float → float
```

Meaning:

* Takes `int` and `float`
* Returns `float`

The compiler needs **signatures** to check correctness, but not the full function body during translation.

---

## Primitive vs User-Defined Types

### Primitive Types

Built into the language:

* `int`
* `float`
* `char`
* `boolean`

### User-Defined Types

Created using language features:

* Classes
* Structures
* Records

Example:

```java
class Student {
    String name;
    int age;
}
```

Primitive types are basic building blocks; user-defined types model real-world concepts.

---

# Final Key Points

* **Noise words** improve readability but increase verbosity.
* **Delimiters** define program structure and scope.
* **Format styles**: Free, Fixed, and Relative indentation-based.
* **Data types** define values + operations.
* **Static vs Dynamic typing** differs by when type checking occurs.
* **Type promotion** is automatic; **casting** is explicit.
* **Primitive types** are built-in; **user-defined types** extend the language.

These concepts explain how languages structure programs, enforce correctness, and balance readability with flexibility.

## Different Types of Data Objects

### 1. Elementary (Primitive) Data Objects

* Manipulated as a **single unit**
* Stored in **fixed-size memory**
* Atomic (cannot be broken into smaller parts)

Example:

* `int`, `float`, `char`, `boolean`
* An integer typically uses 4 bytes

**Idea:** One value, fixed size, handled as a whole.

---

### 2. Data Structures (Structured / Non-scalar)

* **Collections** of multiple data objects
* Memory size may be **variable**
* Components can be accessed individually

Examples:

* Arrays
* Records / Structs
* Objects

**Idea:** Multiple values grouped together.

---

# Primitive (Elementary) Data Types

### Characteristics

* Not defined in terms of other types
* Provided by all languages
* Usually **ordered sets**
* Values are **comparable**

Example (integers):

```
... -2, -1, 0, 1, 2 ...
```

You can compare values (`5 < 10`).

Common primitive types:

* Integer
* Boolean
* Character
* Real (floating point)

---

# Simple Data Types Across Languages

### C / C++

* Integers: `short`, `int`, `long`
* Reals: `float`, `double`
* `char`
* Pointers

### Java

* `boolean`
* `byte`, `short`, `int`, `long`
* `float`, `double`
* `char`
* No explicit pointers

### Python

* `int`
* `float`
* `bool`
* `complex`
* Everything is an object

**Observation:** Concepts are similar; naming and implementation differ.

---

# Structured (Non-Scalar) Data Types

### Key Idea

Structured types are built from **components**.

* **Component types** define the structure
* **Component values** form a specific instance

### Examples

**Array (same type components):**

```python
numbers = [1, 2, 3]
```

**Record/Struct (different types):**

```c
struct Student {
    char name[50];
    int age;
    float gpa;
};
```

**Type = blueprint**
**Value = actual data**

---

# Specification of Data Types

Three approaches:

### 1. Explicit Declaration (C-style)

```c
int age;
```

Programmer specifies the type.

✔ Clear, strong checking
✘ More typing

---

### 2. Default Declaration (FORTRAN-style)

* Default rules assign types
* Example: variables starting with I–N are integers

Less explicit, can cause mistakes.

---

### 3. Implicit Declaration (PHP/Perl-style)

```php
$x = 5;
```

Type inferred from assigned value.

✔ Flexible
✘ Errors may appear later

---

# Declarations and Storage Locations

Variables may be stored in different memory areas:

* **Registers** (fastest, limited)
* **Stack** (local variables)
* **Heap** (dynamic memory)
* **Static memory** (global variables)

Example (C):

```c
register int counter;
```

Specifying location can influence performance (though modern compilers optimize automatically).

---

# Implementation of Elementary Data Types

Implementing a type requires:

### 1. Storage Size

* `int` → typically 4 bytes
* `char` → 1 byte

### 2. Representation

* Integers → two’s complement
* Reals → floating-point (IEEE 754)
* Characters → ASCII / Unicode

### 3. Operations

* Addition, comparison, conversion algorithms

Example:

```c
int a = 5;
int b = 3;
int c = a + b;  // CPU performs binary addition
```

---

# What a Declaration Tells the Compiler

Example:

```c
int age;
```

Provides:

### 1. Attributes

* Type: integer
* Name: age

### 2. Value Range

* Allowed values (e.g., ±2 billion)

### 3. Allowed Operations

* Arithmetic
* Comparison

This helps the compiler:

* Allocate memory
* Select correct machine instructions
* Detect type errors

---

# Benefits of Specifying Data Types

### 1. Type Checking

* **Static:** Errors detected at compile time (C, Java)
* **Dynamic:** Errors detected at runtime (Python)

### 2. Operation Selection

Operator overloading depends on type:

```python
3 + 5        # Addition
"3" + "5"    # Concatenation
```

### 3. Storage Management

* Determines size
* Controls allocation
* Defines variable lifetime

### 4. Storage Representation

* Binary format
* Location (register, stack, heap)

---

# Key Summary

* **Elementary types:** Single value, fixed size
* **Structured types:** Collections of components
* **Declarations:** Explicit, default, or implicit
* **Implementation requires:** size, representation, operations
* **Declarations inform compiler about:** attributes, values, operations
* **Benefits:** error detection, correct operations, efficient memory use

Data types define how memory bits are interpreted, stored, and manipulated — making reliable programming possible.

# Data Types Explained Simply

## 1. Abstract Data Types (ADT)

An **Abstract Data Type (ADT)** defines:

* A **set of values**
* A **set of operations** on those values

It focuses on *what* a type does, not *how* it is implemented.

---

## 2. Why Data Types?

Memory stores only bits:

```
[100...101]
```

Those bits could represent:

* A number
* A character
* An instruction

Without a data type, the bits have **no meaning**.
A data type tells the system how to interpret them.

---

## 3. What is a Data Type?

A data type consists of:

1. **Values** (what it can store)
2. **Operations** (what you can do)
3. **Tests** (comparisons you can make)

### Example: Integer

* Values: `{..., -1, 0, 1, 2, ...}`
* Operations: `+`, `-`, `*`, `/`
* Tests: `<`, `>`, `==`

### Example: Boolean

* Values: `{true, false}`
* Operations: `AND`, `OR`, `NOT`

Mathematically, a data type is like an **algebra**:

```
Type = Set of values + Functions on that set
```

---

## 4. Implementation of ADT

Data types can be implemented in:

### Hardware

* Built into CPU circuits
* Very fast
* Example: integer addition

### Software

* Implemented using program code
* More flexible
* Example: strings, lists

Most systems use both.

---

## 5. Language Differences

Languages differ in:

* **Available types** (e.g., lists in Python, pointers in C)
* **Supported operations**
* **Storage management** (automatic vs manual)

Each language chooses types based on its design goals.

---

# Data Types: Sources and Signatures

## 1. Where Types and Operations Come From

### Hardware

* Integer arithmetic
* Basic logical operations

### Language Built-in

* Strings, lists
* Memory management

### Standard Libraries

* Math functions
* File handling
* Date/time utilities

### Third-Party Libraries

* Specialized tools (e.g., scientific or web frameworks)

---

## 2. Constructed by the Programmer

Programmers create operations in two ways:

### Functions (Reusable)

```python
def calculate_tax(amount):
    return amount * 0.08
```

Reusable and organized.

### In-line Code (One-time use)

```python
total = price1 + price2
tax = total * 0.08
```

Direct and simple.

---

## 3. Signature of Operators

Example in C:

```c
float sub(int x, float y)
```

Signature notation:

```
sub: int × float → float
```

Meaning:

* Inputs: `int` and `float`
* Output: `float`

A signature defines:

* Function name
* Input types
* Return type

---

## 4. What the Compiler Needs

During compilation, the compiler needs:

✔ **Signatures** (input and output types)
✘ Not the full implementation

This allows it to:

* Check argument types
* Verify correct usage

Built-in operators already have known signatures.

---

## 5. Primitive vs User-Defined Data Types

### Primitive Types

Built into the language:

* `int`
* `float`
* `char`
* `boolean`

They are basic building blocks.

---

### User-Defined Types

Created by programmers to model real-world concepts.

Example:

```python
class Student:
    def __init__(self, name, age, gpa):
        self.name = name
        self.age = age
        self.gpa = gpa

    def has_honors(self):
        return self.gpa >= 3.5
```

User-defined types:

* Combine primitive types
* Define custom operations

---

# Final Key Points

* Data types give meaning to raw bits in memory.
* A data type = values + operations + tests.
* Mathematically, types form an algebra (set + functions).
* Implementations may be hardware-based or software-based.
* The compiler uses **signatures** to enforce correctness.
* Primitive types are built-in; user-defined types model complex concepts.

Data types are the foundation that makes structured, reliable programming possible.

# Data Types Classification and Implementation (Simplified)

## 1. Types of Data Objects

### A. Elementary (Primitive) Types

* Single, indivisible value
* Fixed memory size
* Manipulated as one unit

Examples:

* `int`, `float`, `char`, `boolean`
* `42`, `3.14`, `'A'`, `true`

**Idea:** One value, fixed size.

---

### B. Structured (Non-scalar) Types

* Collection of multiple values
* Built from other types
* Memory may vary with size

Examples:

* Array: `[1, 2, 3]`
* Record/Struct: `{name: "John", age: 25}`

**Idea:** Multiple components grouped together.

---

## 2. Primitive Data Types

Primitive types are fundamental and not defined using other types.

### Common Categories

* **Integer:** `1, -5, 42`
* **Float (Real):** `3.14, -0.5`
* **Boolean:** `true, false`
* **Character:** `'A'`
* **Pointer** (in C/C++)

They are basic building blocks of all programs.

---

## 3. Key Characteristics of Primitive Types

* Present in every language
* Form **ordered sets** (values can be compared)
* Have minimum and maximum limits (in computers)

Examples:

* `5 < 10`
* `'A' < 'B'`
* `false < true`

Ordering enables sorting, searching, and comparisons.

---

## 4. Simple Types Across Languages

### C / C++

* `short`, `int`, `long`
* `float`, `double`
* `char`
* Pointers

### Java

* `byte`, `short`, `int`, `long`
* `float`, `double`
* `char`, `boolean`
* No pointers

### Python

* `int` (automatic large size)
* `float`, `complex`
* `bool`
* `str` (no separate char)

**Difference:**
C focuses on hardware control, Java on safety, Python on simplicity.

---

## 5. Structured Data Types

Structured types combine components.

### Array

* Components: same type
* Ordered by index

Example:

```
[10, 20, 30]
```

### Record / Struct

* Components: different types
* Named fields

Example:

```
{name: "Alice", age: 20, gpa: 3.8}
```

**Key Concept:**

* Type = component types (blueprint)
* Value = actual component data

---

## 6. Specification of Data Types

Languages declare types in three ways:

### 1. Explicit (C, Java)

```c
int x = 5;
```

Type must be stated.

### 2. Default (FORTRAN)

Type inferred from variable name.

### 3. Implicit (Python, PHP)

```python
x = 5
```

Type determined by assigned value and can change.

**Trade-off:**
Explicit → safer
Implicit → more flexible

---

## 7. Specifying Memory Location

Some languages allow hints for performance.

Example (C):

```c
register int counter;
```

* Suggests storing variable in CPU register (faster)
* Modern compilers usually optimize automatically

Memory hierarchy (fast → slow):
Registers → Cache → RAM

---

## 8. Implementation of Elementary Types

Implementing a type requires:

### 1. Storage Representation

* How many bytes?
* How are bits arranged?

Example:

* 32-bit integer
* IEEE 754 floating point

### 2. Algorithms

* How to add, subtract, compare, convert

Storage + Operations = Complete data type implementation.

---

## 9. What a Declaration Tells the Compiler

Example:

```c
int student_count = 25;
```

Provides:

### 1. Attributes

* Name: `student_count`
* Type: `int`
* Size and memory allocation

### 2. Possible Values

* Allowed range of integers
* Current value: 25

### 3. Allowed Operations

* Arithmetic (`+`, `-`, `*`, `/`)
* Comparisons (`<`, `>`, `==`)

This enables:

* Error checking
* Correct memory allocation
* Proper machine instruction selection

---

# Final Key Points

* Data objects are either **primitive** (single, fixed) or **structured** (composite, variable).
* Primitive types are ordered and comparable.
* Languages differ in type names and capabilities.
* Structured types are built from components.
* Types may be declared explicitly, by default rules, or implicitly.
* Implementing a type requires storage design and operational algorithms.
* Declarations inform the compiler about attributes, values, and allowed operations.

Data types define how data is stored, interpreted, and manipulated, forming the foundation of reliable programming.

# Type System (Simplified)

## 1. What is a Type System?

A **type system** is the rulebook of a programming language.

It defines:

### 1. Type Assignment

How expressions and variables get their types.

* C: `int x = 5;` → explicitly typed
* Python: `x = 5` → type inferred

### 2. Type Relationships

Rules about how types relate:

* **Type equivalence** → When are two types considered the same?
* **Type compatibility** → When can one type be used in place of another?

Example:
Can an `int` be used where a `float` is expected? Often yes (conversion).

---

# Benefits of Specifying Types

## 1. Type Checking

### Static (Compile-time)

Errors caught before running.

```java
int x = "hello";  // Error
```

### Dynamic (Run-time)

Errors detected during execution.

```python
5 + "hello"  # Runtime error
```

---

## 2. Operation Resolution

Operators may be overloaded.

Example:

```
5 + 3        → addition
"hi" + "!"   → concatenation
```

The type determines which operation is used.

---

## 3. Storage Management

Types determine:

* **Size** (e.g., `int` = 4 bytes)
* **Allocation** (stack or heap)
* **Lifetime** (scope-based or manual)

Example:

```c
int x;        // stack, 4 bytes
int* p = malloc(sizeof(int));  // heap
```

---

## 4. Storage Representation

Types define:

* Bit pattern (e.g., two’s complement, IEEE 754)
* Memory location (register, stack, heap)

Types are full instructions for how data is stored and used.

---

# Boolean Data Type (Simplified)

## 1. Basics

Boolean has only two values:

```
{ True, False }
```

### Operations

* **AND** → both must be true
* **OR** → at least one true
* **NOT** → opposite value

Truth examples:

```
True AND False → False
True OR False  → True
NOT True       → False
```

Mathematically:

* AND, OR: `S × S → S`
* NOT: `S → S`

---

## 2. Boolean Operators in Languages

| Operation | C/Java | Python | SQL   |      |      |
| --------- | ------ | ------ | ----- | ---- | ---- |
| AND       | `&&`   | `and`  | `AND` |      |      |
| OR        | `      |        | `     | `or` | `OR` |
| NOT       | `!`    | `not`  | `NOT` |      |      |

Different symbols, same logic.

---

## 3. Boolean Literals

* **Python:** Case-sensitive → `True`, `False` only
* **PHP:** Not case-sensitive → `true`, `TRUE`, `True` all valid

---

## 4. How Booleans Are Stored

Logically → needs 1 bit (0 or 1)

Practically → usually stored in a full byte (8 bits)

Common representation:

```
00000000 → False
00000001 → True
```

Some languages pack multiple booleans into single bytes for efficiency.

---

## 5. Packed Boolean Collections

To save memory:

* Packed arrays
* Bit fields (C/C++)
* Bit strings

Trade-off:

* Packed → saves space
* Unpacked → faster access

---

## 6. Boolean Expression Results

Languages differ in what `or` returns.

### PHP Style

Always returns boolean.

```
False or 123 → true
```

### Python Style

Returns actual value that determines truth.

```
False or 123 → 123
```

Python returns the first truthy value (or last falsy value).

---

## 7. PHP Example (Important Behavior)

```php
$name = "";
$name = ($name or fgets(STDIN));
echo $name;
```

Result: `1`

Reason:

* `$name` is empty → false
* `fgets()` returns non-empty string → true
* `false or true` → true
* `true` printed as `"1"`

PHP converts expression to boolean.

---

## 8. Python Equivalent

```python
name = ""
name = (name or input("Enter name: "))
print(name)
```

Result: prints entered name.

Reason:

* Python returns actual input string (not just `True`).

Common Python idiom:

```python
value = user_input or "default"
```

---

## 9. PHP Operator Precedence Trap

```php
$x = True;
$y = False;
echo ($z = $y or $x);
```

`=` has higher precedence than `or`.

Actual evaluation:

```
($z = $y) or $x
```

* `$z` becomes `False`
* `False or True` → True
* Prints `1`
* `$z` remains False

Correct version:

```php
$z = ($y or $x);
```

or

```php
$z = $y || $x;
```

---

# Final Key Points

* **Type system** defines how types are assigned and related.
* Types enable error detection, correct operation selection, and memory management.
* Boolean type has only two values with logical operations.
* Storage may use full bytes even though logically only 1 bit is needed.
* Expression behavior differs across languages (PHP vs Python).
* Operator precedence matters—use parentheses when unsure.

Types are not just labels—they control correctness, memory, and execution behavior.

# Character Types (Simplified)

## 1. What is a Character Type?

A **character type** stores a single character like `'A'`, `'3'`, `'$'`, or `'😀'`.

Computers store characters as **numbers (codes)**.

Example (ASCII):

* `'A'` → 65
* `'a'` → 97
* `'0'` → 48

### Main Encoding Systems

**ASCII**

* 7-bit (0–127)
* 128 characters
* English only

**Unicode**

* Universal system
* Over 1 million possible codes
* Supports all languages and emoji

ASCII is limited. Unicode is global.

---

## 2. Collating Sequence (Character Order)

A **collating sequence** is the order of characters in an encoding system.

It determines how characters are compared and sorted.

In ASCII:

```
Digits → Uppercase → Lowercase
```

Examples:
- `'A' < 'B'` (65 < 66)
- `'A' < 'a'` (65 < 97)
- `'1' < 'A'` (49 < 65)

Characters are compared by their numeric codes.

Important: In ASCII, uppercase letters come before lowercase letters.

---

## 3. Character Encoding Schemes (Differences)

| Encoding      | Bits per character | Characters Supported |
|---------------|-------------------|----------------------|
| ASCII         | 7 (stored in 8)   | 128 (English only)   |
| ISO 8859-1    | 8                 | 256 (Western Europe) |
| UCS-2         | 16                | 65,536 characters    |
| UTF-32        | 32                | All Unicode          |

### Key Differences

- **ASCII**: Basic English only.  
- **ISO 8859-1**: Adds European characters like é, ñ.  
- **UCS-2**: Fixed 16-bit Unicode (used by early Java `char`).  
- **UTF-32**: Fixed 32-bit, supports all Unicode but uses more space.  

Modern standard: **UTF-8**  
- Uses 1–4 bytes per character  
- ASCII-compatible  
- Most common encoding today  

More bits → more characters → more storage used.

---

# Numeric Data Types (Simplified)

## 1. Categories of Numeric Types

1. **Integer** – Whole numbers  
   Examples: 5, -2, 100  

2. **Floating-point** – Decimal numbers (approximate)  
   Examples: 3.14, 0.001  

3. **Decimal / Fixed-point** – Exact decimals  
   Used for money (e.g., 12.99 exactly)  

4. **Complex** – Real + imaginary part  
   Example: 3 + 4i  

---

## 2. Integer Type Basics

Integers are directly supported by CPU hardware.

Different sizes exist (example in C):

| Type | Typical Size | Approx Range |
|------|--------------|--------------|
| short | 2 bytes | -32K to 32K |
| int | 4 bytes | ~-2B to 2B |
| long | 8 bytes | very large |

Each type has a **maximum value**.  
Exceeding it causes **overflow**.

Example:
```

INT_MAX + 1 → overflow

```

---

## 3. How Integers Are Stored

### 1. Sign-Magnitude
- First bit = sign  
- Remaining bits = value  
- Problem: two zeros (+0 and -0)  
- Hard arithmetic  

### 2. 2’s Complement (Modern Standard)
- Positive → normal binary  
- Negative → invert bits + add 1  
- Only one zero  
- Easy arithmetic  

2’s complement is used in modern computers.

---

## 4. Converting to 2’s Complement

### Positive Numbers
1. Convert to binary  
2. Pad with leading zeros  

Example (8-bit):
```

+5 → 00000101

```

### Negative Numbers
1. Write positive version  
2. Invert all bits  
3. Add 1  

Example:
```

+5 → 00000101
Invert → 11111010
Add 1 → 11111011
So -5 = 11111011

```

---

## 5. Reading 2’s Complement

Look at the leftmost bit:

- 0 → Positive → read normally  
- 1 → Negative → invert all bits, add 1, make negative  

Example:
```

11111011
Invert → 00000100
Add 1 → 00000101 = 5
So value = -5

```

---

## 6. Integer Operations

### 1. Arithmetic
- `+`, `-`, `*`, `/`, `%`  
- Integer division truncates:
  - `7 / 2 = 3`  

### 2. Relational
- `<`, `>`, `==`, `!=`, `<=`, `>=`  
- Result is Boolean  

### 3. Assignment
- `=` stores value  
- Can return a value:
  - `x = y = 5`  

### 4. Bit Operations
- `&` (AND)  
- `|` (OR)  
- `^` (XOR)  
- `~` (NOT)  
- `<<` (left shift → multiply by 2ⁿ)  
- `>>` (right shift → divide by 2ⁿ)  

Used in low-level programming, networking, encryption, and optimization.

---

# Final Key Points

- Characters are stored as numeric codes (ASCII or Unicode).  
- Collating sequence defines comparison order.  
- UTF-8 is the modern standard encoding.  
- Integers use 2’s complement for negative numbers.  
- Leftmost bit determines sign in 2’s complement.  
- Integer operations include arithmetic, comparison, assignment, and bit manipulation.  

Even simple types like characters and integers rely on carefully designed encoding and binary representation inside the computer.

# Floating-Point Numbers (Simplified)

## 1. What Are Floating-Point Numbers?

Floating-point numbers store **decimal (real) values** like:

```
23.15, -45.123, 0.001, 3.14159
```

Language examples:

* C/C++ → `float`, `double`
* Java → `float`, `double`
* Python → `float`
* FORTRAN → `REAL`

### Important Idea: They Are Approximations

Computers use **binary (base 2)**.
Most decimal fractions (like 0.1) cannot be represented exactly in binary.

Example:

```
0.1 (decimal) → 0.0001100110011... (repeating in binary)
```

That’s why:

```
0.1 + 0.2 ≠ exactly 0.3
```

Floating-point values are very close, but not perfectly exact.

---

## 2. Decimal to Binary Conversion

To convert a decimal number:

### Integer Part

* Repeatedly divide by 2
* Read remainders backward

### Fractional Part

* Repeatedly multiply by 2
* Read integer parts forward

Example:

```
12.25
12 → 1100
0.25 → .01
Result: 1100.01
```

Some decimals convert exactly (like 0.25 = 2⁻²).
Most (like 0.1) repeat infinitely in binary.

---

## 3. Scientific Notation Format

Floating-point numbers use scientific notation:

```
± d × β^e
```

Where:

* Sign (±)
* Mantissa (digits)
* Base β (usually 2 in computers)
* Exponent e

Example (binary):

```
5.0 = 101.0 = 1.01 × 2²
```

---

## 4. Normalization

A number can be written in many scientific forms.
Normalization ensures **one standard form**.

### Rule:

The first digit must be non-zero.

In binary (base 2):

```
1.xxxx × 2^e
```

Example:

```
1011 → 1.011 × 2³
```

Why normalize?

* Ensures one unique representation
* Simplifies comparison and arithmetic

---

## 5. Hidden Bit Trick (Binary Only)

In binary normalized form, the first digit is **always 1**.

Since it is always 1, we **don’t store it**.
It is assumed automatically.

Example:

```
1.1011 → store only .1011
```

This saves 1 bit and increases precision.

Exception: **Zero** (cannot be normalized).

---

## 6. Normalizing Binary Numbers

### If number ≥ 1

Move binary point left → exponent positive.

Example:

```
1101.101 → 1.101101 × 2³
```

### If number < 1

Move binary point right → exponent negative.

Example:

```
0.00101 → 1.01 × 2⁻³
```

Goal: Always get `1.xxxx × 2^e`.

---

## 7. IEEE 754 Standard

Most computers use **IEEE 754** format.

### Single Precision (32-bit)

* 1 sign bit
* 8 exponent bits
* 23 mantissa bits
* Exponent bias = 127

### Double Precision (64-bit)

* 1 sign bit
* 11 exponent bits
* 52 mantissa bits
* Exponent bias = 1023

### Biased Exponent

Stored exponent = true exponent + bias
This avoids negative storage values.

Example:

```
True exponent = 2
Stored = 2 + 127 = 129 (single precision)
```

---

## 8. Representing Zero

Zero cannot be normalized.

IEEE 754 uses a special pattern:

```
Exponent = all 0
Mantissa = all 0
```

Both exist:

* +0 (sign = 0)
* -0 (sign = 1)

They compare equal:

```
+0 == -0 → true
```

But behave differently in some operations:

```
1/+0 → +∞
1/-0 → -∞
```

---

## Final Key Points

* Floating-point numbers represent real numbers approximately.
* Many decimal values cannot be represented exactly in binary.
* Normalized binary form is `1.xxxx × 2^e`.
* The leading 1 is hidden (not stored).
* IEEE 754 defines 32-bit (float) and 64-bit (double) formats.
* Zero, infinity, and NaN use special patterns.

Floating-point arithmetic is powerful, but always remember: **it works with approximations, not exact decimals.**

# Floating-Point Representation: Quizzes and Limitations (Simplified)

## 1. Normalizing Binary Numbers

### Rule

Move the binary point until the number becomes:

```
1.xxxxx × 2^e
```

* Move left → exponent positive
* Move right → exponent negative

### Examples

1. `001101.101`
   Ignore leading zeros → `1101.101`
   Normalize → `1.101101 × 2³`

2. `.00011011`
   Move point 4 places right → `1.1011 × 2⁻⁴`

Normalization ensures a single standard form.

---

## 2. Represent 13.75 in IEEE 754 (Single Precision)

### Step 1: Convert to Binary

```
13 → 1101
0.75 → .11
13.75 → 1101.11
```

### Step 2: Normalize

```
1101.11 = 1.10111 × 2³
```

### Step 3: IEEE 754 Fields

* Sign = 0 (positive)
* True exponent = 3
* Bias = 127
* Stored exponent = 3 + 127 = 130 → `10000010`
* Mantissa = `10111` (pad to 23 bits)

### Final 32-bit Pattern

```
0 10000010 10111000000000000000000
```

Full binary:

```
01000001010111000000000000000000
```

---

## 3. Decode IEEE 754 to Decimal

Given:

```
1 01111110 10000000000000000000000
```

### Step 1: Extract Fields

* Sign = 1 → negative
* Exponent = `01111110` = 126
* Mantissa = `.100000...`

### Step 2: Remove Bias

```
True exponent = 126 − 127 = -1
```

### Step 3: Add Hidden Bit

```
1.100000... = 1.1₂
```

Binary 1.1 = 1 + 0.5 = 1.5

### Step 4: Final Value

```
-1.1 × 2⁻¹
= -0.11₂
= -0.75₁₀
```

Important: `1.1` in binary ≠ `1.1` in decimal.

---

## 4. Limitation: Representing 0.1

Convert 0.1 to binary:

```
0.1 × 2 = 0.2 → 0
0.2 × 2 = 0.4 → 0
0.4 × 2 = 0.8 → 0
0.8 × 2 = 1.6 → 1
0.6 × 2 = 1.2 → 1
0.2 × 2 = 0.4 → repeats
```

Result:

```
0.1 = 0.0001100110011... (repeating)
```

It never terminates.
Since memory is finite, it must be rounded.

That’s why:

```
0.1 + 0.2 ≠ exactly 0.3
```

Floating-point numbers are approximate.

---

## 5. Practical Floating-Point Issues

### Hardware vs Software

* Modern CPUs have FPUs (fast floating-point hardware)
* Without hardware → slower software emulation

### Available Operations

* Arithmetic: +, −, ×, ÷
* Comparison: <, >, etc.
* Math functions: sin, cos, log, sqrt (usually library-based)

### The Equality Problem

Never compare floats directly:

```
if (a == b)   ❌
```

Use tolerance:

```
|a − b| < ε   ✔
```

Because rounding errors are unavoidable.

---

# Decimal (Fixed-Point) Data Types (Simplified)

## 1. What Is Fixed-Point?

Fixed-point numbers have a **fixed decimal position**.

Example (COBOL):

```
999V99
```

Means:

* 3 digits before decimal
* 2 digits after decimal
* Example: 123.45

Used for money and financial data because decimals are exact.

---

## 2. Storage Methods

### 1. Binary Coded Decimal (BCD)

Each decimal digit uses 4 bits.

Example:

```
1234 → 0001 0010 0011 0100
```

Exact but wastes space.

### 2. Integer + Scale Factor

Store number as integer.

Example:

```
12.99 → store 1299
Scale factor = 2 (divide by 100)
```

Efficient and common in financial systems.

---

## 3. Adding Different Scale Factors

Example:

```
100.421 (3 decimal places)
34.34   (2 decimal places)
```

Align decimal places:

```
34.34 → 34.340
```

Then add:

```
100.421 + 34.340 = 134.761
```

Always align decimal precision before arithmetic.

---

## 4. Limitations of Fixed-Point

### 1. Limited Range

Cannot easily represent:

* Very large numbers (e.g., 6 × 10²³)
* Very small numbers (e.g., 1 × 10⁻²⁴)

Floating-point handles these efficiently using exponents.

### 2. Storage Inefficiency (BCD)

BCD uses more bits than pure binary.

### 3. Precision Limits

With 2 decimal places:

```
0.014 → 0.01
0.006 → 0.01
```

Both round to same value → information lost.

Fixed-point has constant decimal precision but limited flexibility.

---

# Final Key Points

### Floating-Point

* Uses normalized form `1.x × 2^e`
* IEEE 754 defines structure (sign, biased exponent, mantissa)
* Cannot represent many decimals exactly (e.g., 0.1)
* Never compare floats with `==`

### Fixed-Point

* Exact decimal values
* Ideal for money
* Limited range
* May waste storage (BCD)
* Requires aligned decimal places for arithmetic

**Choose wisely:**

* Scientific computing → floating-point
* Financial systems → fixed/decimal types

# String Types Explained Simply

## 1. What Is a String?

A **string** is a sequence of characters, like `"Hello"` or `"123 Main St"`.

Two key design questions:

### 1. Is a string just a character array or a built-in type?

* **C, C++** → Strings are **arrays of characters** (manual memory handling).
* **Python, Java, C#** → Strings are **built-in types** (language manages memory).

### 2. Should string length be fixed or flexible?

* **Static (fixed length)** → Size decided at creation.
* **Limited dynamic** → Can vary up to a maximum.
* **Fully dynamic** → Can grow and shrink freely.
* **Null-terminated (C)** → Special character `'\0'` marks the end.

---

## 2. String Declarations

### C (Array-Based)

```c
char str[20] = "Hello";
```

* Fixed-size array.
* Ends with `\0` (null terminator).
* You must manage size and avoid overflow.

### Python (Built-in Type)

```python
str = "Hello"
```

* No size declaration.
* Memory handled automatically.
* Strings are immutable (cannot change in place).

**Key Difference**:
C gives low-level control but is error-prone. Modern languages prioritize safety and simplicity.

---

## 3. Common String Operations

| Operation     | C          | Python      |
| ------------- | ---------- | ----------- |
| Copy          | `strcpy()` | Assignment  |
| Concatenate   | `strcat()` | `+`         |
| Compare       | `strcmp()` | `==`, `<`   |
| Length        | `strlen()` | `len()`     |
| Pattern Match | Regex      | `re` module |

Example (Python):

```python
s1 = "Hello"
s2 = "World"
result = s1 + " " + s2
length = len(result)
```

**Regular Expressions Example**
`[A-Za-z][A-Za-z\d]+` → Starts with a letter, followed by letters or digits.

---

## 4. Substrings and Formatting

### Substring

```python
text = "Hello, World!"
text[0:5]   # "Hello"
```

### String Formatting (Interpolation)

```python
name = "Alice"
age = 25
f"Name: {name}, Age: {age}"
```

* **Single quotes (Perl example)** → Literal text.
* **Double quotes** → Variables are evaluated.

---

## 5. String Length Strategies

### 1. Static Length Strings

* Fixed size.
* Unused space is padded.
* Simple but wastes memory.
* Used in early languages like FORTRAN.

### 2. Limited Dynamic Strings

* Maximum length defined.
* Stores current length separately.
* Efficient but still limited.
* Used in Pascal, VARCHAR fields.

### 3. Fully Dynamic Strings

* No practical fixed limit.
* Grow and shrink as needed.
* Memory allocated dynamically.
* Used in Python, Java, C#, JavaScript.
* Flexible but has memory overhead.

---

## 6. Dynamic Storage Approaches

### 1. Linked List of Characters

* Easy insert/delete in middle.
* Extra memory for pointers.
* Slower traversal.

### 2. Contiguous Memory (Array-Like)

* Characters stored together.
* Fast indexing.
* Insert/delete requires shifting.
* Most modern languages use this with smart resizing (e.g., doubling capacity).

---

## 7. Implementation Overview

### Static Strings

* Fixed length known at compile time.
* Only character data stored.

### Limited Dynamic

* Store:

  * Current length
  * Character data
  * Maximum length (from declaration)

### Fully Dynamic

* Store:

  * Current length
  * Capacity (allocated space)
  * Character data

---

## 8. C’s Null-Terminated Strings

C marks the end of a string using `\0`.

Example in memory:

```
H  e  l  l  o  \0
```

To calculate length, C scans until `\0`.

### Problems:

* Length calculation is slower.
* Easy to forget `\0`.
* Risk of buffer overflow.
* Can cause security vulnerabilities.

Modern languages avoid this by storing length explicitly.

---

## Final Summary

* Strings are sequences of characters.
* Length strategies:

  * Static (fixed)
  * Limited dynamic (bounded)
  * Fully dynamic (flexible)
* Storage methods:

  * Linked list (rare)
  * Contiguous memory (common)
* C uses null-termination.
* Modern languages use dynamic strings with stored length and smart memory management.

Different languages made different trade-offs:

* **C** → Performance and control.
* **Pascal** → Safety with limits.
* **Python/Java** → Flexibility and ease of use.

# Ordinal Data Types Explained Simply

## 1. What Are Ordinal Types?

**Ordinal types** are types whose values have a clear order.

Two kinds:

1. **Enumeration types**

   * Define your own named values.
   * Example: `Days = (Mon, Tue, Wed, Thu, Fri, Sat, Sun)`

2. **Sub-range types**

   * Restrict part of an existing type.
   * Example: `'A'..'Z'` or `1..10`

They are called *ordinal* because values have a sequence:

* `Mon < Tue`
* `'A' < 'B'`

Common uses:

* Loop variables (`for day in Mon..Fri`)
* Array indexes (`array[Mon..Sun]`)

---

## 2. Enumeration Types

Enumeration lets you define a new type with named constants in a specific order.

Example (Ada):

```ada
type Days is (Mon, Tue, Wed, Thu, Fri, Sat, Sun);
```

Internally, the compiler maps them to numbers:

```
Mon=0, Tue=1, Wed=2, ...
```

But you use the names, not the numbers.

Other examples:

* C: `enum Days {Mon, Tue, Wed, Thu, Fri, Sat, Sun};`
* Java: `enum Days {MON, TUE, WED, ...};`

**Why use enums?**
Instead of writing:

```c
if (day == 0)  // What is 0?
```

You write:

```c
if (day == MON)  // Clear meaning
```

---

## 3. Operations on Enumerations

Since enumeration values are ordered, you can:

* **Compare** → `Mon < Fri`
* **Assign** → `day := Tue`
* **Get successor** → `Succ(Tue) = Wed`
* **Get predecessor** → `Pred(Wed) = Tue`

Example loop:

```pascal
for day := Mon to Fri do
   Process(day);
```

This is clearer than using numbers like `0..4`.

---

## 4. Enums in Loops and Arrays

Enums make code more readable.

Instead of:

```pascal
for i := 0 to 4 do ...
```

You write:

```pascal
for day := Mon to Fri do ...
```

Arrays can also use enums as indexes:

```pascal
var Schedule: array[Mon..Sun] of String;
Schedule[Mon] := "Meeting";
```

Benefits:

* Clear meaning
* Safer indexing
* Self-documenting code

---

## 5. Enumeration in C

C handles enums differently.

```c
enum week {monday, tuesday, wednesday};
```

Internally:

```
monday=0, tuesday=1, wednesday=2
```

In C, enums are basically **integers with names**.

You can even do:

```c
today = 5;  // Allowed, even if invalid logically
```

So:

* **Pascal/Ada** → True new type (type-safe)
* **C** → Just integers (flexible but less safe)

---

## 6. Overloaded Literal Problem

Problem: Same name appears in two enums.

```pascal
Type Days = (Mon, Tue, Sun);
Type holyDays = (Sat, Sun);
```

Now `Sun` is ambiguous.

Languages solve this differently:

1. **Pascal** → Forbid overlapping names.
2. **Ada/Java/C#** → Allow overlap, but require qualification:

   ```ada
   Days.Sun
   holyDays.Sun
   ```
3. **Some languages** → Infer from context.

---

## 7. Advantages of Enumeration Types

### 1. Readability

```c
if (light == GREEN)
```

is clearer than:

```c
if (light == 2)
```

### 2. Reliability

* Compiler prevents invalid values.
* Prevents mixing unrelated types.
* Avoids “magic numbers”.

Enums improve maintenance: change definition once, not everywhere in code.

---

## 8. Sub-Range Types

A **sub-range type** is a restricted portion of an existing ordinal type.

Examples (Pascal):

```pascal
type Age = 0..150;
type Month = 1..12;
type Uppercase = 'A'..'Z';
```

Why use sub-ranges?

* Documentation (`Score = 0..100`)
* Safety (compiler checks invalid values)
* Possible optimization

Example:

```pascal
Age := 25;   // OK
Age := 200;  // Error
```

---

## 9. Sub-Range Is Not a New Type

Sub-range types behave like the base type but with constraints.

Example:

```pascal
type Small = 1..10;
```

* Still behaves like an integer.
* Arithmetic works normally.
* Only assignments are range-checked.

C has no built-in sub-range types. You must manually check:

```c
if (age < 0 || age > 150) error();
```

---

## 10. Implementation of Ordinal Types

### Enumeration

* Stored as integers.
* Comparisons are numeric comparisons.

Example:

```
Red=0, Green=1, Blue=2
```

### Sub-Range

* Stored as base type.
* Compiler inserts range checks during:

  * Assignment
  * Parameter passing
  * Array indexing

Example (conceptually):

```pascal
if value < 0 or value > 100 then error;
```

Range checking improves safety but may reduce performance slightly.

---

## Final Summary

* **Ordinal types** are ordered types.
* Two kinds:

  * **Enumeration** → Named ordered constants.
  * **Sub-range** → Restricted portion of existing type.
* Enums improve readability and remove magic numbers.
* Sub-ranges improve safety by enforcing limits.
* Enums map to integers internally.
* Sub-ranges add automatic range checking.
* Pascal/Ada emphasize safety.
* C emphasizes flexibility and performance.

Ordinal types make programs clearer, safer, and easier to maintain.

# Structured Data Types – Arrays

## 1. Structured (Non-Scalar) Data Types

Structured types hold **multiple related values** together.

Common examples:

* **Arrays** – Numbered collection of same-type elements
* **Associative arrays** – Key–value collections
* **Records** – Group of different fields (like a form)
* **Files** – Data stored externally

---

## 2. Three Steps in Using Data Structures

```
1. Declare    → Specify the structure type
2. Create     → Allocate memory
3. Initialize → Assign starting values
```

Example (Java):

```java
int[] a;            // Declare
a = new int[10];    // Create
int[] b = {1,2,3};  // Declare + create + initialize
```

Java auto-initializes numeric arrays to 0.

---

## 3. What Is an Array?

An **array** is a homogeneous collection accessed by index.

```
scores:  [85, 92, 78, 95, 88]
index:     0   1   2   3   4
```

Access: `scores[2] → 78`

Key properties:

* Homogeneous (same type)
* Indexed access
* Finite size

---

## 4. Rectangular vs Jagged Arrays

**Rectangular (regular grid):**

```
[10,20,30]
[15,25,35]
```

(All rows same length)

**Jagged (irregular rows):**

```
[10,20]
[15,25,35,45]
```

(Rows may differ in size)

---

## 5. Array Address Calculation

To access `numbers[k]`:

```
address = base + (k - lower_bound) × element_size
```

Example:

* Base = 1000
* Element size = 4 bytes
* `numbers[2] = 1000 + (2×4) = 1008`

Address calculation happens at run time (unless fully static).

---

## 6. Design Issues in Arrays

Language designers decide:

1. **When is memory allocated?**

   * Compile-time (static)
   * Run-time (dynamic)

2. **Are indices checked?**

   * No checking (C, C++) → Faster, unsafe
   * With checking (Java, Ada) → Safer

3. **What is the starting index?**

   * C/Java → 0
   * Fortran → 1 (default)
   * Pascal/Ada → Custom bounds allowed

4. **How many dimensions?**

   * Most languages support multiple dimensions.

---

# Array Types (Based on Allocation)

## 1. Static Arrays

* Size fixed at compile time.
* Memory allocated once.
* Cannot change size.

**Pros:** Fast, simple
**Cons:** Possible wasted space

---

## 2. Stack-Dynamic Arrays

* Size determined at run time.
* Allocated on the **stack**.
* Automatically destroyed when function ends.

**Pros:** Efficient use of space
**Cons:** Limited size, temporary lifetime

Example (C local array):

```c
void f() {
    int arr[100];
}
```

---

## 3. Heap-Dynamic Arrays

* Allocated on the **heap**.
* Can grow/shrink during execution.
* Flexible lifetime.

Example (Python list):

```python
my_list = []
my_list.append(5)
```

**Pros:** Flexible, large capacity
**Cons:** Slower, more overhead

---

## 4. Stack vs Heap Summary

| Feature    | Stack          | Heap                  |
| ---------- | -------------- | --------------------- |
| Size       | Small          | Large                 |
| Speed      | Faster         | Slower                |
| Management | Automatic      | Manual / dynamic      |
| Lifetime   | Function scope | Programmer-controlled |

---

# Array Implementation & Fortran Arrays

## 1. Compile-Time vs Run-Time

* **Static arrays** → Addresses can be precomputed.
* **Dynamic arrays** → Address formula computed at run time.

Compiler stores array metadata (descriptor):

* Element type
* Bounds
* Base address

---

## 2. Multidimensional Arrays

Memory is 1D, so multidimensional arrays are flattened.

### Row-Major (C, Java)

Store row by row:

```
[1,2,3]
[4,5,6]
→ [1,2,3,4,5,6]
```

### Column-Major (Fortran)

Store column by column:

```
[1,2,3]
[4,5,6]
→ [1,4,2,5,3,6]
```

**Performance Tip:**

* In C → Last index changes fastest.
* In Fortran → First index changes fastest.

---

## 3. Fortran Arrays

Examples:

```fortran
real a(20)        ! indices 1..20
real b(0:19)      ! custom bounds
real d(3,5)       ! 2D array
```

Key points:

* Default index starts at 1.
* Uses parentheses `()`.
* Supports custom bounds.
* Uses column-major storage.
* No automatic bounds checking (older versions).

---

## 4. Array Slices

A **slice** is a subsection of an array.

Python example:

```python
arr = [10,20,30,40,50]
arr[1:4]   # [20,30,40]
```

Slices allow working with part of an array without copying everything manually.

---

# Final Summary

* Arrays are homogeneous indexed collections.
* Address calculation:
  `base + (index - lower_bound) × element_size`
* Allocation types:

  * **Static** (fixed)
  * **Stack-dynamic** (temporary)
  * **Heap-dynamic** (flexible)
* Multidimensional arrays use:

  * **Row-major** (C/Java)
  * **Column-major** (Fortran)
* Design trade-offs:

  * Speed vs Safety
  * Simplicity vs Flexibility

Arrays are foundational structures that balance memory layout, performance, and safety depending on language design choices.

# Dictionaries and Records

## 1. Dictionaries (Associative Arrays)

A **dictionary** stores data as **key → value** pairs.

```python
d = {'1': 123, 1: 'abc', 2: [1,2,3]}
d[1]   # returns 'abc'
```

Key features:

* Not position-based (no index numbers).
* Each key is unique.
* Values can be any type.
* Usually implemented using **hash tables** for fast lookup.

Examples:

* Phone book: Name → Phone number
* Student DB: ID → Student record

---

## 2. Records

A **record** groups related fields about one entity.

Example (Employee):

| Field      | Type    |
| ---------- | ------- |
| first_name | String  |
| last_name  | String  |
| id         | Integer |
| salary     | Float   |

Key properties:

* **Heterogeneous** (different data types allowed).
* Accessed by **field names**, not numeric indexes.

---

## 3. Record Definitions (Examples)

### COBOL (Hierarchical Levels)

```cobol
01 Employee-record
   02 Name
      05 First  PIC X(20)
      05 Middle PIC X(20)
      05 Last   PIC X(20)
   02 Hourly-Rate PIC 99V99
```

### Pascal/Ada (Nested Records)

```pascal
Employee_record : record
   name : record
      first  : string(1..20);
      middle : string(1..10);
      last   : string(1..20);
   end record;
   hourly_rate : float;
end record;
```

---

## 4. Referencing Record Fields

### Dot Notation (Most Common)

```pascal
Employee_record.name.middle
```

### COBOL Style

```
middle of Name of Employee-record
```

### Elliptical Reference

Shortened form when context is clear:

```pascal
with Employee_record do
   first := 'John';
```

Elliptical references reduce typing but can cause ambiguity.

---

## 5. Operations on Records

1. **Assignment**

   * Copy entire record at once.
2. **Comparison**

   * Field-by-field comparison (language dependent).
3. **Initialization**

   ```javascript
   employee = {name: "John", id: 123, salary: 50000};
   ```

---

## 6. Record Implementation

Records are stored **field by field in memory**.

Address calculation:

```c
address = base_address + field_offset
```

Compiler keeps a descriptor:

| Field      | Type       | Offset |
| ---------- | ---------- | ------ |
| first_name | String[20] | 0      |
| last_name  | String[20] | 20     |
| id         | Integer    | 40     |
| salary     | Float      | 44     |

Total size = sum of field sizes.

---

# Files

## 1. What Is a File?

A **file** is a permanent collection of records stored on disk (not RAM).

Properties:

* Stored in secondary storage.
* Much larger than memory.
* Persists after program ends.

---

## 2. Why Use Files?

1. **Input/Output**

   * Load data from disk.
   * Save program results.
2. **Scratch space**

   * Temporarily move data when RAM is insufficient.

---

## 3. What Cannot Be Stored?

* Mixed record types in same structured file.
* Raw memory addresses (pointers) — they become invalid when program restarts.

---

## 4. File Access Methods

### 1. Sequential Files

* Access records in order.
* Must read earlier records to reach later ones.
* Good for logs, simple text files.

### 2. Direct Access Files

* Use an index: Key → Location.
* Jump directly to desired record.
* Faster lookup.

### 3. Indexed Sequential Files

* Index points to record groups.
* Sequential search within group.
* Hybrid approach (efficient and compact index).

---

## 5. Searching Efficiency

Without index:

* Scan entire file (slow).

With index:

* Search small index.
* Jump directly to location.

Indexes significantly improve performance.

---

## 6. File Operations

Typical sequence:

```python
file = open("data.txt", "r")  # Open
data = file.read()            # Read
file.close()                  # Close
```

Main operations:

* Open
* Read / Write
* End-of-file test
* Close

Always close files to prevent data loss and resource leaks.

---

## 7. Buffering

Disk access is slow compared to RAM.

**Buffering solution:**

* Read/write data in blocks.
* Store temporarily in RAM buffer.
* Process from buffer (fast).
* Refill buffer when needed.

This reduces disk access frequency and improves performance.

---

# Final Summary

## Dictionaries

* Key–value mapping.
* Fast lookup using hashing.
* Keys unique.

## Records

* Group related fields with names.
* Stored sequentially in memory.
* Accessed using dot notation.

## Files

* Permanent external storage.
* Access types:

  * Sequential
  * Direct
  * Indexed sequential
* Require open → read/write → close.
* Buffering improves efficiency.

Dictionaries organize data by keys, records group related fields, and files store data permanently outside program memory.

# Pointer Types

## 1. What Is a Pointer?

A **pointer** stores a memory address, not the actual data.

```id="k3f8s1"
x (int) at 1000 → 42
ptr at 2000     → 1000
```

`ptr` holds **1000**, the address of `x`.
Dereferencing (`*ptr`) gives the value **42**.

Pointers enable:

* **Indirect addressing** (access data via its address)
* **Dynamic memory management** (allocate memory during execution)

---

## 2. Core Pointer Features

To support pointers, a language needs:

1. **Pointer type**

   ```c
   int* ptr;
   ```

2. **Allocation operator**

   ```c
   ptr = malloc(sizeof(int));
   ```

3. **Dereferencing operator**

   ```c
   *ptr = 42;
   ```

Special value:

* `NULL` → points to nothing.

---

## 3. Type Systems for Pointers

### Type-Specific (C, Pascal)

```id="l0a7zr"
int* p;   // Only points to int
```

* Compiler checks type compatibility.
* Safer (static checking).

### Untyped (Some dynamic languages)

* Pointer can reference any object.
* Type checked at runtime.
* More flexible, less safe.

---

## 4. Pointer Operations

### Assignment

```c
ptr = &x;   // store address of x
ptr = NULL; // no valid address
```

### Dereferencing

```c
*ptr        // value at stored address
```

Two interpretations:

* `ptr` → address
* `*ptr` → value at that address

---

# Pointers – Part 2

## 1. Dereferencing: Explicit vs Implicit

### Explicit (C, Pascal)

```c
*ptr = 20;
```

Programmer must manually dereference.

### Implicit (Some languages)

Assignment automatically follows pointer.

Explicit dereferencing is clearer but more error-prone.

---

## 2. Pointer Implementation

A pointer stores:

* Address of single value
* Address of array block
* Address of structured data

Conceptually:

```id="oe7zbx"
ptr → address → actual data
```

---

## 3. Addressing Methods

### Absolute Addressing

* Pointer stores real physical address.
* Fast access.
* Hard to relocate memory.

### Relative Addressing

* Pointer stores offset from base.
* Access = `base + offset`
* Slightly slower but more flexible.
* Useful for memory relocation and garbage collection.

---

## 4. Major Pointer Problems

### 1. Dangling Pointer

Pointer refers to memory that has already been freed.

```c
free(p1);
*p2 = 42;   // unsafe if p2 points to freed memory
```

Consequences:

* Crashes
* Data corruption
* Security risks

---

### 2. Memory Leak

Allocated memory becomes unreachable.

```c
p = malloc(sizeof(int));
p = malloc(sizeof(int));   // old memory lost
```

Consequences:

* Increasing memory usage
* Program slowdown or crash

---

## 5. Memory Deallocation Methods

### Explicit Deallocation (C, Pascal)

```c
free(ptr);
```

* Full control.
* Easy to forget → leaks.

### Garbage Collection (Java, Python)

```java
obj = null;
```

* Automatic memory cleanup.
* Safer.
* Uses extra CPU time.

---

# Final Summary

* A **pointer stores an address**, not data.
* Main purposes:

  * Indirect access
  * Dynamic memory allocation
* Key operations:

  * Assignment
  * Dereferencing
* Two addressing models:

  * Absolute (fast)
  * Relative (flexible)
* Common dangers:

  * Dangling pointers
  * Memory leaks
* Memory management styles:

  * Manual (explicit free)
  * Automatic (garbage collection)

Pointers are powerful tools for efficiency and dynamic data structures, but require careful memory management to avoid serious errors.

# Control Structures Explained

## 1. What Is Control Flow?

**Control flow** is the order in which program instructions execute.

Like a recipe:

* Follow steps in order (sequence)
* Choose based on a condition (selection)
* Repeat steps (looping)
* Jump to a subtask and return (function call)
* Stop completely (halt)

### Three Levels of Control Flow

1. **Within expressions**

   * Controlled by operator precedence and associativity
   * Example: `3 + 4 * 5` → multiplication first

2. **Among statements**

   * Order of execution of instructions

3. **Among program units**

   * Moving between functions/methods

---

## 2. Main Types of Control Flow

### 1. Unconditional Branch

* Always jump somewhere
* Example: `goto`, function call

### 2. Conditional Branch

* Jump only if condition is true
* Example: `if`, `switch`

### 3. Looping (Iteration)

* Repeat while condition holds
* Example: `while`, `for`

### 4. Functions/Subroutines

* Jump to code, then return

### 5. Unconditional Halt

* Stop execution
* Example: `exit()`

---

## 3. Machine-Level View: Program Counter

Every CPU has a **Program Counter (PC)**.

```
Address | Instruction
-----------------------
1000    | LOAD
1004    | ADD
1008    | STORE
1012    | JUMP 1000
```

Normally:

```
PC → next instruction
```

Control flow instructions:

```
Change the PC to another address
```

At machine level, everything reduces to:

* **Unconditional jump**
* **Conditional jump**

All high-level constructs (`if`, `for`, functions) compile down to jumps.

---

# Sequence Control Between Statements

## Three Fundamental Control Structures

All programs can be built using:

### 1. Sequence

```
A → B → C
```

### 2. Selection

```
If condition:
    Do this
Else:
    Do that
```

### 3. Iteration

```
While condition:
    Repeat
```

These are sufficient to build any program (structured programming principle).

---

## Compound Statements

A **compound statement** groups multiple statements as one unit.

Examples:

**C/Java**

```c
{
    statement1;
    statement2;
}
```

**Python**

```python
if condition:
    statement1
    statement2
```

When variable declarations are included, the compound statement becomes a **block**.

---

## Entry and Exit Issues

### Multiple Entry Points (Bad)

Jumping into the middle of a loop or `if` block:

* Skips initialization
* Creates confusing “spaghetti code”

### Multiple Exit Points (Usually OK)

Using:

* `break`
* `return`

Jumping **out** is generally acceptable.
Jumping **in** is dangerous.

---

# Explicit Sequence Control (`goto`)

## What Is Explicit Sequence Control?

Directly telling the program where to go next using `goto`.

Example:

```c
int i = 0;

start:
if (i >= 5) goto end;
printf("%d\n", i);
i++;
goto start;

end:
```

Equivalent structured version:

```c
while (i < 5) {
    printf("%d\n", i);
    i++;
}
```

Structured version is:

* Clearer
* Safer
* Easier to maintain

---

## Spaghetti Code

Too many `goto` jumps cause tangled control flow:

* Hard to read
* Hard to debug
* Hard to modify

Modern languages avoid or restrict `goto`.

---

# Forms of `goto`

## 1. Unconditional Branch

Always jumps:

```go
goto label
```

## 2. Conditional Branch

Jump only if condition holds:

```go
if A == 0 {
    goto zero_case
}
```

---

## Jumping INTO Control Structures (Dangerous)

Example (invalid in safer languages):

```
goto 1
for i := 1 to 10 do
begin
    1: writeln(i)
end
```

Problem:

* Loop initialization skipped
* Variables may be undefined
* Leads to bugs

---

## Language Approaches

### PL/I

* `goto` to variable labels
* Extremely flexible
* Very unsafe

### Pascal

* Allows `goto`
* Restricts jumping into nested structures
* Safer than PL/I

### Modern Languages

* Java, Python, JavaScript → No `goto`
* C/C++ → Keep but discourage
* Prefer structured constructs

---

# Final Summary

1. **Control flow** = Order of execution.
2. All programs can be built using:

   * Sequence
   * Selection
   * Iteration
3. At machine level, everything becomes jumps.
4. `goto` is powerful but dangerous.
5. Jumping into control structures causes bugs.
6. Structured programming improves clarity and safety.

Modern programming emphasizes readable, maintainable control flow rather than unrestricted jumping.

# Labels, Break, and Continue

## Labels

A **label** marks a position in code so control can jump to it (usually via `goto`).
It does nothing by itself.

Common forms:

* **Identifier labels (C):**

```c
start:
```

* **Number labels (FORTRAN, Pascal):**

```pascal
10:
```

* **Variable labels (PL/I – unsafe):**

```pl/i
GOTO LABEL_NAME;
```

Most languages use `:` after the label name.

---

## `break`

**Meaning:** Exit the current loop immediately.

```c
while (a < b) {
    if (error)
        break;
}
```

Effect:

* Leaves the loop.
* Execution continues after the loop.
* Clean and predictable.

---

## `continue`

**Meaning:** Skip the rest of the current iteration and start the next one.

```c
while (a < b) {
    if (skip)
        continue;

    printf("Work\n");
}
```

Effect:

* Jumps to next loop iteration.
* Does not exit the loop.

---

## Comparison

| Statement  | Purpose                       | Scope                    |
| ---------- | ----------------------------- | ------------------------ |
| `goto`     | Jump to any label in function | Unrestricted (dangerous) |
| `break`    | Exit current loop             | Controlled               |
| `continue` | Skip to next iteration        | Controlled               |

`break` and `continue` are safer, structured alternatives to `goto`.

---

# Structured Sequence Control

## What Is Structured Control?

Structured control means each control structure has:

* **One entry point**
* **One exit point**

This improves readability, debugging, and maintenance.

---

## Three Fundamental Structures

All programs can be built from:

1. **Sequence**

```plaintext
A → B → C
```

2. **Selection**

```c
if (condition) {
    ...
}
```

3. **Iteration**

```c
while (condition) {
    ...
}
```

---

# Selection Statements

## 1. Single-Way (`if`)

Execute block only if condition is true.

```c
if (age >= 18) {
    printf("Allowed\n");
}
```

Flow:

```
Check → If true execute → Continue
```

---

## 2. Two-Way (`if-else`)

Choose between two paths.

```c
if (score >= 50) {
    printf("Pass\n");
} else {
    printf("Fail\n");
}
```

Flow:

```
Check → Then OR Else → Continue
```

---

## 3. N-Way Selection

### If-Else Chain

```c
if (grade == 'A') ...
else if (grade == 'B') ...
else ...
```

### Switch

```c
switch (grade) {
    case 'A': ...
    case 'B': ...
    default: ...
}
```

Used when selecting among many alternatives.

---

# Why Structured Control Is Better

* Flow matches code order.
* No jumping into the middle of blocks.
* Easier to understand and debug.
* Avoids “spaghetti code”.

---

# Final Summary

* **Labels** mark positions for jumps.
* **`break`** exits loops early.
* **`continue`** skips to next iteration.
* Structured programming relies on:

  * Sequence
  * Selection
  * Iteration
* Each structured control has one entry and one exit.
* Modern programming favors structured control over unrestricted `goto`.

# Single-Way Selection

## What Is Single-Way Selection?

Single-way selection means:

> **Execute a block only if a condition is true.**
> If false, skip it and continue.

---

## Early FORTRAN Approach (Using `GO TO`)

```fortran
IF (.NOT. Condition) GO TO 30
Statement 1
Statement 2
...
30 CONTINUE
```

Logic:

* If condition is **false**, jump to 30 (skip statements).
* If condition is **true**, execute statements.

Example:

```fortran
IF (.NOT. (AGE .GE. 18)) GO TO 30
PRINT *, 'You can vote!'
30 CONTINUE
```

Issue:

* Uses **negative logic**.
* Harder to read.
* Relies on `GO TO`.

---

## ALGOL 60 Improvement (Structured `if`)

```algol
if (condition) then
begin
    Statement 1;
    Statement 2;
end;
```

Logic:

* If condition is **true**, execute block.
* If false, skip block.

This introduced:

* Clear structure
* Positive logic
* No `GO TO`

---

## Modern Syntax

All modern languages follow ALGOL’s style:

**C**

```c
if (condition) {
    statements;
}
```

**Python**

```python
if condition:
    statements
```

---

## Key Insight

* FORTRAN: “If NOT condition, skip.”
* ALGOL and modern languages: “If condition, do this.”

Positive logic is clearer and forms the foundation of structured programming.

---

# Two-Way Selection and the Dangling Else Problem

## What Is Two-Way Selection?

Two-way selection chooses between two paths:

```vb
If condition Then
    statements
Else
    statements
End If
```

Rules:

* Only one branch executes.
* Never both.

---

## The Dangling Else Problem

Example:

```pascal
If sum = 0 then
    if count = 0 then
        result := 0
    else
        result := 1
```

Question:
Which `if` does `else` belong to?

---

## Ambiguity

Two interpretations are possible:

1. `else` matches **inner if**
2. `else` matches **outer if**

This ambiguity is called the **dangling else problem**.

---

## Solutions

### 1. Nearest-If Rule (Most Common)

`else` pairs with the closest unmatched `if`.

Most languages (C, Java, etc.) use this rule.

---

### 2. Use Compound Statements

```pascal
if sum = 0 then
begin
    if count = 0 then
        result := 0
    else
        result := 1
end;
```

Blocks remove ambiguity.

---

### 3. Selection Closure (End Markers)

```ada
if sum = 0 then
    if count = 0 then
        result := 0
    else
        result := 1;
    end if;
end if;
```

Languages like Ada and VB use explicit `end if`.

Python uses indentation for clarity.

---

## Hardware-Level Implementation

High-level:

```c
if (x > 10)
    y = 20;
else
    y = 30;
```

Becomes:

1. Compare `x` and 10
2. If false, jump to else
3. Execute then-block
4. Jump past else
5. Execute else-block

Everything reduces to **conditional and unconditional jumps**.

---

# Final Summary

## Single-Way Selection

* Execute block only if condition is true.
* Modern form uses structured `if`.
* Positive logic improves readability.

## Two-Way Selection

* Choose between two paths using `if-else`.
* Only one branch runs.

## Dangling Else Problem

* Ambiguity in nested `if` statements.
* Solved by:

  * Nearest-if rule
  * Code blocks
  * End markers

Structured selection makes program behavior clear, predictable, and easier to maintain.

# Multiple Selection Constructs

## What Is Multiple Selection?

Multiple selection (multi-way branching) lets a program choose **one path from many** based on a value.

Key design questions:

1. Is the structure **encapsulated** in one block?
2. Does execution stay in one case or **fall through**?
3. Is there a **default/else** case?

---

## Early FORTRAN Approaches

### 1. Arithmetic IF (Scattered Design)

```fortran
IF (expression) 10, 20, 30
```

* Negative → jump to 10
* Zero → jump to 20
* Positive → jump to 30

Problems:

* Code scattered via labels
* Requires `GO TO`
* Hard to read and maintain

---

### 2. Computed GOTO

```fortran
GO TO (100, 200, 300), index
```

* Jumps based on `index`
* Still relies on labels
* Still not encapsulated

---

# Modern Multiple Selection

## C `switch`

```c
switch(index) {
    case 1: statement1; break;
    case 2: statement2; break;
    default: statementN;
}
```

Features:

* All cases inside one block
* Allows **fall-through** (unless `break` used)
* Flexible but potentially unsafe

Example (fall-through):

```c
case 'A':
    printf("Excellent\n");
case 'B':
    printf("Good\n");
    break;
```

If `'A'`, both lines print.

---

## Pascal `case` (Safer)

```pascal
Case grade of
    'A', 'B': writeln('Pass');
    'C': writeln('Conditional');
    else writeln('Invalid');
end;
```

Features:

* No fall-through
* Single entry, single exit
* Matches constant values only
* Safer and clearer

---

## Default / Else Clause

Handles unmatched values:

* C → `default`
* Pascal → `else`

Ensures predictable behavior.

---

## Implementation: Jump Tables

Compilers often use **jump tables**:

1. Evaluate expression.
2. Compute offset.
3. Jump directly to corresponding case.

Advantages:

* Fast (O(1) time).
* Efficient for many cases.

---

# Case vs Nested-If

## Nested-If

```c
if (x > 10 && y < 5) ...
else if (z == 0) ...
```

* Uses Boolean expressions.
* Can test multiple variables.
* Supports ranges and complex logic.

## Case / Switch

```c
switch(day) {
    case 1: ...
}
```

* Evaluates one expression.
* Matches exact values only.
* No complex Boolean conditions.

**Conclusion:**
A `case` cannot replace all nested `if` statements because it lacks Boolean flexibility.

---

# Iteration Statements (Loops)

## What Is Iteration?

Execute a statement/block **zero or more times**.

Every loop has:

* **Head** (control mechanism)
* **Body** (repeated code)

---

## Design Issues in Loops

1. **Control type**

   * Logical (`while`)
   * Counter-controlled (`for`)
   * Combination (C `for`)

2. **Test position**

   * Top-tested (`while`) → may run 0 times
   * Bottom-tested (`do-while`) → runs at least once

3. **Loop variable scope**

   * Visible inside only?
   * Also visible outside?

4. **Modifying loop variable**

   * Does changing it affect control?

Example (FORTRAN 77):

```fortran
DO 100 I = 1, 10, 2
   I = I * 2
100 CONTINUE
```

* Iteration count precomputed.
* Changing `I` does not affect number of iterations.

5. **Parameter evaluation**

   * Once at start (efficient)
   * Every iteration (flexible)

---

## Types of Iteration

1. **Simple repetition**
2. **Counter-controlled loops** (`for`)
3. **Logical loops** (`while`, `do-while`)
4. **User-controlled exit** (`break`, `continue`)
5. **Data-structure iteration** (`for item in list`)
6. **User-defined iteration** (custom iterators)

---

# Final Summary

* **Multiple selection** chooses one path from many.
* Early FORTRAN used scattered `GO TO`-based designs.
* Modern `switch/case` structures are encapsulated.
* C allows fall-through; Pascal prevents it.
* Jump tables make switch efficient.
* `case` matches values; nested-`if` evaluates Boolean expressions.
* Loops repeat code and involve design decisions about control, scope, and evaluation.

Understanding these design choices explains why languages differ in flexibility, safety, and efficiency.

# Simple Repetition Loops

## What Is Simple Repetition?

Simple repetition means:

> **Repeat a block exactly K times.**

Example in COBOL:

```cobol
PERFORM body K TIMES.
```

* `body` → code to repeat
* `K` → number of repetitions

The loop runs a fixed number of times using an internal counter.

---

## Main Design Issues

### 1. When Is K Evaluated?

#### Option A: Evaluated Once (Static — Common Choice)

```cobol
MOVE 5 TO K.
PERFORM body K TIMES.
```

Even if `K` changes inside the loop, it still runs 5 times.

**Advantages:**

* Predictable
* Efficient
* Safe from accidental infinite loops

Most languages follow this approach.

---

#### Option B: Re-evaluated Each Iteration (Dynamic)

If `K` is checked every time, modifying it inside the loop can change the number of iterations — even cause infinite loops.

**More flexible, but less safe.**

---

### 2. What If K ≤ 0?

Common behavior:

* If `K = 0` → loop runs 0 times.
* If `K < 0` → usually treated as 0 iterations.

Example (Python):

```python
for i in range(0):   # 0 iterations
    print(i)
```

---

## Key Idea

Most languages prefer:

* Evaluate loop count once.
* Skip loop if count ≤ 0.

This makes loops simple, predictable, and safe.

---

# Counter-Controlled Loops

## What Is a Counter-Controlled Loop?

A loop controlled by a **loop variable** with:

1. Initial value
2. Terminal value
3. Step size

These are called **loop parameters**.

Example (Pascal):

```pascal
for i := 1 to 10 do
    writeln(i);
```

Parameters:

* Initial = 1
* Terminal = 10
* Step = 1 (implicit)

Counting down:

```pascal
for i := 10 downto 1 do
    writeln(i);
```

Step = −1.

---

## Important Pascal Rule

After normal termination, the loop variable is **undefined**.

```pascal
for i := 1 to 5 do
    writeln(i);

writeln(i);  // Undefined in Pascal
```

Other languages differ:

* **C** → keeps last value (often 6 after `1..5`)
* **Python** → keeps last value (5)
* **Java** → depends on variable scope

---

## Design Considerations

1. **Type of loop variable** (usually integer)
2. **Step direction** (positive or negative)
3. **Parameter evaluation timing** (usually once at start)
4. **Modifying loop variable** (discouraged — confusing)
5. **Initial already past terminal** → loop skipped

---

## Core Idea

Counter-controlled loops make iteration explicit and predictable by clearly defining start, stop, and step values.

---

# FORTRAN DO Loops: Evolution

The `DO` loop syntax stayed similar, but its meaning changed.

---

## FORTRAN IV (Older Version)

```fortran
DO 100 I = 1, 5
100 CONTINUE
```

Characteristics:

* Parameters must be positive integers.
* Loop variable undefined after loop.
* Loop parameters evaluated once.
* Changing loop variable not allowed.
* Multiple entry/exit via `GO TO` allowed.

Strict and limited.

---

## FORTRAN 77 / 90 (Improved Version)

Same syntax:

```fortran
DO 100 I = initial, terminal, step
```

Major changes:

1. Parameters can be expressions and negative.
2. Supports integer, real, double types.
3. **Iteration count is pre-computed at start.**
4. Changing parameters inside does not affect loop count.
5. Loop variable retains last value after loop.

---

## Pre-Computed Iteration Count

At loop start:

```
count = MAX(INT((terminal - initial + step) / step), 0)
```

The loop then runs exactly `count` times.

Even if parameters change inside, execution count stays fixed.

This makes the loop stable and predictable.

---

# Final Summary

## Simple Repetition

* Repeat K times.
* K usually evaluated once.
* Loop skipped if K ≤ 0.

## Counter-Controlled Loops

* Defined by initial, terminal, and step.
* Clear and structured.
* Languages differ on post-loop variable behavior.

## FORTRAN Evolution

* FORTRAN IV: Strict, limited, undefined variable after loop.
* FORTRAN 77/90: More flexible, pre-computed iteration count, safer behavior.

The overall trend in language design moved from restrictive and unsafe control to predictable, structured, and robust iteration mechanisms.

# Counter-Controlled Loops in Pascal, Ada, and C/C++

## Pascal `for` Statement

### Syntax

```pascal
for variable := initial (to | downto) final do
    statement;
```

### Key Features

* **Ordinal types only** (integer, char, boolean, enumerated).
* **Loop variable cannot be modified** inside the loop.
* **Initial and final values evaluated once** at start.
* **Loop variable undefined after normal termination.**
* **Top-tested** (may execute 0 times).

Example:

```pascal
for i := 1 to 5 do
    writeln(i);
```

Strict and safety-oriented design.

---

## Ada `for` Statement

### Syntax

```ada
for variable in [reverse] discrete_range loop
    ...
end loop;
```

### Key Features

* Loop variable is **implicitly declared**.
* Scope exists **only inside the loop**.
* Cannot modify loop variable (treated as constant).
* Works with discrete ranges (`1..10`, `'A'..'Z'`).
* Supports `reverse` for backward iteration.
* Bounds evaluated once.

Example:

```ada
for i in 1..5 loop
    Put_Line(Integer'Image(i));
end loop;
```

Cleaner and safer than Pascal due to controlled scope.

---

## C / C++ `for` Statement

### Syntax

```c
for(init; test; increment)
    statement;
```

Example:

```c
for(i = 0; i < 10; i++)
    sum += array[i];
```

### Key Features

* All three parts optional (`for(;;)` = infinite loop).
* Multiple expressions allowed (comma operator).
* Test evaluated **every iteration**.
* Loop variable **can be modified** inside.
* Scope depends on declaration:

  * Declared outside → exists after loop.
  * Declared inside (`for(int i...)`) → local to loop (C99/C++).

Most flexible — and easiest to misuse.

---

## Comparison Summary

| Feature           | Pascal                   | Ada              | C/C++                  |
| ----------------- | ------------------------ | ---------------- | ---------------------- |
| Variable scope    | Outside, undefined after | Inside loop only | Depends on declaration |
| Modify variable   | Not allowed              | Not allowed      | Allowed                |
| Types allowed     | Ordinal only             | Discrete types   | Any type               |
| Bounds evaluation | Once                     | Once             | Test each iteration    |
| Reverse loop      | `downto`                 | `reverse`        | Manual (`i--`)         |
| Flexibility       | Low                      | Medium           | High                   |

**Trend:** Pascal and Ada prioritize safety; C/C++ prioritize flexibility.

---

# Logically Controlled Loops & Advanced Iteration

## Logically Controlled Loops

Controlled by a **Boolean expression** instead of a counter.

### Pre-Test Loop (`while`)

```c
while (condition) {
    body;
}
```

* Condition checked first.
* May execute 0 times.

### Post-Test Loop (`do-while`)

```c
do {
    body;
} while (condition);
```

* Body executes at least once.

**Important:**
Every counter loop can be rewritten as a logical loop, but not all logical loops can be expressed as counter loops.

---

## User-Located Loop Control (Manual Exit)

Some languages allow infinite loops with explicit exit conditions.

### Ada Example

```ada
loop
    ...
    exit when condition;
end loop;
```

Supports:

* Exit current loop
* Exit labeled outer loop
* Unconditional exit

Equivalent to `break` in C.

---

## `continue` vs `break` in C/C++

### `continue`

Skips rest of current iteration.

```c
if (value < 0)
    continue;
```

### `break`

Exits loop immediately.

```c
if (value < 0)
    break;
```

---

## Iteration Over Data Structures

Instead of counting, loop over elements in a collection.

### Python Example

```python
for fruit in fruits:
    print(fruit)
```

The loop:

1. Gets an iterator.
2. Repeatedly calls `next()`.
3. Stops when no elements remain.

---

## Iterators

An **iterator**:

* Returns next element.
* Remembers position.
* Signals completion.

Custom example (Python):

```python
class CountDown:
    def __init__(self, start):
        self.current = start
    def __iter__(self):
        return self
    def __next__(self):
        if self.current <= 0:
            raise StopIteration
        self.current -= 1
        return self.current + 1
```

Used in:

```python
for number in CountDown(5):
    print(number)
```

---

# Final Summary

* **Pascal**: Strict and safe; loop variable controlled tightly.
* **Ada**: Even safer; loop variable scoped and immutable.
* **C/C++**: Extremely flexible; supports both counting and logical patterns.
* **Logical loops** (`while`, `do-while`) are more general than counter loops.
* **Manual exits** (`exit`, `break`, `continue`) provide fine-grained control.
* **Data-structure iteration** and **iterators** power modern `foreach` loops.

Modern languages provide multiple loop styles because different problems require different control strategies.