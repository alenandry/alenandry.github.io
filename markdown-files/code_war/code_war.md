# Code war Solutions

## Kata 1

Your goal is to return multiplication table for `number` that is always an integer from 1 to 10.

For example, a multiplication table (string) for `number == 5` looks like below:

```
1 * 5 = 5
2 * 5 = 10
3 * 5 = 15
4 * 5 = 20
5 * 5 = 25
6 * 5 = 30
7 * 5 = 35
8 * 5 = 40
9 * 5 = 45
10 * 5 = 50
```

P. S. You can use `\n` in string to jump to the next line.

```js
const multiTable = (number) =>
  [...Array(10)]
    .map((_, idx) => `${++idx} * ${number} = ${idx * number}`)
    .join(`\n`);
```

## Kate 2

## Examples

```rust
songDecoder("WUBWEWUBAREWUBWUBTHEWUBCHAMPIONSWUBMYWUBFRIENDWUB")
  // =>  WE ARE THE CHAMPIONS MY FRIEND
```

```rust
#[cfg(test)]
mod tests {
    use super::song_decoder;
    
    #[test]
    fn returns_expected() {
        assert_eq!(song_decoder("WUBAWUBWUBC"), "A C");
        assert_eq!(song_decoder("AWUBWUBWUBBWUBWUBWUBC"), "A B C");
        assert_eq!(song_decoder("WUBAWUBBWUBCWUB"), "A B C");
        assert_eq!(song_decoder("AWUBBWUBC"), "A B C");
    }
}
```

Solution

```rust
#[allow(dead_code)]
#[allow(unused_variables)]
fn song_decoder(song: &str) -> String {
    // todo!();
    let arr = song.split("WUB").collect::<Vec<_>>();
    let mut new_arr = String::new();
    for x in arr.iter() {
        if x.to_owned() != "" {
            new_arr.push_str(x);
            new_arr.push_str(" ");
        }
    }
    new_arr.trim().to_string()
}
fn main() {
    println!(
        "{}",
        song_decoder("WUBWEWUBAREWUBWUBTHEWUBCHAMPIONSWUBMYWUBFRIENDWUB")
          // =>  WE ARE THE CHAMPIONS MY FRIEND
    );
}


//solution 2
use itertools::Itertools;

fn song_decoder(song: &str) -> String {
    song.split("WUB").filter(|s| !s.is_empty()).join(" ")
}
```

## Kata 3 (find_next_square)

**Examples:(Input --> Output)**

```
121 --> 144
625 --> 676
114 --> -1 since 114 is not a perfect square
```

```rust
#[cfg(test)]
mod tests {
    use super::find_next_square;
    
    #[test]
    fn sample_tests() {
        assert_eq!(find_next_square(121), Some(144));
        assert_eq!(find_next_square(625), Some(676));
        assert_eq!(find_next_square(319_225), Some(320_356));
        assert_eq!(find_next_square(15_241_383_936), Some(15_241_630_849));
        assert_eq!(find_next_square(155), None);
        assert_eq!(find_next_square(342_786_627), None);
    }
}
```

Solution

```rust
fn find_next_square(sq: u64) -> Option<u64> {
    // todo!();
    let root = (sq as f64).sqrt();
    // println!("{}", root);
    if root != root.floor() {
        return None;
    }
    Some((root as u64 + 1).pow(2))
}
```

## Kata 4 (repeater())

Write a function named `repeater()` that takes two arguments (a string and a number), and returns a new string where the input string is repeated that many times.

## Example: (Input1, Input2 --> Output)

```rust
//"a", 5 --> "aaaaa"

#[test]
fn basic_test() {
  assert_eq!(repeater("a", 5), "aaaaa");
  assert_eq!(repeater("Na", 16), "NaNaNaNaNaNaNaNaNaNaNaNaNaNaNaNa");
  assert_eq!(repeater("Wub ", 6), "Wub Wub Wub Wub Wub Wub ");
}
```

```rust
fn repeater(string: &str, n: u32) -> String {
    string.repeat(n as usize)
}
```

## Kata 5  判断是否递增数

```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn basic() {
        assert_eq!(tidy_number(12), true);
        assert_eq!(tidy_number(102), false);
        assert_eq!(tidy_number(222), true);
        assert_eq!(tidy_number(2789), true);
        assert_eq!(tidy_number(2335), true);
    }
}

```

```rust
fn tidy_number(n: u64) -> bool {
  
    if n.to_string()
        .chars()
        .collect::<Vec<char>>()
        .windows(2)
        .all(|x| x[0] <= x[1])
    {
        true
    } else {
        false
    }
}
//windows 的用法
let slice = ['r', 'u', 's', 't'];
let mut iter = slice.windows(2);
assert_eq!(iter.next().unwrap(), &['r', 'u']);
assert_eq!(iter.next().unwrap(), &['u', 's']);
assert_eq!(iter.next().unwrap(), &['s', 't']);
assert!(iter.next().is_none());
```

