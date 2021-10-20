# Code war Solutions

## Kata 1 (a multiplication table)

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

P. S. You can use `\n` in string to jump to the next line.\

Code

```js
const multiTable = (number) =>
  [...Array(10)]
    .map((_, idx) => `${++idx} * ${number} = ${idx * number}`)
    .join(`\n`);
```

## Kate 2 (&str split trim ..)

Examples

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

Code

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

Code

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

Example: (Input1, Input2 --> Output)

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

## Kata 5  (判断是否递增数  123,999,889 =>true; 102,956 =>false)

Test

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

Code

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

## Kata 6  (计算字符价值)

Given a string `"abc"` and assuming that each letter in the string has a value equal to its position in the alphabet, our string will have a value of `1 + 2 + 3 = 6`. This means that: `a = 1, b = 2, c = 3 ....z = 26`.

You will be given a list of strings and your task will be to return the values of the strings as explained above multiplied by the position of that string in the list. For our purpose, position begins with `1`.

`nameValue ["abc","abc abc"]` should return `[6,24]` because of `[ 6 * 1, 12 * 2 ]`. Note how spaces are ignored.

`"abc"` has a value of `6`, while `"abc abc"` has a value of `12`. Now, the value at position `1` is multiplied by `1` while the value at position `2` is multiplied by `2`.

Test

```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn basic_tests() {
        assert_eq!(word_value(&["abc", "abc", "abc", "abc"]), [6, 12, 18, 24]);
        assert_eq!(word_value(&["codewars", "abc", "xyz"]), [88, 12, 225]);
    }
}

```

Code

```rust
#[allow(dead_code)]
#[allow(unused_variables)]
fn word_value(words: &[&str]) -> Vec<i32> {
    // todo!();
    let mut all_sum = Vec::new();
    for i in 0..words.len() {
        let value = each_word(words[i]);
        all_sum.push(value as i32 * (i + 1) as i32);
    }
    fn each_word(words: &str) -> i64 {
        let value = words
            .split("")
            .filter(|s| !s.is_empty())
            .collect::<Vec<&str>>();
        let mut sum = 0;
        for i in 0..value.len() {
            if value[i] != " " {
                let acsii = value[i].chars().collect::<Vec<char>>()[0] as usize - 96;
                sum += acsii;
            }
        }
        return sum as i64;
    }
    return all_sum;
}
fn main() {
    println!("{:?}", word_value(&["abc", "abc abc", "abc", "abc"]));  //[6, 24, 18, 24]
}

```

## Kata 7 (Sum of Minimums!)

Given a 2D list of size `4 * 4`. Your task is to find the sum of minimum value in each row.

For Example:

So, the function should return `26` because sum of minimums is as `1 + 5 + 20 = 26`

Note: You will be always given non-empty array containing Positive values.

Test

```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_sum_of_minimums() {
        assert_eq!(sum_of_minimums([[7, 9, 8, 6], [6, 5, 4, 3], [5, 7, 4, 5], [7, 9, 4, 3]]), 16);
        assert_eq!(sum_of_minimums([[7, 9, 8, 6], [6, 5, 4, 3], [5, 7, 4, 5], [7, 9, 4, 4]]), 17);
        assert_eq!(sum_of_minimums([[7, 9, 8, 84], [6, 5, 4, 65], [5, 7, 4, 23], [7, 9, 4, 25]]), 19);
    }
}

```

Code

```rust
#[allow(dead_code)]
#[allow(unused_variables)]
fn sum_of_minimums(numbers: [[u8; 4]; 4]) -> u8 {
    // todo!()
    let mut sum = 0;
    for i in numbers.clone().iter_mut() {
        i.sort();
        sum += i[0];
        // println!("{:?}", i);
    }
    sum
}
fn main() {
    println!(
        "{:?}",
        sum_of_minimums([[7, 9, 8, 6], [6, 5, 4, 3], [5, 7, 4, 5], [7, 9, 4, 3]])
    );
}
```

## Kata 8 (Over The Road 在对立面第几个房子)

Given your house number `address` and length of street `n`, give the house number on the opposite side of the street.

```
1, 3 --> 6
3, 3 --> 4
2, 3 --> 5
3, 5 --> 8
```

Test

```rust
#[cfg(test)]
mod tests {
    use super::over_the_road;

    #[test]
    fn basic() {
        assert_eq!(over_the_road(1, 3), 6);
        assert_eq!(over_the_road(3, 3), 4);
        assert_eq!(over_the_road(2, 3), 5);
        assert_eq!(over_the_road(3, 5), 8);
        assert_eq!(over_the_road(7, 11), 16);
        assert_eq!(over_the_road(20, 1_000_000), 1_999_981);
        assert_eq!(over_the_road(23_633_656_673, 310_027_696_726), 596_421_736_780);       
    }
}

```

Code

```rust
#[allow(dead_code)]
#[allow(unused_variables)]
fn over_the_road(address: u64, n: u64) -> u64 {
    // todo!()
     let even = address % 2 == 0;
    if even {
        let row = n - (address / 2);
        (row * 2) + 1
    } else {
        let row = (address - 1) / 2;
        (n - row) * 2
    }
}
fn main() {
    assert_eq!(over_the_road(1, 3), 6);
    assert_eq!(over_the_road(3, 3), 4);
}

```

## Kata 9 (Who likes it?)

Implement the function which takes an array containing the names of people that like an item. It must return the display text as shown in the examples:

```rust
[]                                -->  "no one likes this"
["Peter"]                         -->  "Peter likes this"
["Jacob", "Alex"]                 -->  "Jacob and Alex like this"
["Max", "John", "Mark"]           -->  "Max, John and Mark like this"
["Alex", "Jacob", "Mark", "Max"]  -->  "Alex, Jacob and 2 others like this"
```

Test

```rust
#[cfg(test)]
mod tests {
    use super::likes;

    #[test]
    fn example_tests() {
        assert_eq!(likes(&[]), "no one likes this");
        assert_eq!(likes(&["Peter"]), "Peter likes this");
        assert_eq!(likes(&["Jacob", "Alex"]), "Jacob and Alex like this");
        assert_eq!(
            likes(&["Max", "John", "Mark"]),
            "Max, John and Mark like this"
        );
        assert_eq!(
            likes(&["Alex", "Jacob", "Mark", "Max"]),
            "Alex, Jacob and 2 others like this"
        );
    }
}
```

Code

```rust
fn likes(names: &[&str]) -> String {
    // todo!()
    if names.len() == 0 {
        return String::from("no one likes this");
    } else if names.len() == 1 {
        return String::from(format!("{} likes this", names[0]));
    } else if names.len() == 2 {
        return String::from(format!("{} and {} like this", names[0], names[1]));
    } else if names.len() == 3 {
        return String::from(format!(
            "{}, {} and {} like this",
            names[0], names[1], names[2]
        ));
    } else {
        return String::from(format!(
            "{}, {} and {} others like this",
            names[0],
            names[1],
            names.len() - 2
        ));
    }
}

//other solution for likes
fn likes(names: &[&str]) -> String {
    match names {
        [] => format!("no one likes this"),
        [a] => format!("{} likes this", a),
        [a, b] => format!("{} and {} like this", a, b),
        [a, b, c] => format!("{}, {} and {} like this", a, b, c),
        [a, b, rest @ ..] => format!("{}, {} and {} others like this", a, b, rest.len()),
    }
}
```

## kata 10 (Rainfall 查找城市，雨量均值和方差)

`data`and `data1` are two strings with rainfall records of a few cities for months from January to December. The records of towns are separated by `\n`. The name of each town is followed by `:`.

`data` and `towns` can be seen in "Your Test Cases:".

Task:

- function: `mean(town, strng)` should return the average of rainfall for the city `town` and the `strng` `data` or `data1` (In R and Julia this function is called `avg`).
- function: `variance(town, strng)` should return the variance of rainfall for the city `town` and the `strng` `data` or `data1`.

Examples:

```rust
mean("London", data), 51.19(9999999999996) 
variance("London", data), 57.42(833333333374)
```

Test

```rust
#[cfg(test)]
    mod tests {
    use super::*;
    use float_eq::float_eq;
    
    fn assert_float_equals(actual: f64, expected: f64) {
        let merr = 1.0e-2;
        let res = float_eq!(actual, expected, abs <= merr) || float_eq!(actual, expected, rmax <= merr);
        assert!(res, format!("Expected value must be near: {:e} but was:{:e}", expected, actual));
    }

    fn dotest(town: &str, strng: &str, exp_mean: f64, exp_variance: f64) -> () {
        let m = mean(town, strng);
        let v = variance(town, strng);
        assert_float_equals(m, exp_mean);
        assert_float_equals(v, exp_variance);
    }

    fn da_ta() -> String {
    
// don't move the string below

let dr0 = r#"Rome:Jan 81.2,Feb 63.2,Mar 70.3,Apr 55.7,May 53.0,Jun 36.4,Jul 17.5,Aug 27.5,Sep 60.9,Oct 117.7,Nov 111.0,Dec 97.9
London:Jan 48.0,Feb 38.9,Mar 39.9,Apr 42.2,May 47.3,Jun 52.1,Jul 59.5,Aug 57.2,Sep 55.4,Oct 62.0,Nov 59.0,Dec 52.9
Paris:Jan 182.3,Feb 120.6,Mar 158.1,Apr 204.9,May 323.1,Jun 300.5,Jul 236.8,Aug 192.9,Sep 66.3,Oct 63.3,Nov 83.2,Dec 154.7
NY:Jan 108.7,Feb 101.8,Mar 131.9,Apr 93.5,May 98.8,Jun 93.6,Jul 102.2,Aug 131.8,Sep 92.0,Oct 82.3,Nov 107.8,Dec 94.2
Vancouver:Jan 145.7,Feb 121.4,Mar 102.3,Apr 69.2,May 55.8,Jun 47.1,Jul 31.3,Aug 37.0,Sep 59.6,Oct 116.3,Nov 154.6,Dec 171.5
Sydney:Jan 103.4,Feb 111.0,Mar 131.3,Apr 129.7,May 123.0,Jun 129.2,Jul 102.8,Aug 80.3,Sep 69.3,Oct 82.6,Nov 81.4,Dec 78.2
Bangkok:Jan 10.6,Feb 28.2,Mar 30.7,Apr 71.8,May 189.4,Jun 151.7,Jul 158.2,Aug 187.0,Sep 319.9,Oct 230.8,Nov 57.3,Dec 9.4
Tokyo:Jan 49.9,Feb 71.5,Mar 106.4,Apr 129.2,May 144.0,Jun 176.0,Jul 135.6,Aug 148.5,Sep 216.4,Oct 194.1,Nov 95.6,Dec 54.4
Beijing:Jan 3.9,Feb 4.7,Mar 8.2,Apr 18.4,May 33.0,Jun 78.1,Jul 224.3,Aug 170.0,Sep 58.4,Oct 18.0,Nov 9.3,Dec 2.7
Lima:Jan 1.2,Feb 0.9,Mar 0.7,Apr 0.4,May 0.6,Jun 1.8,Jul 4.4,Aug 3.1,Sep 3.3,Oct 1.7,Nov 0.5,Dec 0.7
"#;
        return String::from(dr0);
    }

    #[test]
    fn basic_tests() {
        let da_ta = &da_ta();
        dotest("London", da_ta, 51.199999999999996, 57.42833333333374);
        dotest("Beijing", da_ta, 52.416666666666664, 4808.37138888889);
    }
}

```

Code

```rust
#[allow(dead_code)]
#[allow(unused_variables)]
fn da_ta() -> String {
    // don't move the string below
    let dr0 = r#"Rome:Jan 81.2,Feb 63.2,Mar 70.3,Apr 55.7,May 53.0,Jun 36.4,Jul 17.5,Aug 27.5,Sep 60.9,Oct 117.7,Nov 111.0,Dec 97.9
London:Jan 48.0,Feb 38.9,Mar 39.9,Apr 42.2,May 47.3,Jun 52.1,Jul 59.5,Aug 57.2,Sep 55.4,Oct 62.0,Nov 59.0,Dec 52.9
Paris:Jan 182.3,Feb 120.6,Mar 158.1,Apr 204.9,May 323.1,Jun 300.5,Jul 236.8,Aug 192.9,Sep 66.3,Oct 63.3,Nov 83.2,Dec 154.7
NY:Jan 108.7,Feb 101.8,Mar 131.9,Apr 93.5,May 98.8,Jun 93.6,Jul 102.2,Aug 131.8,Sep 92.0,Oct 82.3,Nov 107.8,Dec 94.2
Vancouver:Jan 145.7,Feb 121.4,Mar 102.3,Apr 69.2,May 55.8,Jun 47.1,Jul 31.3,Aug 37.0,Sep 59.6,Oct 116.3,Nov 154.6,Dec 171.5
Sydney:Jan 103.4,Feb 111.0,Mar 131.3,Apr 129.7,May 123.0,Jun 129.2,Jul 102.8,Aug 80.3,Sep 69.3,Oct 82.6,Nov 81.4,Dec 78.2
Bangkok:Jan 10.6,Feb 28.2,Mar 30.7,Apr 71.8,May 189.4,Jun 151.7,Jul 158.2,Aug 187.0,Sep 319.9,Oct 230.8,Nov 57.3,Dec 9.4
Tokyo:Jan 49.9,Feb 71.5,Mar 106.4,Apr 129.2,May 144.0,Jun 176.0,Jul 135.6,Aug 148.5,Sep 216.4,Oct 194.1,Nov 95.6,Dec 54.4
Beijing:Jan 3.9,Feb 4.7,Mar 8.2,Apr 18.4,May 33.0,Jun 78.1,Jul 224.3,Aug 170.0,Sep 58.4,Oct 18.0,Nov 9.3,Dec 2.7
Lima:Jan 1.2,Feb 0.9,Mar 0.7,Apr 0.4,May 0.6,Jun 1.8,Jul 4.4,Aug 3.1,Sep 3.3,Oct 1.7,Nov 0.5,Dec 0.7
"#;
    return String::from(dr0);
}
#[allow(unused_variables)]
fn mean(town: &str, strng: &str) -> f64 {
    // your code
    let sitys = strng.split("\n").collect::<Vec<_>>();
    // println!("{:?}", sitys);
    let mut town_set = Vec::new();
    for i in 0..sitys.len() {
        if sitys[i].split(":").collect::<Vec<_>>()[0] == town {
            town_set.push(sitys[i].split(":").collect::<Vec<_>>()[1]);
        }
    }
    let mut town_set_num: Vec<f64> = Vec::new();
    for i in 0..town_set.len() {
        for j in 0..town_set[i].split(",").collect::<Vec<_>>().len() {
            town_set_num.push(
                town_set[i].split(",").collect::<Vec<_>>()[j]
                    .split(" ")
                    .collect::<Vec<_>>()[1]
                    .parse()
                    .unwrap(),
            );
        }
    }

    // println!("{:?}", town_set);
    // println!("{:?}", town_set_num);
    let mut sum: f64 = 0.0;
    for i in town_set_num.clone() {
        sum += i;
    }
    let len = town_set_num.len();
    let avr = sum / len as f64;
    avr
}
#[allow(unused_variables)]
fn variance(town: &str, strng: &str) -> f64 {
    // your code
    let sitys = strng.split("\n").collect::<Vec<_>>();
    // println!("{:?}", sitys);
    let mut town_set = Vec::new();
    for i in 0..sitys.len() {
        if sitys[i].split(":").collect::<Vec<_>>()[0] == town {
            town_set.push(sitys[i].split(":").collect::<Vec<_>>()[1]);
        }
    }
    let mut town_set_num: Vec<f64> = Vec::new();
    for i in 0..town_set.len() {
        for j in 0..town_set[i].split(",").collect::<Vec<_>>().len() {
            town_set_num.push(
                town_set[i].split(",").collect::<Vec<_>>()[j]
                    .split(" ")
                    .collect::<Vec<_>>()[1]
                    .parse()
                    .unwrap(),
            );
        }
    }

    // println!("{:?}", town_set);
    // println!("{:?}", town_set_num);
    let mut sum: f64 = 0.0;
    for i in town_set_num.clone() {
        sum += i;
    }
    let len = town_set_num.clone().len();
    let avr = sum / len as f64;
    let mut s_sum = 0.0;
    for i in town_set_num.clone() {
        s_sum += (i - avr).powf(2.0);
    }
    let variance_result = s_sum / (len) as f64;
    variance_result
}
fn main() {
    let data = &da_ta().to_owned();
    println!("{}", mean("London", data));
    println!("{}", variance("London", data));
    println!("{}", mean("Beijing", data));
    println!("{}", variance("Beijing", data));
    // 51.199999999999996
    // 57.428333333333335
    // 52.416666666666664
    // 4808.37138888889
}

```

