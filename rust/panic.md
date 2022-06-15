Panicking is the simplest error handling mechanism in Rust.

You can use the panic! macro to panic the current thread. It prints an error message, frees resources, and then exits the program.

In general terms, you should use panic! when a program reaches an unrecoverable state meaning anything where there is absolutely no way to recover from the error.

Rust panics on some operations such as a division by zero or an attempt to access an index that isn't present in an array, a vector, or a hash map.

```rust
fn main() {
    panic!("Farewell!");

    let v = vec![0, 1, 2, 3];
    println!("{}", v[6]); // this will cause a panic!

}
```
