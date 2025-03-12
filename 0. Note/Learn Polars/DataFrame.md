---
tags:
  - note
Project:
  - "[[Lean Polars]]"
Status: In progress
---
## Instantiation
```rust
let df = df!(
	"name" => ["Name1", "Name2"],
	"weight" => [123, 124],
	"height" => [342, 525]
).unwrap();
```

## Inspecting a DataFrame
### Head
You can see the top n rows of a `DataFrame` by making use of the `df.head` method. This takes a single argument which is an `Option` wrapped integer. If None is supplied `df.head` defaults to the displaying the first 5 rows of the `DataFrame`.

### Glimpse
*Python Only*
This is effectively identical as head but allows you to decide how the data is represented. This is especially useful for examining wide `DataFrames`.

### Tail
This is just the antithesis of head and shows you the last n rows. 

### Sample
This is probably more useful than head and tail in most scenarios. This grabs a random sample from your `DataFrame`.

### Describe
*Python only*
This can be used to find out summary statistics about your `DataFrame`.

### Schema
This can be used to find out what data types are associated with each `Series` with the `DataFrame`.
When [[DataFrame#Instantiation|instantiating]] a `DataFrame` in python you can supply a schema dictionary that will map the column name to a pre-specified data type, you can use None if you wish to defer to Polars default type inference. 


## Casting
Simply put you can cast the columns of a `DataFrame` to different data types.
This includes down-casting numeric types. This is done with the `.cast()` function.
```rust
let cast_expr = col("integers").cast(DataType::float32).alias("integers_as_float");
```
- Float -> int, truncates
- string -> numeric, if strict is not set to false errors out when trying to cast a non-numeric string. Otherwise supplies null when set to false.
- Numeric -> boolean, true if 1 else false
- Boolean -> numeric, 1 if true else 0
- date -> string, as you would expect see chrono for details