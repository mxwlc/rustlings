# Rustlings Exercises Notes

## Intro

### `intro1.rs`

NB : Removing `// I AM NOT DONE` to let rustlings to forget the current rust file and run the next.

### `intro2.rs`

In rust you can use curly braces to to allow for arguements to be added after the format string.

```rust
fn main() {
    println!("Hello {}!", "World");
}
```

## Variables

### `variables1.rs`

To define variables in rust use the `let` keyword, for exampel

```rust
fn main() {
    let x = 5;
    println!("x has the value {}", x);
}
```

### `variables2.rs`

To define variables of a certain type use a colon followed by the variables type e.g.

```rust
fn main() {
    let x: i32 = 10;
}
```

or for a string

```rust
fn main() {
    let x: str = "goblin";
}
```

### `variables3.rs`

As in [intro2.rs](#intro2rs) you can pass a variable into `println!` as an arguement for example.

```rust
fn main() {
    let x: i32 = 10;
    println!("Number {}", x);
}
```

### `variables4.rs`

adding the `mut` keyword allows for the variable to be mutable (can be changed)

```rust
fn main() {
    let mut x = 3;
    println!("Number {}", x);
    x = 5; // don't change this line
    println!("Number {}", x);
}
```

### `variables5.rs`

Rust allows for the variable name to be used more than once (
see [shadowing](https://doc.rust-lang.org/book/ch03-01-variables-and-mutability.html#shadowing)) This is done by
redeclaring the variable and using the `let` keyword again. e.g.

```rust
fn main() {
    let number = "T-H-R-E-E"; // don't change this line
    println!("Spell a Number : {}", number);
    let number = 3; // don't rename this variable
    println!("Number plus two is : {}", number + 2);
}
```

### `variables6.rs`
`const` variables have to be declared with the data type of the underlying variable. e.g.
```rust
const NUMBER : i32 = 3;
```

## Functions

### `functions1.rs`
Functions (disregarding the return type) are defined as such.
```rust
fn call_me(){}
fn main() {
    call_me();
}
```

### `functions2.rs`
Arguements datatypes are declared as such
```rust
fn foo(bar : i32){}
```
Where `foo` is the function and `bar` is an arguement.
e.g.
```rust
fn main(){ call_me(3); }
fn call_me(num:i32) {
    for i in 0..num {
        println!("Ring! Call number {}", i + 1);
    }
}
```
### `functions3.rs`

When calling a function you need to provide an arguement of the matching type.
e.g.
```rust
fn main() { call_me(3); }

fn call_me(num: u32) {
    for i in 0..num {
        println!("Ring! Call number {}", i + 1);
    }
}
```

### `functions4.rs`
When declaring a function a return type (like c) needs to be declared as well
```rust
fn foo(bar : i32) -> i32 {
    return baz;
}
```

### `functions5.rs`
As in pretty much all other languages with functions (provided they arent void) a return statement is needed.
```rust
fn square(num: i32) -> i32 {
    return num * num;
}
```
## If statements
### `if1.rs`
If statements declared like normal and uses no brackets (cf. c/c++)
```rust
pub fn bigger(a: i32, b: i32) -> i32 {
    if a > b {
        return a;
    }
    return b;
}
```

### `if2.rs`
An `else if` can be used as again. \
NB : The whole block needs to return the same datatype.
```rust
pub fn foo_if_fizz(fizzish: &str) -> &str {
    if fizzish == "fizz" {
        "foo"
    }
    else if fizzish=="fuzz"  {
        return "bar";
    }
    else {
        return "baz";
    }
}
```

### `if3.rs`
ALL statements within an if block must all give the same return type.
```rust
pub fn animal_habitat(animal: &str) -> &'static str {
    let identifier = if animal == "crab" {
        1
    } else if animal == "gopher" {
        2
    } else if animal == "snake" {
        3
    } else {
        0
    };
    // All return types the same
    let habitat = if identifier == 1 {
        "Beach"
    } else if identifier == 2 {
        "Burrow"
    } else if identifier == 3 {
        "Desert"
    } else {
        "Unknown"
    };

    habitat
}
```
NB : the variable being by itself at the end of the function as is following
```rust
 fn foo() -> i32{
    bar
}
```
is the equivalent of
```rust
fn foo()-> i32{
    return bar;
}
```
## `quiz1.rs`
For this quiz I used an if block within a declarator for a variable.
```rust
fn calculate_price_of_apples(num: i32) -> i32 {
    let price_per_apple = if num > 40 {
        1
    } else {
        2
    };
    return price_per_apple*num;
}
```
## Primative Types
>Booleans are either True or False (1/0) 

### `primative_types1.rs` - Booleans
Booleans are declared as follows.
```rust
fn main() {
    // Booleans (`bool`)

    let is_morning = true;
    if is_morning {
        println!("Good morning!");
    }

    let is_evening = false;// Finish the rest of this line like the example! Or make it be false!
    if is_evening {
        println!("Good evening!");
    }
}
```
### `primative_types2.rs` - Characters
> `Char` datatype is 8 bits

Characters also have methods such as `.is_alphabetic()` and `.is_numeric()`

```rust
fn main() {
    // Characters (`char`)
    let my_first_initial = 'C';
    if my_first_initial.is_alphabetic() {
        println!("Alphabetical!"); 
    } else if my_first_initial.is_numeric() {
        println!("Numerical!");
    } else {
        println!("Neither alphabetic nor numeric!");
    }
    let your_character = '0';
    if your_character.is_alphabetic() {
        println!("Alphabetical!");
    } else if your_character.is_numeric() {
        println!("Numerical!");
    } else {
        println!("Neither alphabetic nor numeric!");
```
### `primatice_types3.rs` - Arrays
> Arrays are a contiguous reserved block in memory
 
Arrays are defined in the form
```
let a : [<type>; <numberofelements>] = [<expression>;<numberofelements>];
```
For example:
```rust
fn main() {
    let a : [i32; 100] = [0;100];
}
```
### `primative_types4.rs` - Array Slicing
To slice an array we need to borrow the array first, to make a "copy", and then slicing it as follows
```rust
fn slice_out_of_array() {
    let a = [1, 2, 3, 4, 5];
    let nice_slice = &a[1..4];
}
```
It works as follows, to get array of size n entries with indices between i and j non inclusive
```rust
fn slice(){
    let a : [i32; n] = [0; n];
    let slice = &a[i..j];
}
```
### `primative_types5.rs` - Tuples
Tuples can be declared as a such. For numbers x,y,z.
```rust
fn main(){
    // Constructing
    let tup = (x,y,z);
    // Deconstruction
    let (x,y,z) = tup;
}
```

### `primative_types6.rs` - Tuple indexing
Tuple entries are indexed like OOP methods.
```rust
fn indexing_tuple() {
    let numbers = (1, 2, 3);
    let second = numbers.1;
}
```
> NB : Tuples like arrays are indexed from zero.

## Vectors
> Arrays with dynamic memory allocation
### `vecs1.rs` - Vector Declaration
Vectors can be declared similarly to arrays nut with the `vec![]` macto
```rust
fn array_and_vec() -> ([i32; 4], Vec<i32>) {
let a = [10, 20, 30, 40]; // a plain array
let v= vec![10,20,30,40];// TODO: declare your vector here with the macro for vectors

    (a, v)
}
```

### `vecs2.rs` - changing vector values
One way is to loop through the array referencing each element, dereferencing it as shown below.
```rust
fn vec_loop(mut v: Vec<i32>) -> Vec<i32> {
    for element in v.iter_mut() {
        *element = *element * 2;
    }
    v
}
```
Another way is to iterate through the vector, mapping each element with a function declared within `.iter().map(<input> { <modified_input>}).collect()`
```rust
fn vec_map(v: &Vec<i32>) -> Vec<i32> {
    v.iter().map(|element| {
        element *2
    }).collect()
}
```
## Move Semantics
### `move_semantics1.rs` - copying vectors
In order to alter the a vector that is input into a function, you need to create a new variable while using the `mut` keyword. 
```rust
fn fill_vec(vec: Vec<i32>) -> Vec<i32> {
    let mut vec = vec;
    vec.push(88);
    vec
}
```
### `move_semantics2.rs` - Copying vectors in functions.
In order to pass a vector into a function a copy needs to be passed in as opposed to the vector itself.
```rust
fn main() {
    let vec0 = vec![22, 44, 66];
    let mut vec1 = fill_vec(vec0.clone());
}
```
### `move_semantics3.rs`- Borrowing vec
In order to pass vectors into functions to be changed first they need to be declared as `mut <variable> : <datatype>`.
```rust
fn fill_vec(mut vec: Vec<i32>) -> Vec<i32> {
    vec.push(88);
    vec
}
```
### `move_semantics4.rs` - Scope
As this function has no arguments the vector vec can only be declared within the function (as opposed ot outside in the main funciton)
```rust
fn fill_vec() -> Vec<i32> {
    let mut vec = vec![22,44,66];
    vec.push(88);
    vec
}
```
### `move_semantics5.rs` - Mutable references
When you borrow a variable `&<variable>` alter it before making a second borrow.
```rust
fn main() {
    let mut x = 100;
    let y = &mut x;
    *y += 100;
    let z = &mut x;
    *z += 1000;
    assert_eq!(x, 1200);
}
```
### `move_semantics6.rs` - Borrowing
```rust
fn main() {
    let data = "Rust is great!".to_string();
    get_char(data.clone());
    string_uppercase(data);
}
fn get_char(data: String) -> char {
    data.chars().last().unwrap()
}
fn string_uppercase(mut data: String) {
    data = data.to_uppercase();
    println!("{}", data);
}
```
Here `get_char` doesnt alter the value `data` at all so a clone of data can be passed through, this allows for a fuction like `string_uppercase` to take ownership of and alter `data`.

## Structs
### `structs1.rs` - c type structs
####  1 : a list of field:type pairs
```rust
struct ColorClassicStruct {
    red: i32,
    green: i32,
    blue: i32,
}
```
These are declared as such
```rust
let green = ColorClassicStruct {
    red: 0,
    green: 255,
    blue: 0, 
};
```
####  2 : a tuple
```rust
struct ColorTupleStruct(i32, i32, i32);
```
Defined as a tuple of datatypes. Declared like thi.
```rust
let green = ColorTupleStruct(0,255,0);
```
## `structs2.rs` - Update Syntax
```rust
fn your_order() { 
    let order_template = create_order_template();
    let your_order = Order {
        name: String::from("Hacker in Rust"),
        count: 1,
        ..order_template
    };
}
```
In order to define a new struct with the sam values as another struct with some values chagned, we use `..<struct>`, as shown below.
### `structs3.rs` - `impl` package.
The `impl` package allows for logic to be added for a struct.
```rust
struct Package {
    sender_country: String,
    recipient_country: String,
    weight_in_grams: u32,
}
impl Package {
    fn new(sender_country: String, recipient_country: String, weight_in_grams: u32) -> Package {
        if weight_in_grams < 10 {
            panic!("Can not ship a package with weight below 10 grams.")
        } else {
            Package {
                sender_country,
                recipient_country,
                weight_in_grams,
            }
        }
    }
    fn is_international(&self) -> bool {
        if  *self.recipient_country != *self.sender_country {
        return true
        }
    return false
    }
    fn get_fees(&self, cents_per_gram: u32) -> u32 {
        return self.weight_in_grams * cents_per_gram
    }
}
```
In order to call each of the funtions in `impl` just call <struct>::<method>, (see namespace in c++).
## Enums
### `enums1.rs` - Declaring enums and using values
Enums are declared like this
```rust
enum Message {
    Quit,
    Echo,
    Move,
    ChangeColor
}
```
With values being accessed like `<enum>::<values>`
### `enums2.rs` - Declaring fields datatype
```rust
enum Message {
    Move{x:i32,y:i32},
    Echo(String),
    ChangeColor(i32,i32,i32),
    Quit
}
```
Declared as <field>:<datatype>
### `enums3.rs` - Match Statements
Like a switch case in c/c++. Matches `<input>=><func>`
```rust
fn process(&mut self, message: Message) {
    match message {
        Message::ChangeColor(r,g,b) => self.change_color((r,g,b)),
        Message::Echo(s)=>self.echo(s),
        Message::Move(p)=>self.move_position(p),
        Message::Quit => self.quit(), 
    }
}
```
## Strings
### `string1.rs` - `"<str>"` vs String
"<str>" is an array of character (string slice), so for something to be returned as a `String` the `.to_string()` method needs to be called.  
```rust
fn current_favorite_color() -> String {
    "blue".to_string()
}
```

### `string2.rs` - `&str` vs `String`
```rust

fn main() {
    let word = String::from("green"); // Try not changing this line :)
    if is_a_color_word(&word) {} else {}
}
fn is_a_color_word(attempt: &str) -> bool {
    attempt == "green" || attempt == "blue" || attempt == "red"
}
```
In order to pass word into the funcion `is_a_color_word` we first need to borrow it so the datatype is a `&str` and not a `String`.

### `string3.rs` - Str Methods
```rust
fn trim_me(input: &str) -> String {
    (input.trim()).to_string()
}
fn compose_me(input: &str) -> String {
    input.to_owned() + " world!"
}
fn replace_me(input: &str) -> String {
    input.replace("cars", "balloons")
}
```
| Method                  | Description                                 |
|-------------------------|---------------------------------------------|
| `.trim()`               | Removes Spaces                              |
| `<&str>+<&str>`         | String Concatination                        |
| `.replace(<from>,<to>)` | Renames all occurances of `<from>` to `<to>` |
## `string4.rs` - `&str` vs `String`
```rust
fn main() {
    string_slice("blue"); /* &str */
    string("red".to_string()); /* String */
    string(String::from("hi")); /* String */
    string("rust is fun!".to_owned()); /* String */
    string("nice weather".into()); /* String */
    string(format!("Interpolation {}", "Station")); /* String */
    string_slice(&String::from("abc")[0..1]); /* &str */
    string_slice("  hello there ".trim()); /* &str */
    string("Happy Monday!".to_string().replace("Mon", "Tues")); /* String */
    string("mY sHiFt KeY iS sTiCkY".to_lowercase()); /* String */ 
}
```
## Modules
### `modules1.rs` - Access Modifiers
Private functions are declared without the `pub` keyword, whereas public function have the `pub` keyword.
```rust
    fn get_secret_recipe() -> String {
        String::from("Ginger")
    }
    pub fn make_sausage() {
        get_secret_recipe();
        println!("sausage!");
    }
```
### `modules2.rs` - Renaming variable
`use <...> as <...>` aliases a varible. the `pub` keyword allows for the attribute to be accessed outside of the modules.
```rust
mod delicious_snacks {
    pub use self::fruits::PEAR as fruit;
    pub use self::veggies::CUCUMBER as veggie;
    mod fruits {
        pub const PEAR: &'static str = "Pear";
        pub const APPLE: &'static str = "Apple";
    }
    mod veggies {
        pub const CUCUMBER: &'static str = "Cucumber";
        pub const CARROT: &'static str = "Carrot";
    }
}
```
### `modules3.rs` - Importing external modules.
The followng line of code imports all functions from the module `std::time` .
```rust
use std::time::*;
```
The following code only imports the function `SystemTime`
```rust
use std::time::SystemTime;
```
## Hash Maps
### `hashmaps1.rs` - Declaring Hash Maps
This works for explicitly typed maps.
```rust
let mut basket : HashMap<String, u32> = Default::default();
```
Whereas here the types are inferred.
```rust
let mut <hash_map> = HashMap:new();
```
### `hashmaps2.rs` - Updating based on no key
The `.entry(<key>)` is the view into a single entry on a map, could be vacant or full. If the entry is vacant then the `.or_insert(<value>)` inserts `<value>` into the hashmap.
```rust
fn fruit_basket(basket: &mut HashMap<Fruit, u32>) {
    let fruit_kinds = vec![
        Fruit::Apple,
        Fruit::Banana,
        Fruit::Mango,
        Fruit::Lychee,
        Fruit::Pineapple,
    ];
    for fruit in fruit_kinds {
        basket.entry(fruit).or_insert(1);
    }
}
```
Here the function `fruit_basket(basket, HashMap<fruit, u32>)` checks if a fruit is present in the hashmap and then adds the fruits that are in the `fruit_kinds` vector but not in the `basket` hashmap.

### `hashmaps3.rs` - updateing based on old keys
In the following code the methods `.entry(<key>)`, `.or_insert_with_key(<key> <value>)` and `.modify(<expr>)`

| Method                               | Description                                                               |
|--------------------------------------|---------------------------------------------------------------------------|
| `and_modify(<expr>)`                 | Modifies the value corresponding to the entry returned by `.entry(<key>)` |
| `.or_insert_with_key(<key> <value>)` | Inserts a key value entry with key=`<key>` and value=`<values>`.          |
```rust
fn build_scores_table(results: String) -> HashMap<String, Team> {
    let mut scores: HashMap<String, Team> = HashMap::new();
    for r in results.lines() {
        let v: Vec<&str> = r.split(',').collect();
        let team_1_name = v[0].to_string();
        let team_1_score: u8 = v[2].parse().unwrap();.
        let team_1 = scores
            .entry(team_1_name)
            .and_modify(|e| {
                e.goals_scored += team_1_score;
                e.goals_conceded += team_2_score;
            })
            .or_insert_with_key(|name| Team {
                goals_scored: team_1_score,
                goals_conceded: team_2_score,
            });
    };
    scores
}
```
## `quiz2.rs` - Stirng Transformations
```rust
pub fn transformer(input: Vec<(String, Command)>) -> Vec<String> {
    let mut output: Vec<String> = vec![];
    for (string, command) in input.iter() {
        let mut t_string: String = String::new();
        match command {
            Command::Append(usize) => t_string = string.to_owned() + &"bar".repeat(*usize),
            Command::Trim => t_string = string.trim().to_owned(),
            Command::Uppercase => t_string = string.to_uppercase(),
        }
        output.push(t_string);
    }
    output
}
```
This function takes a vector of `(string,command)` tuples and then performs the operation on `string` corresponding to `command` using a `match` statement, the processed string is then pushed to the `output` vector which contains the processed strings which is the data the function returns.

## Options
### `options1` - Some vs None
Options are a datatype that either has a value of`Some(<T>)` or `None`. The listing below returns the number of ice cream depending on the time of day.
```rust
fn maybe_icecream(time_of_day: u16) -> Option<u16> {
    if time_of_day < 22 { return Some(5) }
    if time_of_day >= 22 && time_of_day < 25  {return Some(0)}
    return None;
}
```
### `options2.rs` - `if let` & `while let`
`if let` statement is use sometimes instead of a match case. `if let` allows us to check if variables match enums then execute the code in the curled brackets.
```rust
fn simple_option() {
    let target = "rustlings";
    let optional_target = Some(target);
    if let Some(word) = optional_target {
        assert_eq!(word, target);
    }
}
```
`while let` achieves the same concept of the `if let` w/r to the comparison.
```rust
while let Some(integer) = optional_integers.pop().flatten() {
    assert_eq ! (integer, cursor);
    cursor -= 1;
}
```
### `options3.rs` - `ref` keyword
The ref ekyword is used to borrow now move the variable making it available afterwards.
```rust
fn main() {
    let y: Option<Point> = Some(Point { x: 100, y: 200 });
    match y {
        Some(ref p) => println!("Co-ordinates are {},{} ", p.x, p.y),
        _ => panic!("no match!"),
    }
    y;
}
```
## Errors
### `errors1.rs` - Result data type
The Result Datatype is of the form `Result<<Ok-datatype>,<Err-datatype>>` as shown below.
Errors are thrown by returning `Err(<expr>)` otherwise returning `Ok(<expr>)`
```rust
pub fn generate_nametag_text(name: String) -> Result<String, String> {
    if name.is_empty() {
        Err("`name` was empty; it must be nonempty.".to_owned())
    } else {
        Ok(format!("Hi! My name is {}", name))
    }
}
```
### `errors2.rs` - the `?` operator
As can be seen by the line `let qty = item_quantity.parse::<i32>()?;` the `?` opeator can be used to stop the execution of a funtion and return an error from the original function call.
```rust
pub fn total_cost(item_quantity: &str) -> Result<i32, ParseIntError> {
    let processing_fee = 1;
    let cost_per_item = 5;
    let qty = item_quantity.parse::<i32>()?;
    Ok(qty * cost_per_item + processing_fee)
}
```
### `errors3.rs` - Returning an Error from Main
By convention if we want the main funciton to throw an error we have to specify the return type as `Result<(),ErrorType>`. The datatype `()` is an empty datatype used conventionally because the main function doesnt necessarily need to return anything.  
```rust
fn main() -> Result<(), ParseIntError> {
    let mut tokens = 100;
    let pretend_user_input = "8";
    let cost = total_cost(pretend_user_input)?;
    if cost > tokens {
        println!("You can't afford that many!");
    } else {
        tokens -= cost;
        println!("You now have {} tokens.", tokens);
    }
    Ok(())
}
```
### `errors4.rs` - Enum as error
An enum can be used as one of the data types in the result datatype as shown below.
```rust
fn new(value: i64) -> Result<PositiveNonzeroInteger, CreationError> {
    if value < 0 { return Err(CreationError::Negative); }
    if value == 0 { return Err(CreationError::Zero); }
    return Ok(PositiveNonzeroInteger(value as u64));
}
```
Here `CreationError::Negative` and `CreationError::Zero` are used.
### `errors5.rs` - `Box<dyn Error>`
Here `Box<dyn Error>` is used to allow for any error to be thrown, the downside of this is that the error type is only known at runtime.
```rust
fn main() -> Result<(), Box<dyn Error>> {
    let pretend_user_input = "42";
    let x: i64 = pretend_user_input.parse()?;
    println!("output={:?}", PositiveNonzeroInteger::new(x)?);
    Ok(())
}
```
### `errors6.rs` - Library error handling with enums
Functionality is implemented to handle errors to stop the propagation.
```rust
impl ParsePosNonzeroError {
    fn from_creation(err: CreationError) -> ParsePosNonzeroError {
        ParsePosNonzeroError::Creation(err)
    }
    fn from_parseint(err: ParseIntError) -> ParsePosNonzeroError{
        ParsePosNonzeroError::ParseInt(err)
    }
}
```
`.map_err(<function>)` is used to allow for a valid result to be passed through while handling the error that could be thrown.
```rust
fn parse_pos_nonzero(s: &str) -> Result<PositiveNonzeroInteger, ParsePosNonzeroError> {
    let x: i64 = s.parse().map_err(ParsePosNonzeroError::from_parseint)?;
    PositiveNonzeroInteger::new(x).map_err(ParsePosNonzeroError::from_creation)
}
```
## Generics
### `generics1.rs`
```rust
fn main() {
    let mut shopping_list: Vec<&str> = Vec::new();
    shopping_list.push("milk");
}
```
A basic example of a generic is the `vector`. Where the generic vector DataType can be instantiated with another datatype in angled brackets `vector<T>` where `T` is a datatype.

### `generics2.rs`
```rust
struct Wrapper<T> {
    value: T,
}
impl<T> Wrapper<T> {
    pub fn new(value: T) -> Self {
        Wrapper { value }
    }
}
mod tests {
    use super::*;
    fn store_u32_in_wrapper() {
        assert_eq!(Wrapper::new(42).value, 42);
    }
    fn store_str_in_wrapper() {
        assert_eq!(Wrapper::new("Foo").value, "Foo");
    }
}
```
Here `<T>` is used to define the struct (see `struct wrapper<T>`) as well as the methods in the `impl` where the angle bracket needs to also be put at the end of `impl<T>`. Here the type (`T`) is inferred when using the function `Wrapper::new()`.
## Traits
### `traits1.rs`
```rust
trait AppendBar {
    fn append_bar(self) -> Self;
}
impl AppendBar for String {
    fn append_bar(self) -> Self {
        return  self + "Bar";
    }
}
```
Here the trait `AppendBar` can be implemented for different data DataTypes in this case it implements the `append_bar` method for the `String` datatype.