---
tags:
  - Resources_Summarized
---

2025-12-21 05:19 

# A half-hour to learn Rust

**Source material**: [A half-hour to learn Rust](https://fasterthanli.me/articles/a-half-hour-to-learn-rust)

**Tags**: [[Rust]], [[programming]]

---

## Core Rust Concepts

### Variable Bindings
Rust uses the **`let`** keyword to introduce variable bindings.
*   **Immutability**: By default, bindings are **immutable** and cannot be reassigned or have their interior mutated.
*   **Mutability**: Use **`mut`** to allow a variable's value to change.
*   **Shadowing**: You can declare a new variable with the same name as an existing one, "shadowing" the previous binding.
*   **The Underscore (`_`)**: A special name used to **discard** or "throw away" values, such as results from functions you don't need.

**Example:**
```rust
let x = 42; // immutable
let mut y = 5; // mutable
y = 6; 

let x = x + 1; // shadowing: the first x is no longer accessible
```

### Functions and Blocks
*   **Function Declaration**: Defined with **`fn`**. Return types are indicated by an arrow `->`.
*   **Expressions**: Almost everything in Rust is an expression, meaning it evaluates to a value.
*   **Implicit Return**: The last expression in a function (the **"tail"**) is returned automatically if the semicolon is omitted.

**Example:**
```rust
fn add(x: i32, y: i32) -> i32 {
    x + y // tail expression, returns automatically
}
```

---

## Data Types

### Structs
Used to create custom types with named fields.
*   **Struct Update Syntax**: Use `..` to initialize remaining fields from another struct instance.
*   **Destructuring**: You can break a struct apart into individual variables.

```rust
struct Vec2 { x: f64, y: f64 }

let v1 = Vec2 { x: 1.0, y: 2.0 };
let v2 = Vec2 { x: 3.0, ..v1 }; // x is 3.0, y is 2.0
let Vec2 { x, y } = v2; // destructuring into variables x and y
```

### Enums (Sum Types)
Enums allow a type to be one of several variants. Common examples include **`Option<T>`** (for values that might be missing) and **`Result<T, E>`** (for operations that might fail).
*   **Match**: Used to handle different enum variants exhaustively.

### Tuples
Fixed-length collections of different types.
```rust
let pair = ('a', 17);
let first = pair.0; // access via dot notation
```

---

## Memory and Ownership

### Ownership and Moving
In Rust, values have a single owner. When you assign a non-`Copy` value to a new variable or pass it to a function, the value is **moved**, and the original variable can no longer be used.

### Borrowing (References)
To use a value without taking ownership, you **borrow** it using references.
*   **Immutable References (`&T`)**: Allow reading but not modifying. You can have many at once.
*   **Mutable References (`&mut T`)**: Allow modification. You can only have **one** at a time to prevent data races.

| Feature          | Immutable Borrow (`&`)      | Mutable Borrow (`&mut`)               |
| :--------------- | :-------------------------- | :------------------------------------ |
| **Quantity**     | Multiple allowed            | Only one allowed                      |
| **Modification** | No                          | Yes                                   |
| **Co-existence** | Cannot co-exist with `&mut` | Cannot co-exist with any other borrow |

### Lifetimes
Lifetimes ensure that references do not outlive the data they point to.
*   **Elision**: In many cases, the compiler can infer lifetimes automatically (lifetime elision).
*   **'static**: A special lifetime that lasts for the entire duration of the program, common for string literals.

---

## Traits and Generics

### Traits
Traits define shared behavior that multiple types can implement.
*   **Orphan Rules**: You can implement your trait on any type, or any trait on your type, but you cannot implement a foreign trait on a foreign type.
*   **Deriving**: Common traits like `Clone`, `Copy`, `Debug` can be automatically implemented using `#[derive(...)]`.
*   **Marker Traits**: Traits like `Copy` indicate a type can be duplicated simply by copying bits, changing how assignment works (no move).

### Generics
Functions and structs can be generic over types (`<T>`).
*   **Turbofish (`::<>`)**: Used to explicitly specify concrete types for generic functions when the compiler cannot infer them.

---

## Best Practices & Tips

*   **Error Handling**: Prefer the **`?` operator** to concisely "bubble up" errors to the caller instead of using `match` or `if let` every time.
*   **Explicit Borrows**: When calling methods or functions, use `&` or `&mut` to make it clear that a value is being borrowed rather than moved.
*   **Clippy**: Rust tools like Clippy can suggest idiomatic improvements, such as using **struct literal shorthand** when a variable name matches a field name.
*   **Iterators**: Use the powerful iterator methods like `.filter()`, `.map()`, and `.flat_map()` to process collections cleanly in `for` loops.

---

## Quick Snippets

*   **Macros**: Distinguished by the `!` (e.g., `println!`, `vec!`, `panic!`).
*   **Slices**: References to a contiguous sequence of elements (e.g., `&str` is a string slice).
*   **Closures**: Anonymous functions that can capture their environment using `||` syntax.

**Metaphor for Understanding Ownership**: Think of Rust ownership like a **library book**. You can have many people in the room reading (immutable borrowing) the book at the same time, but if someone wants to underline or write in it (mutable borrowing), they must be the only person with the book. If you give the book away to a friend (moving), you no longer have it to read yourself. [Non-source metaphor]