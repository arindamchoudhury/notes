# Structs
A struct is a type that's composed of other types. The elements in a struct are called fields. Like tuples, the fields in a struct can have different data types. A significant benefit of the struct type is that you can name each field so it's clear what the value means.

To work with structs in a Rust program, first you define the struct by name and specify the data type for each field. Then, you create an instance of the struct with another name. When you declare the instance, you provide the specific values for the fields.

Rust supports three struct types: classic structs, tuple structs, and unit structs. These struct types support different ways to group and work with the data.

- Classic C structs are the most commonly used. Each field in the struct has a name and a data type. After a classic struct is defined, the fields in the struct can be accessed by using the syntax <struct>.<field>.
- Tuple structs are similar to classic structs, but the fields don't have names. To access the fields in a tuple struct, we use the same syntax as we do for indexing a tuple: <tuple>.<index>. As with tuples, the index values in the tuple struct start at zero.
- Unit structs are most commonly used as markers. We'll learn more about why unit structs are useful when we learn about Rust's traits feature.

The following code shows example definitions for the three varieties of struct types:

```rust
// Classic struct with named fields
struct Student { name: String, level: u8, remote: bool }

// Tuple struct with data types only
struct Grades(char, char, char, char, f32);

// Unit struct
struct Unit;
```
## Classic struct
Like a function, the body of a classic struct is defined inside curly brackets {}. Each field in the classic struct is given a name that's unique within the struct. The type for each field is specified with the syntax : <type>. The fields in the classic struct are specified as a comma-separated list <field>, <field>, .... A classic struct definition doesn't end with a semicolon.

A benefit of the classic struct definition is you can access the value for a struct field by name. To access the field value, we use the syntax <struct>.<field>.

## Tuple struct
Like a tuple, the body of a tuple struct is defined inside parentheses (). The parentheses immediately follow the struct name. There's no space between the struct name and the opening parentheses.

Unlike a tuple, the tuple struct definition contains only the data type for each field. The data types in the tuple struct are specified as a comma-separated list <type>, <type>, ....

## Instantiate a struct

```rust
// Instantiate classic struct, specify fields in random order, or in specified order
let user_1 = Student { name: String::from("Constance Sharma"), remote: true, level: 2 };
let user_2 = Student { name: String::from("Dyson Tan"), level: 5, remote: false };

// Instantiate tuple structs, pass values in same order as types defined
let mark_1 = Grades('A', 'A', 'B', 'A', 3.75);
let mark_2 = Grades('B', 'A', 'A', 'C', 3.25);

println!("{}, level {}. Remote: {}. Grades: {}, {}, {}, {}. Average: {}",
         user_1.name, user_1.level, user_1.remote, mark_1.0, mark_1.1, mark_1.2, mark_1.3, mark_1.4);
println!("{}, level {}. Remote: {}. Grades: {}, {}, {}, {}. Average: {}",
         user_2.name, user_2.level, user_2.remote, mark_2.0, mark_2.1, mark_2.2, mark_2.3, mark_2.4);

```
