## Appendix A: Keywords

The following list contains keywords that are reserved for current or future. 
Aur ye, identifiers ki trah use nahi kr sakte (exception here, raw identifiers h ham 
usko discuss karenge “[RawIdentifiers][raw-identifiers]<!-- ignore -->” section me). Identifiers are names of functions, variables, parameters, struct fields, modules, 
crates, constants,macros, static values, attributes, types, traits, or lifetimes.

[raw-identifiers]: #raw-identifiers

### Keywords Currently in Use

Ye sari list h currently, in use keyword aur functionality described as below:

- `as` - perform primitive casting, disambiguate the specific trait containing
  an item, or rename items in `use` statements
- `async` - return a `Future` instead of blocking the current thread
- `await` - suspend execution until the result of a `Future` is ready
- `break` - exit a loop immediately
- `const` - define constant items or constant raw pointers
- `continue` - continue to the next loop iteration
- `crate` - in a module path, refers to the crate root
- `dyn` - dynamic dispatch to a trait object
- `else` - fallback for `if` and `if let` control flow constructs
- `enum` - define an enumeration
- `extern` - link an external function or variable
- `false` - Boolean false literal
- `fn` - define a function or the function pointer type
- `for` - loop over items from an iterator, implement a trait, or specify a
  higher-ranked lifetime
- `if` - branch based on the result of a conditional expression
- `impl` - implement inherent or trait functionality
- `in` - part of `for` loop syntax
- `let` - bind a variable
- `loop` - loop unconditionally
- `match` - match a value to patterns
- `mod` - define a module
- `move` - make a closure take ownership of all its captures
- `mut` - denote mutability in references, raw pointers, or pattern bindings
- `pub` - denote public visibility in struct fields, `impl` blocks, or modules
- `ref` - bind by reference
- `return` - return from function
- `Self` - a type alias for the type we are defining or implementing
- `self` - method subject or current module
- `static` - global variable or lifetime lasting the entire program execution
- `struct` - define a structure
- `super` - parent module of the current module
- `trait` - define a trait
- `true` - Boolean true literal
- `type` - define a type alias or associated type
- `union` - define a [union][union]<!-- ignore -->; is only a keyword when used
  in a union declaration
- `unsafe` - denote unsafe code, functions, traits, or implementations
- `use` - bring symbols into scope
- `where` - denote clauses that constrain a type
- `while` - loop conditionally based on the result of an expression

[union]: ../reference/items/unions.html

### Keywords Reserved for Future Use

Ye sare keywords ke abhi functionality nahi h magar isko reserve krke rakhe h for future.

- `abstract`
- `become`
- `box`
- `do`
- `final`
- `macro`
- `override`
- `priv`
- `try`
- `typeof`
- `unsized`
- `virtual`
- `yield`

### Raw Identifiers

_Raw identifiers_ esse syntax h jo aapko reserved ko use karne ka mauka deta hai 
jo normally allowed nahi h. Raw identifier ke prefix mein `r#` keyword add kare.

For example, `match` ek keyword hai. Agar aap compile krne ka try kare, jo ki yaha 
`match` ko function name ki tarah use kr raha h:

<span class="filename">Filename: src/main.rs</span>

```rust,ignore,does_not_compile
fn match(needle: &str, haystack: &str) -> bool {
    haystack.contains(needle)
}
```

Apko ye error aaega:

```text
error: expected identifier, found keyword `match`
 --> src/main.rs:4:4
  |
4 | fn match(needle: &str, haystack: &str) -> bool {
  |    ^^^^^ expected identifier, found keyword
```

Ye error dikha raha h ki app `match` keyword ko as function identifier use 
nahi kr sakte. `match` as function name use krna h, to hame use krna hoga 
raw identifier syntax, like this:

<span class="filename">Filename: src/main.rs</span>

```rust
fn r#match(needle: &str, haystack: &str) -> bool {
    haystack.contains(needle)
}

fn main() {
    assert!(r#match("foo", "foobar"));
}
```

Yeh code bina kisi error ke compile ho jayega. Function ki definition me aur 
`main` ke function ko call karte waqt `r#` prefix ko note kare.

Raw identifiers hame pura freedom deta h kisi bhi word ko select krne me 
identifier ki trah, chahe wo reserved keyword hi ho. Iss tarah se ham
esse words ko bhi choose kr sakte h jo dusre programs me keywords nahi h.
Aur raw identifiers hame help kr sakte h purane rust version se naye 
rust versions me portability provide kr ke. For example, `try` keyword 2015 
version me nahi tha, magar 2018 me introduce kiya gaya. Agar ham 2015 edition 
library pe depend karte h aur `try` function h, to phir hame raw identifier 
syntax,`r#try`use krna hoga, 2018 edition me wo function ko call krne ke liye. 
See [AppendixE][appendix-e]<!-- ignore --> for more information on editions.

[appendix-e]: appendix-05-editions.html