We define an enum with variants similar to how we define different kinds of struct types. All the variants are grouped together in the same WebEvent enum type. Each variant in the enum isn't its own type. Any function that uses a variant of the WebEvent enum must accept all the variants in the enum. We can't have a function that accepts only the WEClick variant, but not the other variants.

## Define an enum with structs

A way to work around enum variant requirements is to define a separate struct for each variant in the enum. Then, each variant in the enum uses the corresponding struct. The struct holds the same data that was held by the corresponding enum variant. This style of definition allows us to refer to each logical variant on its own.

The following code shows how to use this alternate definition style. The structs are defined to hold the data. The variants in the enum are defined to refer to the structs.

```rust
// Define a tuple struct
struct KeyPress(String, char);

// Define a classic struct
struct MouseClick { x: i64, y: i64 }

// Redefine the enum variants to use the data from the new structs
// Update the page Load variant to have the boolean type
enum WebEvent { WELoad(bool), WEClick(MouseClick), WEKeys(KeyPress) }
```

## Instantiate an enum

Now let's add code to create instances of our enum variants. For each variant, we use the let keyword to make the assignment. To access the specific variant in the enum definition, we use the syntax <enum>::<variant> with double colons ::.

```rust
let we_load = WebEvent::WELoad(true);

// Instantiate a MouseClick struct and bind the coordinate values
let click = MouseClick { x: 100, y: 250 };

// Set the WEClick variant to use the data in the click struct
let we_click = WebEvent::WEClick(click);

// Instantiate a KeyPress tuple and bind the key values
let keys = KeyPress(String::from("Ctrl+"), 'N');

// Set the WEKeys variant to use the data in the keys tuple
let we_key = WebEvent::WEKeys(keys);

```
