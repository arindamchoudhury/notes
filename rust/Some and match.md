The Rust standard library provides an Option<T> enum to be used when the absence of a value is a possibility. Option<T> is widely used in Rust code. It's useful for working with values that might exist or that might be empty.

In many other languages this would be modeled using null or nil, but Rust doesn't use null outside of code that interoperates with other languages. This means Rust is explicit about when a value is optional. While in many languages, a function that takes a String might actually take either a String or null, in Rust, that same function can only take actual Strings. If you want to model an optional string in Rust, you need to explicitly wrap it in an Option type: Option<String>.

```rust
enum Option<T> {
    None,     // The value doesn't exist
    Some(T),  // The value exists
}
```

The <T> part of the Option<T> enum declaration states that the type T is generic and will be associated with the Some variant of the Option enum.

As discussed in previous sections, None and Some are not types but rather variants of the Option<T> type. This means among other things that functions cannot take Some or None as arguments but only Option<T>.

In the preceding unit, we mentioned that trying to access a vector's non-existent index would cause the program to panic, but you could avoid that by using the Vec::get method, which returns an Option type instead of panicking. If the value exists at a specified index, it's wrapped in the Option::Some(value) variant. If the index is out of bounds, it would return a Option::None value instead.


```rust
let fruits = vec!["banana", "apple", "coconut", "orange", "strawberry"];

// pick the first item:
let first = fruits.get(0);
println!("{:?}", first);

// pick the third item:
let third = fruits.get(2);
println!("{:?}", third);

// pick the 99th item, which is non-existent:
let non_existent = fruits.get(99);
println!("{:?}", non_existent);
```

## Pattern matching

There's a powerful operator in Rust that's called match. You can use it to control the flow of your program by providing patterns. When match finds a matching pattern, it runs code that you supply with that pattern.

```rust
let fruits = vec!["banana", "apple", "coconut", "orange", "strawberry"];
for &index in [0, 2, 99].iter() {
    match fruits.get(index) {
        Some(fruit_name) => println!("It's a delicious {}!", fruit_name),
        None => println!("There is no fruit! :("),
    }
}
```

Whenever you use the match expression, keep the following rules in mind:

- match arms are evaluated from top to bottom. Specific cases must be defined earlier than generic cases or they'll never be matched and evaluated.
- match arms must cover every possible value that the input type could have. You'll get a compiler error if you try to match against a non-exhaustive pattern list.

## The if let expression

An if let operator compares a pattern with an expression. If the expression matches the pattern, the if block is executed. The nice thing about if let expressions is that you don't need all the boilerplate code of a match expression when you're interested in a single pattern to match against

```rust
let a_number: Option<u8> = Some(7);
match a_number {
    Some(7) => println!("That's my lucky number!"),
    _ => {},
}
```

```rust
let a_number: Option<u8> = Some(7);
if let Some(7) = a_number {
    println!("That's my lucky number!");
}
```

## Use unwrap and expect

You can try to access the inner value of an Option type directly by using the unwrap method. Be careful, though, because this method will panic if the variant is a None.

```rust
let gift = Some("candy");
assert_eq!(gift.unwrap(), "candy");

let empty_gift: Option<&str> = None;
assert_eq!(empty_gift.unwrap(), "candy"); // This will panic!
```

The expect method does the same as unwrap, but it provides a custom panic message that's provided by its second argument:

```rust
let a = Some("value");
assert_eq!(a.expect("fruits are healthy"), "value");

let b: Option<&str> = None;
b.expect("fruits are healthy"); // panics with `fruits are healthy`
```

Because these functions might panic, we don't recommend using them. Instead, consider either of the following approaches:

- Use pattern matching and handle the None case explicitly.
- Call similar non-panicking methods, such as unwrap_or, which returns a default value if the variant is None or the inner value if the variant is Some(value).


```rust
assert_eq!(Some("dog").unwrap_or("cat"), "dog");
assert_eq!(None.unwrap_or("cat"), "cat");
```
