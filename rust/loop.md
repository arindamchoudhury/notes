Rust offers three loop expressions to make a program repeat a block of code:

- loop: Repeat, unless a manual stop occurs.
- while: Repeat while a condition remains true.
- for: Repeat for all values in a collection.

## Just keep looping
The loop expression creates an infinite loop. This keyword lets us repeat the actions in the expression body continuously. The actions repeat until we take some direct action to make the loop stop.

The most common way to stop a loop expression is by using the break keyword to set a break point:

When the program encounters the break keyword, it stops executing the actions in the body of the loop expression and continues to the next code statement.

The break keyword reveals a special feature of the loop expression. By using the break keyword, you can both stop repeating the actions in the expression body and also return a value at the break point.

```rust
let mut counter = 1;
// stop_loop is set when loop stops
let stop_loop = loop {
    counter *= 2;
    if counter > 100 {
        // Stop loop, return counter value
        break counter;
    }
};
// Loop should break when counter = 128
println!("Break the loop at counter = {}.", stop_loop);
```

## Loop a while

The while loop uses a conditional expression. The loop repeats as long as the conditional expression remains true. This keyword lets us execute the actions in the expression body until the conditional expression is false.

```rust
while counter < 5 {
    println!("We loop a while...");
    counter = counter + 1;
}
```

## Loop for these values

The for loop uses an iterator to process a collection of items. The loop repeats the actions in the expression body for each item in the collection. This type of loop repetition is called iterating. When all iterations are complete, the loop stops.

In Rust, we can iterate over any collection type, such as an array, vector, or hash map. Rust uses an iterator to move through each item in the collection from first to last.

The for loop uses a temporary variable as the iterator. The variable is implicitly declared at the start of the loop expression, and the current value is set with each iteration.

```rust
let big_birds = ["ostrich", "peacock", "stork"];

for bird in big_birds.iter() {
    println!("The {} is a big bird.", bird);
}

for number in 0..5 {
    println!("{}", number * 2);
}
```
