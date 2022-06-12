An array is a collection of objects of the same type that are stored sequentially in memory. The length or size of an array equals the number of elements in the array. The size of an array can be specified in the code, or computed by the compiler.

At compile time, the signature of an array is defined as [T; size]:

- T is the data type for all elements in the array.
- size is a nonnegative integer that represents the array length.

The signature reveals two important characteristics about arrays:

- Every element of an array has the same data type. The data type never changes.
-  The size of an array is fixed. The length never changes.

Only one thing about an array can change over time: the values of the elements in the array. The data type remains constant and the number of elements (length) remains constant. Only the values can change.


An array can be defined in two ways:

- A comma-separated list of values, where the length isn't specified.
- The initial value followed by a semicolon, and then the array length.

In both cases, the content is enclosed in square brackets [].

The elements in an array are implicitly numbered starting from 0. We use indexing to access the elements in an array with the expression <array>[<index>]. For example, my_array[0] accesses the element at index 0 in the my_array variable. The expression returns the value of the array element at that index location.

```rust
// Declare array, initialize all values, compiler infers length = 7
let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];

// Declare array, initialize all values to 0, length = 5
let bytes = [0; 5];

// Get the first day of the week
let first = days[0];

// Get the second day of the week
let second = days[1];
```

If we try to access an element in our array with an index that's not in the allowed range, the compiler returns an error.
