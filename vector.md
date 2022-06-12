 vectors store multiple values that have the same data type. The size or length of a vector can grow or shrink at any time. The ability for the size to change over time is implied at compile time. As a result, Rust can't prevent you from accessing an invalid position in your vector like it does for out-of-bounds access in arrays.

 The syntax <vector><T> declares a vector type composed of a generic (not yet known) data type T. To actually create a vector, we use a concrete type like <vector>u32, a vector of type u32, or <vector>String, a vector of type String.

A common way to declare and initialize a vector is with the vec! macro. This macro also accepts the same syntax as the array constructor.

Vectors can also be created by using the Vec::new() method. This method of vector creation lets us add and remove values at the end of the vector. To support this behavior, we declare the vector variable as mutable with the mut keyword.

To add a value to the end of the vector, we use the push(<value>) method.

After the type of a vector is set to a concrete type, only values of that specific type can be added to the vector. If we try to add a value of a different type, the compiler returns an error.

To remove the value at the end of the vector, we use the pop() method.

We can access element values in the vector by using an index. The first element is at index 0 and the last element is at vector length - 1.

Because vector values are mutable, we can change a value in place by accessing the element value with the index.

As with arrays, we can't access an element in a vector with an index that's not in the allowed range. This type of expression for an array causes the compiler to return an error. For vectors, compilation passes, but the program enters an unrecoverable panic state at the expression and stops program execution.

```rust
// Declare vector, initialize with three values
let three_nums = vec![15, 3, 46];
println!("Initial vector: {:?}", three_nums);

// Declare vector, value = "0", length = 5
let zeroes = vec![0; 5];
println!("Zeroes: {:?}", zeroes);

let mut fruit = Vec::new();

// Push values onto end of vector, type changes from generic `T` to String
fruit.push("Apple");
fruit.push("Banana");
fruit.push("Cherry");
println!("Fruits: {:?}", fruit);

// Pop off value at end of vector
// Call pop() method from inside println! macro
println!("Pop off: {:?}", fruit.pop());
println!("Fruits: {:?}", fruit);

// Declare vector, initialize with three values
let mut index_vec = vec![15, 3, 46];
let three = index_vec[1];
println!("Vector: {:?}, three = {}", index_vec, three);

// Add 5 to the value at index 1, which is 5 + 3 = 8
index_vec[1] = index_vec[1] + 5;
println!("Vector: {:?}", index_vec);

```
