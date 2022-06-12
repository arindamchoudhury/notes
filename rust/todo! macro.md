# The todo! macro
The todo! macro is used to identify unfinished code in the Rust program. The macro is helpful for prototyping, or when you want to indicate behavior that isn't complete.

```rust
fn main() {
    // Display the message "Hello, world!"
    todo!("Display the message by using the println!() macro");
}
```
When you compile code that uses the todo! macro, the compiler can return a panic message where it expects to find completed functionality:

```
   Compiling playground v0.0.1 (/playground)
    Finished dev [unoptimized + debuginfo] target(s) in 1.50s
     Running `target/debug/playground`
thread 'main' panicked at 'not yet implemented: Display the message by using the println!() macro', src/main.rs:3:5
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
```

