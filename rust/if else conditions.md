```rust
if 1 == 2 {
    println!("True, the numbers are equal."); //
} else {
    println!("False, the numbers are not equal.");
}
```

if blocks in Rust can also act as expressions. All execution blocks in the condition branches must return the same type for the code to compile.


```rust
let formal = true;
let greeting = if formal { // if used here as an expression
    "Good day to you."     // return a String
} else {
    "Hey!"                 // return a String
};
println!("{}", greeting)   // prints "Good day to you."

```
