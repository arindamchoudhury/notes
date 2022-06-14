The HashMap<K, V> type stores data by mapping each key K with its value V. While data in a vector is accessed by using an integer index, data in a hash map is accessed by using a key.

The hash map type is used in many programming languages for data items like objects, hash tables, and dictionaries.

Like vectors, hash maps are growable. The data is stored in the heap and access to the hash map items are checked at run time.

```rust
use std::collections::HashMap;
let mut reviews: HashMap<String, String> = HashMap::new();

reviews.insert(String::from("Ancient Roman History"), String::from("Very accurate."));
reviews.insert(String::from("Cooking with Rhubarb"), String::from("Sweet recipes."));
reviews.insert(String::from("Programming in Rust"), String::from("Great examples."));

// Look for a specific review
let book: &str = "Programming in Rust";
println!("\nReview for \'{}\': {:?}", book, reviews.get(book));

// Remove book review
let obsolete: &str = "Ancient Roman History";
println!("\n'{}\' removed.", obsolete);
reviews.remove(obsolete);

// Confirm book review removed
println!("\nReview for \'{}\': {:?}", obsolete, reviews.get(obsolete));
```
