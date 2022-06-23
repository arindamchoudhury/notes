Rust includes an ownership system to manage memory. At compile time, the ownership system checks a set of rules to ensure that the ownership features allow your program to run without slowing down.

## Scoping rules
In Rust, like most other programming languages, variables are valid only within a certain scope. In Rust, scopes are often denoted by using curly brackets {}. Common scopes include function bodies and if, else, and match branches.

```rust
// `mascot` is not valid and cannot be used here, because it's not yet declared.
{
    let mascot = String::from("ferris");   // `mascot` is valid from this point forward.
    // do stuff with `mascot`.
}
// this scope is now over, so `mascot` is no longer valid and cannot be used.

```
The variable is valid from the point at which it's declared until the end of that scope.

In Rust, "variables" are often called "bindings". This is because "variables" in Rust aren't very variable - they don't change that often since they're unchangeable by default. Instead, we often think about names being "bound" to data, hence the name "binding". In this module, we'll use the terms "variable" and "binding" interchangeably.

## Ownership and dropping
Rust adds a twist to the idea of scopes. Whenever an object goes out of scope, it's "dropped." Dropping a variable means releasing any resources that are tied to it. For variables of files, the file ends up being closed. For variables that have allocated memory associated with them, the memory is freed.

In Rust, bindings that have things "associated" with them that they'll free when the binding is dropped are said to "own" those things.
```rust
{
    let mascot = String::from("ferris");
    // transfer ownership of mascot to the variable ferris.
    let ferris = mascot;
    // ferris dropped here. The string data memory will be freed here.
}
```

```rust
{
    let mascot = String::from("ferris");
    let ferris = mascot;
    println!("{}", mascot) // We'll try to use mascot after we've moved ownership of the string data from mascot to ferris.
}
```

```rust
fn process(input: String) {}

fn caller() {
    let s = String::from("Hello, world!");
    process(s); // Ownership of the string in `s` moved into `process`
    process(s); // Error! ownership already moved.
}
```
## Move semantics
Sometimes, though, we don't want the things associated with a variable to be dropped at the end of scope. Instead, we want to transfer ownership of an item from one binding to another.

A key thing to understand is that once ownership is transferred, the old variable is no longer valid. In our example above, after we transfer ownership of the String from mascot to ferris, we can no longer use the mascot variable.

In Rust, only one thing can ever own a piece of data at a time.

## Copying instead of moving
```rust
fn process(input: u32) {}

fn caller() {
    let n = 1u32;
    process(n); // Ownership of the number in `n` copied into `process`
    process(n); // `n` can be used again because it wasn't moved, it was copied.
}
```
Simple types like numbers are copy types. They implement the Copy trait, which means they're copied rather than moved. The same action occurs for most simple types. Copying numbers is inexpensive, so it makes sense for these values to be copied. Copying strings or vectors or other complex types can be very expensive, so they don't implement the Copy trait and are instead moved.

## Copying types that don't implement Copy
One way to work around the errors we saw above is by explicitly copying types before they're moved: known as cloning in Rust. A call to .clone will duplicate the memory and produce a new value. The new value is moved meaning the old value can still be used.

```rust
fn process(s: String) {}

fn main() {
    let s = String::from("Hello, world!");
    process(s.clone()); // Passing another value, cloned from `s`.
    process(s); // s was never moved and so it can still be used.
}
```

This approach can be useful, but it can make your code slower as every call to clone makes a full copy of the data. This method often includes memory allocations or other expensive operations.

## borrowing
We transfer ownership of a value by moving ownership from one variable to another. Ownership can't be transferred for types that implement the Copy trait, such as for simple values like numbers.

We can also explicitly copy values by using the cloning process. We call the clone method and get new values that are copied, which leaves the original values unmoved and free to still use.

Wouldn't it be nice to be able to allow functions and other variables to use certain data without fully owning it?

This type of functionality is available by using references. References allow us to "borrow" values without taking ownership of them.

```rust
let greeting = String::from("hello");
let greeting_reference = &greeting; // We borrow `greeting` but the string data is still owned by `greeting`
println!("Greeting: {}", greeting); // We can still use `greeting`
```


```rust
fn print_greeting(message: &String) {
  println!("Greeting: {}", message);
}

fn main() {
  let greeting = String::from("Hello");
  print_greeting(&greeting); // `print_greeting` takes a `&String` not an owned `String` so we borrow `greeting` with `&`
  print_greeting(&greeting); // Since `greeting` didn't move into `print_greeting` we can use it again
}
```

Borrowing allows us to use a value without taking full ownership.

## Mutate borrowed values
What happens if we try to mutate a value we borrowed?
```rust
fn change(message: &String) {
  message.push_str("!"); // We try to add a "!" to the end of our message
}

fn main() {
  let greeting = String::from("Hello");
  change(&greeting);
}
```
This code won't compile. If you take a closer look at the compiler error, you'll see a hint about changing our reference to be mutable by changing the type parameter from &String to &mut String. We also need to declare our original value as mutable:

```rust
fn main() {
    let mut greeting = String::from("hello");
    change(&mut greeting);
}

fn change(text: &mut String) {
    text.push_str(", world");
}
```
With & borrows, known as "immutable borrows," we can read the data but we can't change it. With &mut borrows, known as "mutable borrows," we can both read and write the data.

## Borrowing and mutable references

Now we get to the real core of Rust's memory management story. Immutable and mutable references differ in one other way that has radical effects on how we build our Rust programs. When borrowing a value of any type T, the following rules apply:

Your code must implement either of the following definitions, but not both at the same time:
- One or more immutable references (&T)
- Exactly one mutable reference (&mut T)

The following code doesn't have allowed definitions, so the compilation fails:

```rust
fn main() {
    let mut value = String::from("hello");

    let ref1 = &mut value;
    let ref2 = &mut value;

    println!("{}, {}", ref1, ref2);
}
```
We can even try to mix immutable references with mutable references, but the compiler will still complain:

```rust
fn main() {
    let mut value = String::from("hello");

    let ref1 = &value;
    let ref2 = &mut value;

    println!("{}, {}", ref1, ref2);
}

```

```rust

```
