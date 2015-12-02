---
layout: post
title: Error handling in Rust
---

A short cheatsheet for dealing with `Return` values in [Rust](http://rust-lang.org/).

When a `Result` is `Ok<T>`:

```rust
let result: Result<&str, &str> = Ok("Succeeded");

result.is_ok() == true;
result.is_err() == false;

result.ok() == Some("Succeeded");
result.err() == None;

let other_result: Result<&str, &str> = Ok("Other result");
result.and(other_result) == Ok("Other result");
result.or(other_result) == Ok("Succeeded");

fn example(string: &str) -> Result<&str, &str> { Ok("Example") }
result.and_then(example) == Ok("Example");
result.or_else(example) == Ok("Succeeded");
```

When a `Result` is `Err<E>`:

```rust
let result: Result<&str, &str> = Err("Failed");

result.is_ok() == false;
result.is_err() == true;

result.ok() == None;
result.err() == Some("Failed");

let other_result: Result<&str, &str> = Ok("Other result");
result.and(other_result) == Err("Failed");
result.or(other_result) == Ok("Other result");

fn example(string: &str) -> Result<&str, &str> { Ok("Example") }
result.and_then(example) == Err("Failed");
result.or_else(example) == Ok("Example");
```

When an `Option` is `Some<T>`:

```rust
let option: Option<&str> = Some("Example");

option.is_some() == true;
option.is_none() == false;

option.unwrap() == "Example";
option.unwrap_or("Other") == "Example";
option.expect("the world is ending") == "Example";
```

When an `Option` is `None`:

```rust
option.is_some() == false;
option.is_none() == true;

option.unwrap(); // panic!()
option.unwrap_or("Other") == "Other";
option.expect("the world is ending"); // panic!("the world is ending")
```
