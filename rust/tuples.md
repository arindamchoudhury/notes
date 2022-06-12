# Tuples

A tuple is a grouping of values of different types collected into one compound value. The individual values in a tuple are called elements. The values are specified as a comma-separated list enclosed in parentheses (<value>, <value>, ...).

A tuple has a fixed length, which is equal to its number of elements. After a tuple is declared, it can't grow or shrink in size. Elements can't be added or removed. The data type of a tuple is defined by the sequence of the data types of the elements.

The elements in a tuple can be accessed by index position starting from zero. This process is referred to as tuple indexing. To access an element in a tuple, we use the syntax <tuple>.<index>.

```rust
// Declare a tuple of three elements
let tuple_e = ('E', 5i32, true);

// Use tuple indexing and show the values of the elements in the tuple
println!("Is '{}' the {}th letter of the alphabet? {}", tuple_e.0, tuple_e.1, tuple_e.2);
```
