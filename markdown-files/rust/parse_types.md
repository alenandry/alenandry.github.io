# rust 常用类型转换

#### 原生类型

```
| x 类型\至类型 | i32                | u32                | f64                | String        |
| ------------- | ------------------ | ------------------ | ------------------ | ------------- |
| i32           | n/a                | x as u32           | x as f64           | x.to_string() |
| u32           | x as u32           | n/a                | x as f64           | x.to_string() |
| f64           | x as i32           | x as u32           | n/a                | x.to_string() |
| String\*      | x.parse().unwrap() | x.parse().unwrap() | x.parse().unwrap() | n/a           |
```

- \*可以看到 i32, u32, f64 到 String 类型是同一个函数，这样的话，如何来确定要转换至的具体类型？就是类型推导！当然，如果 rust 无法通过上下文推导出类型，就需要给出提示，例如 x.parse::<i32>().unwrap()。但是通常情况下，都不需要提示即可自动推导出类型。

#### &str/String/collections::string::String

```
| x 类型\至类型 | String        | &str |
| ------------- | ------------- | ---- |
| String        | n/a           | &\*x |
| &str          | x.to_string() | n/a  |
```

#### Vec<T>/&[T]/Box<[T]>

```
| x 类型\至类型 | Vec<T>     | &[T]   | Box<[T]>             |
| ------------- | ---------- | ------ | -------------------- |
| Vec<T>        | n/a        | &x[..] | x.into_boxed_slice() |
| &[T]          | x.to_vec() | n/a    | Box::new(\*x)        |
| Box<[T]>      | x.to_vec() | &\*x   | n/a                  |
```
