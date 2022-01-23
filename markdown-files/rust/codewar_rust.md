# Use Rust implement codewar Kata solutions

## Kata 1 (vec 删除重复的元素,返回 Unique Vec)

```rust
use std::collections::BTreeSet;
fn unique_in_order(vec: Vec<i32>) -> Vec<i32> {
            let mut bset = BTreeSet::new();
            for i in vec {
                bset.insert(i);
            }
            let mut re_vec = Vec::new();
            for item in &bset {
                re_vec.push(*item);
            }
            re_vec
}

fn unique_in_order<T>(sequence: T) -> Vec<T::Item>
    where
        T: std::iter::IntoIterator,
        T::Item: std::cmp::PartialEq + std::fmt::Debug,
    {
        let mut v: Vec<_> = sequence.into_iter().collect();
        v.dedup();
        v
    }
```

## Kata 2 (寻找 k 大元素，删除重复)

```rust
/**
 * Kata1
 * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
 * @param a int整型一维数组
 * @param n int整型
 * @param K int整型     * @return int整型
 */
struct Kata1 {}
impl Kata1 {
    fn new() -> Self {
        Kata1 {}
    }
    #[allow(non_snake_case)]
    #[allow(dead_code)]
    #[allow(unused_variables)]
    pub fn findKth(&self, a: Vec<i32>, n: i32, K: i32) -> i32 {
        // write code here
        use std::collections::BTreeSet;
        fn unique_in_order(vec: Vec<i32>) -> Vec<i32> {
            let mut bset = BTreeSet::new();
            for i in vec {
                bset.insert(i);
            }
            let mut re_vec = Vec::new();
            for item in &bset {
                re_vec.push(*item);
            }
            re_vec
        }
        let mut a_ = a.clone();
        a_ = unique_in_order(a_.clone());
        a_.sort();
        // dbg!(&a_);
        // println!("{:?}", unique_in_order(a_.clone()));
        return a_[a_.len() - K as usize];
    }
}
fn main{
    println!("{}",Kata1::findKth(&Kata1::new(),vec![1,5,14,65,2,5],6,3)); //return 5
}
```

## Kata 3 (三个数的最大乘积)

```rust
struct Solution{}
impl Solution {
    fn new() -> Self {
        Solution{}
    }
    /**
    * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
    * 最大乘积
        * @param A int整型一维数组
        * @return long长整型
    */
    pub fn solve(&self, A: Vec<i32>) -> i64 {
   let mut vec = A;
    vec.sort();
    fn contain_minus(vec: Vec<i32>) -> bool {
        let mut re = false;
        for i in vec {
            if i < 0 {
                re = true;
            }
        }
        re
    }
    if contain_minus(vec.clone()) {
        if vec[0] as i64 * vec[1] as i64 > vec[vec.len() - 2] as i64 * vec[vec.len() - 3] as i64 {
            return vec[vec.len() - 1] as i64 * vec[0] as i64 * vec[1] as i64;
        }
    }
    return vec[vec.len() - 1] as i64 * vec[vec.len() - 2] as i64 * vec[vec.len() - 3] as i64; }
}
```

## Kata 4 (排序算法的实现 Sort Algorithm in Rust)

```rust
fn bubble_sort<T>(slice: &mut [T])
where
    T: Ord,
{
    let mut swapped = true;
    while swapped {
        swapped = false;
        for i in 1..slice.len() {
            if slice[i - 1] > slice[i] {
                slice.swap(i - 1, i);
                swapped = true;
            }
        }
    }
}

fn isertion_sort<T>(slice: &mut [T])
where
    T: Ord,
{
    for unsorted in 1..slice.len() {
        let i = match slice[..unsorted].binary_search(&slice[unsorted]) {
            Ok(i) => i,
            Err(err) => err,
        };
        slice[i..=unsorted].rotate_right(1);
    }
}

fn main() {
    let mut vec1 = vec![1, 2, 30, 40, 5, 6, 7];
    bubble_sort(&mut vec1);
    assert_eq!(vec1, vec![1, 2, 5, 6, 7, 30, 40]);
    println!("buble_sort {:?}", vec1);

    let mut vec2 = vec![10, 2, 30, 40, 5, 6, 7];
    isertion_sort(&mut vec2);
    assert_eq!(vec2, vec![2, 5, 6, 7, 10, 30, 40]);
    println!("isertion_sort {:?}", vec2);
}
```

## Kata 5 (最小移动次数，每次操作 n-1 各元素加 1，最终值相等)

```rust
#[allow(dead_code)]
/**
 * 输入：nums = [1,2,3]
输出：3
解释：
只需要3次操作（注意每次操作会增加两个元素的值）：
[1,2,3]  =>  [2,3,3]  =>  [3,4,3]  =>  [4,4,4]
*/
struct Solution {}
impl Solution {
    pub fn min_moves(nums: Vec<i128>) -> i128 {
        nums.iter().sum::<i128>() - nums.iter().min().unwrap() * nums.len() as i128
    }
}
fn main() {
    println!(
        "{}",
        Solution::min_moves(vec![11515115151, 100000000, 20000000000000000000000000])
    );
    println!("{}", Solution::min_moves(vec![1, 2, 3]));
}
```

## Kata 6 (Vec 中所有类型转化为 String)

```rust
macro_rules! vec_strs {
    (
        $($element:expr),*
    ) => {
        {
            let mut v = Vec::new();
            $(
                v.push(format!("{}", $element));
            )*
            v
        }
    };
}
fn main() {
    let s = vec_strs![1, "a", true, 3.14159f32];
    println!("{:?}", s); //["1", "a", "true", "3.14159"]
    assert_eq!(s, &["1", "a", "true", "3.14159"]);
}
```

## Kata 7 ( kmp 算法)

```rust
/**
描述
给你一个文本串 T ，一个非空模板串 S ，问 S 在 T 中出现了多少次
数据范围：1 \le len(S) \le 500000, 1 \le len(T) \le 10000001≤len(S)≤500000,1≤len(T)≤1000000
要求：空间复杂度 O(len(S))O(len(S))，时间复杂度 O(len(S)+len(T))O(len(S)+len(T))
示例1
输入：
"ababab","abababab"
复制
返回值：
2
* */
```

## Kata 8 (数字的幂 i64.pow(2 as u32))

```rust
#![allow(unused_imports)]
#![allow(unused_macros)]
#![allow(dead_code)]
#![allow(unused_variables)]
use proconio::{input, marker::*};
use std::cmp::*;
use std::collections::*;

//solution for problem A
pub mod a {
    pub fn run() {
        proconio::input! {
            a: i32, b: i32
        }
        println!("{}", 32i64.pow((a - b) as u32))
    }
}
```

## Kata 9 (判断输入的两个字符串中的 chars 是否相同，是->Yes，否->No)

```rust
#![allow(unused_imports)]
#![allow(unused_macros)]
#![allow(dead_code)]
#![allow(unused_variables)]
use proconio::{input, marker::*};
use std::cmp::*;
use std::collections::*;
//solution for problem B
pub mod b {
    pub fn run() {
        use proconio::{input, marker::*};
        input! {
            mut s: Chars,
            t: Chars,
        }
        if s.iter().zip(t.iter()).all(|(a, b)| a == b) {
            println!("Yes");
        } else {
            let mut f = false;
            for i in 0..s.len() - 1 {
                s.swap(i, i + 1);
                f |= s.iter().zip(t.iter()).all(|(a, b)| a == b);
                s.swap(i, i + 1);
            }
            if f {
                println!("Yes");
            } else {
                println!("No");
            }
        }
    }
}
```

## Kata 10 (Select Mul,把 String 分为二，parse 以后相乘，放到数组里 返回最大的 item)

```rust
/**
 * Sample Input 1
123
Sample Output 1
63
As described in Problem Statement, there are six ways to separate it:
12 and 3,
21 and 3,
13 and 2,
31 and 2,
23 and 1,
32 and 1.
The products of these pairs, in this order, are 36, 63, 26, 62, 23, 32, with 63 being the maximum.
 */
//solution for problem C
pub mod c {
    pub fn run() {
        use proconio::{input, marker::*};
        use std::collections::BTreeMap;
        input! {
            mut s: Chars,
        }
        //reverse
        fn reverse(phrase: String) -> String {
            let mut i = phrase.len();
            let mut reversed = String::new();

            while i > 0 {
                reversed.push(phrase.chars().nth(i - 1).unwrap());
                i -= 1;
            }
            reversed
        }
        let s = s.iter_mut().map(|x| x.to_string()).collect::<Vec<_>>();
        //generate bmap
        fn generate_bmap(s: Vec<String>) {
            let s_string = s.join("").to_string();
            let mut bmap: BTreeMap<String, String> = BTreeMap::new();
            for i in 1..s_string.len() {
                let mut s_string = s.clone().join("").to_string();
                let s_string_l = s_string.split_off(i);
                bmap.insert(s_string, s_string_l);
            }
            for i in 1..s_string.len() {
                let mut s_string = reverse(s.clone().join("").to_string());
                let s_string_l = s_string.split_off(i);
                bmap.insert(s_string, s_string_l);
            }
            let mut first_last_string = s.clone()[s.len() - 1].to_string();
            first_last_string.push_str(&s.clone()[0].to_owned());

            let mut middle_string = String::new();
            for i in 1..s.len() - 1 {
                middle_string.push_str(&s.clone()[i]);
            }
            bmap.insert(first_last_string, middle_string);

            let mut vec = vec![];
            for (v, k) in &bmap {
                vec.push(
                    v.to_owned().parse::<i128>().unwrap() * k.to_owned().parse::<i128>().unwrap(),
                );
            }
            vec.sort();
            println!("{:?}", vec[vec.len() - 1]);
            // println!("{:?}", bmap);
            // println!("{:?}", vec);
        }

        generate_bmap(s.clone());
    }
}
```

## Kata 11 (Online games)

```rust
//https://atcoder.jp/contests/abc221/tasks/abc221_d

mod d {
    pub fn run() {
        proconio::input! {
            n: usize,
            ab: [(u32, u32); n],
        }
        let mut m = std::collections::BTreeMap::new();
        for (a, b) in ab {
            *m.entry(a).or_insert(0) += 1;
            *m.entry(a + b).or_insert(0) -= 1;
        }
        // println!("{:?}", m);
        let mut d = vec![0; n + 1]; //if n=5,[0, 0, 0, 0, 0, 0]
                                    // println!("{:?}", &d);
        let mut p = 0;
        let mut k = 0;
        for (i, j) in m {
            d[k as usize] += i - p;
            p = i;
            k += j;
        }
        d.remove(0);
        println!(
            "{:?}",
            d.iter_mut()
                .map(|x| x.to_string())
                .collect::<Vec<_>>()
                .join(" ")
        );
    }
}
```

## Kata 12 (快速开平方根倒数算法)

```rust
#[allow(unused_macros)]
macro_rules! input {
    () => {{
        let mut string = String::new();
        std::io::stdin().read_line(&mut string).unwrap();
        string = string.to_string().trim().to_owned();
        string
    }};
}
fn main() {
    let data: f64 = input!().parse::<f64>().unwrap();
    println!("{}", fast_sqrt64(data) * fast_sqrt64(data));
    println!("{}", 1.0 / f64::sqrt(16.0 * 16.0));
}

use std::mem;

/**
 * used to compute the 1/sqrt(x*x)
 */
fn fast_sqrt64(number: f64) -> f64 {
    const MAGIC_U64: u64 = 0x5fe6ec85e7de30da;
    const THREEHALFS: f64 = 1.5;
    let x2: f64 = number * 0.5;
    let i: u64 = MAGIC_U64 - (unsafe { mem::transmute::<f64, u64>(number) } >> 1); // convert f64 to u64
    let y: f64 = unsafe { mem::transmute::<u64, f64>(i) }; // convert u64 to f64
    y * (THREEHALFS - (x2 * y * y))
}
```

## Kata 13 (生成和判断素数，prime number)

```rust
/** 生成素数*/
pub fn find_primes(n: usize) -> Vec<usize> {
    let mut result = Vec::new();
    let mut is_prime = vec![true; n + 1];
    for i in 2..=n {
        if is_prime[i] {
            result.push(i);
        }
        ((i * 2)..=n).into_iter().step_by(i).for_each(|x| {
            is_prime[x] = false;
        });
    }
    result
}
/**判断是否素数 */
pub fn is_prime(n: u64) -> bool {
        n == 2 || n % 2 > 0 && (3..=(n as f64).sqrt() as u64).step_by(2).all(|i| n % i > 0)
}
```

## Kata 14 (vec add each)

```rust
/**
 * Vec add each trait
 */
trait InIterator<Type:Copy>{
    fn each<Function:Fn(Type) -> Type>(&mut self,f:Function);
}
/**
 * each trait to Vec
 */
impl<Type:Copy> InIterator<Type> for Vec<Type>{
    fn each<Function:Fn(Type) -> Type>(&mut self,f:Function){
        let mut i = 0;
        while i < self.len(){
            self[i] = f(self[i]);
            i+= 1;
        }
    }
}

fn main(){
    let mut v:Vec<i128>= vec![1,50,65,100];
    v.each(|x| x*9999999999999999999999999999999999);
    eprintln!("{:?}",v);
}
```

## Kata 15 (生成菱形 \*图)

```rust
/**
 * Examples
A size 3 diamond:

 *
***
 *
 生成菱形 *图
 */
mod diamond {
    pub fn print(n: i32) -> Option<String> {
    if n < 0 || n % 2 == 0 {
        return None;
    }

    let n = n as usize;
    let diamond = (1..=n)
        .chain((1..n).rev())
        .step_by(2)
        .map(|i| format!("{}{}\n", " ".repeat((n - i) / 2), "*".repeat(i)))
        .collect();

    Some(diamond)
    }
}
fn main(){
    eprintln!("{}",diamond::print(3).unwrap());
}
```

## Kata 16 (找出 m 到 n 之间的 prime number 存到 vec)

```rust
/**
输入g,m,n
找出m到n之间的prime number 存到vec
vec中找出 任意两个数的差 ==g
输出这两个数Some(a,b)
*/
mod steps_in_primes{
    use std::convert::TryInto;
    pub fn step(g: i32, m: u64, n: u64) -> Option<(u64, u64)> {
    // your code
    // let mut vec:Vec<> = find_primes(n as usize);
    let mut vec:Vec<i128> = vec![];
    for i in m..=n{
        if is_prime(i as i128){
            vec.push(i as i128);
        }
    }
    // eprintln!("{:?}",vec);
    let mut re:Vec<i128> = vec![];
    for i in 0..vec.len()-1 {
        for j in i+1..vec.len()-1 {
            if vec[j] -vec[i] == g.try_into().unwrap(){
                re.push(vec[i].try_into().unwrap());
                re.push(vec[j].try_into().unwrap());
            }
        }
    }
    // eprintln!("{:?}",re);
    if re.len()<1{
        return None;
    }
    Some((re[0].try_into().unwrap(),re[1].try_into().unwrap()))
    }
    pub fn is_prime(n: i128) -> bool {
        n == 2 || n % 2 > 0 && (3..=(n as f64).sqrt() as u64).step_by(2).all(|i| n % i as i128 > 0)
    }
}

/**
输入g,m,n
找出m到n之间的prime number 存到vec
vec中找出 任意两个数的差 ==g
输出这两个数Some(a,b)
*/
mod steps_in_primes1{
    pub fn is_prime(p: u64) -> bool {
      p >= 2 &&
      (2..)
      .take_while(|q| q * q <= p)
      .all(|q| p % q != 0)
    }
    pub fn step(g: i32, m: u64, n: u64) -> Option<(u64, u64)> {
      (m..n)
      .map(|p| (p, p + g as u64))
      .filter(|&(p0, p1)| is_prime(p0) && is_prime(p1))
      .nth(0)
        }
}
```

## Kata 17 （分数相加 ，得到不可简化的分数）

```rust
/**
 * 分数相加 ，得到不可简化的分数
 * in:vec![(1, 2), (1, 3), (1, 4)]
 * 1/2 + 1/3 +1/4 = 6/12+4/12+3/12
 * out:Some((13, 12))
 *
*/
mod irreducible_sum_of_rationals{
    pub fn gcd(a: i64, b: i64) -> i64 {
        if b == 0 {
            a
        } else {
            gcd(b, a % b)
        }
    }

    pub fn sum_fracts(l: Vec<(i64, i64)>) -> Option<(i64, i64)> {
        if l.len() == 0 {
            None
        } else {
            let res = l.iter().fold((0, 1), |acc, item| {
                // dbg!(&acc,&item);
                let n = acc.0 * item.1 + acc.1 * item.0;
                // dbg!(n);
                let d = acc.1 * item.1;
                // dbg!(d);
                let g = gcd(n, d);
                // dbg!(g);
                (n / g, d / g)
            });
            // eprintln!("{}/{}",res.0,res.1); //13/12
            Some(res)
        }
    }

}
```

## Kata 18 (最大公约数)

```rust
//最大公约数
   pub fn gcd(a: i64, b: i64) -> i64 {
        if b == 0 {
            a
        } else {
            gcd(b, a % b)
        }
    }
```

## Kata 19 (最小公倍数)

```rust
//公式法求最小公倍数
pub fn lcm(a: i32,b: i32) -> i32 {
    a*b/gcd(a,b)
}
```

## Kata 20(前 n 个 prime number 的乘积)

```rust
/**
 * in:n :usize
 * out：前n个prime number的乘积
 */

mod primorial_of_a_number{
    pub fn num_primorial(n: usize) -> u64 {
        let mut vec = vec![];
        for i in 2..100{
            if is_prime(i as u64){
                vec.push(i);
            }
        }
        let mut count =0;
        let mut mul =1;
        for i in 0..vec.len(){
            mul*=vec[i];
            count += 1;
            if count==n{
                break;
            }
        }
        mul
    }
    pub fn is_prime(p: u64) -> bool {
      p >= 2 &&
      (2..)
      .take_while(|q| q * q <= p)
      .all(|q| p % q != 0)
    }
}
```

## Kata 21 (丢番图方程 , Diophantine Equation\*)

```rust
/**
 * 丢番图方程
 * Diophantine Equation
 * x2 - 4 * y2 = n
 https://www.codewars.com/kata/554f76dca89983cc400000bb/train/rust
 */
mod diophantine_equation{
    pub fn solequa(n: u64) -> Vec<(u64, u64)> {
    let mut result = vec![];
    if n % 4 == 2 { return result; } // early bailout
    let rn = (n as f64).sqrt() as u64;
    for a in 1u64..rn+1 {
        let b = n/a;
        if b*a != n || (b-a) % 4 != 0 { continue; }
        let y = (b-a) / 4;
        let x = a + 2*y;
        result.push((x,y));
    }
    result
    }
}
fn main(){
    eprintln!("{:?}",diophantine_equation::solequa(5)); //[(3, 1)]
    eprintln!("{:?}",diophantine_equation::solequa(20)); //[(6, 2)]
}
```

## Kata 22 (convet_char_vec_string_vec)

```rust
fn convet_char_vec_string_vec(vec:Vec<char>)->Vec<String> {
                    let mut v = vec![];
                    for i in vec.iter() {
                        if !i.is_ascii_whitespace(){
                        let mut s = "".to_string();
                        s.push(*i);
                        s.push_str(" ");
                        v.push(s);
                        }
                    }
                    v
}
```

## Kata 23 (assert type in rust)

```rust
pub mod rust_type_assert{
    pub fn run() {
        use std::any::Any;
        pub fn is_string(s: &dyn Any)->&str {
            if s.is::<String>() {
                return "It's a string!";
            } else {
            return "Not a string...";
            }
        }
        assert_eq!(is_string(&"aa"),"Not a string...");
        assert_eq!(is_string(&"aa".to_string()),"It's a string!");

        pub fn is_i64(s: &dyn Any)->&str {
            if s.is::<i64>() {
                return "It's a i64!";
            } else {
            return "Not a i64...";
            }
        }
        assert_eq!(is_i64(&12),"Not a i64...");
        assert_eq!(is_i64(&(12 as i64)),"It's a i64!");

    }
}
```

## Kata 24 (Casting binary float to integer)

```rust
/**
 * 10.0 (f32) == 01000001001000000000000000000000 (binary)
 * convert_to_i32(10.0) returns 1092616192 (i32)
 */
pub mod casting_binary_float_to_integer{
    // return binary representation as i32
    use std::cell::RefCell;

    pub fn convert_to_i32(f: f32) -> i32 {
        let ff:RefCell<f32> = RefCell::new(f);
        // eprintln!("2进制：{:b}", 10);
        // eprintln!("{:?}",  ff.clone().borrow_mut().to_bits() as i32);
        // println!("8进制：{:o}", 10);
        // println!("16进制：{:x}", 10);
         ff.clone().borrow_mut().to_bits() as i32
    }
    #[cfg(test)]
    mod tests {
        use super::*;
        #[test]
        fn provided_tests() {
            assert_eq!(convert_to_i32(10.0), 1092616192);
            assert_eq!(convert_to_i32(f32::INFINITY), 0x7f800000);
            assert_eq!(convert_to_i32(1.40129846432e-44), 10);
        }
    }

}
```

## Kata 25 (Cow in Rust)

```rust
//Cow
    pub mod cow_demo{
        use std::borrow::Cow;
        pub fn run(){
            fn abs_all(input: &mut Cow<[i32]>) {
                for i in 0..input.len() {
                    let v = input[i];
                    if v < 0 {
                        input.to_mut()[i] = -v;
                    }
                }
            }
            let slice = [0, -31, 2];
            let mut input = Cow::from(&slice[..]);
            abs_all(&mut input);
            input.to_mut().push(-120);
            println!("to_mut {:?}", input);

            //use from
            let s = Cow::from("alen ");
            println!("from {:?}", s.clone()+"andry");
            println!("from {:?}", s.clone().to_string());

            //use to_owned
            use std::borrow::Borrow;
            let b = Cow::from("ops b!");
            let cow_borrow = Cow::to_owned(&b);
            println!("cow_borrow: {:?}", cow_borrow.clone());

            //use from_iter
            use std::iter::FromIterator;
            let iter = Vec::from_iter([0,5,15].iter());
            let iter1 = Vec::from_iter((0..15).into_iter());
            let iter_cow = Cow::from_iter(iter);
            let iter_cow1 = Cow::from_iter(iter1.clone());
            println!("from_iter {:?}", iter_cow);
            println!("from_iter {:?}", iter_cow1);

            let find_7 = iter1.iter().find(|&&x| x == 7).unwrap();
            println!("iter1 include 7 : {:?}", *find_7==7);
        }}
```

## Kata 26 (Cell in Rust)

```rust
//Cell
    pub mod cell_demo{
        use std::cell::Cell;
        use std::cell::RefCell;
        struct Point{x:usize, y:usize,sum:Cell<Option<usize>>}

        impl Point {
            pub fn sum(&self) -> usize {
                match self.sum.get() {
                    Some(sum) => {
                        println!("{}",sum);
                        sum
                    },
                    None => {
                        let new_sum = self.x+self.y;
                        self.sum.set(Some(new_sum));
                        println!("sum set: {:?}",new_sum);
                        new_sum
                    }
                }
            }
        }
        pub fn run() {
            let p = Point{x:8,y:16,sum:Cell::new(None)};
            println!("{}",p.sum());
            println!("{}",p.sum());
        }
    }
```

## Kata 27 (RefCell in Rust)

```rust
 //RefCell
    pub mod refcell_demo{
        use std::cell::RefCell;
        struct Point{x:usize, y:usize,sum:RefCell<Option<usize>>}
        impl Point {
            pub fn sum(&self) -> usize {
                match self.sum.take() {
                    Some(sum) => {
                        println!("{}",sum);
                        sum
                    },
                    None => {
                        let new_sum = self.x+self.y;
                        self.sum.replace(Some(new_sum));
                        println!("sum set: {:?}",new_sum);
                        new_sum
                    }
                }
            }
        }
        pub fn run() {
            let p = Point{x:8,y:16,sum:RefCell::new(None)};
            println!("{}",p.sum());
            println!("{}",p.sum());
            use std::cell::RefCell;

            let c1 = RefCell::new(5);
            let ptr = c1.as_ptr();
            println!("{:?}",ptr);

            let mut c2 = RefCell::new(5);
            *c2.get_mut() += 1;
            assert_eq!(c2, RefCell::new(6));
            println!("{:?}",c2);
            println!("before take:{:?}",c2.take());
            println!("after take:{:?}",c2.take());
            println!("after take:{:?}",c2.take());
            println!("after take:{:?}",c2.take());
            let mut cc = *c2.borrow_mut();
            cc+=0;
            println!("{:?}",cc);
        }
    }
```

## Kata 28 (impl Drop trait in Rust)

```rust
pub mod drop_demo{
        struct Person{
            name: String,
        }
        impl Drop for Person{
            fn drop(&mut self) {
                println!("drop:{}",self.name);
            }
        }
        pub fn run(){
            let _alen = Person{name: "Alen".into()};
            let _andry = Person{name: "Andry".into()};
            eprintln!("{},{}",_alen.name,_andry.name);
        }
    }
```

## Kata 29 (每 n 个位组合存到 HashSet 中,已存的值重复的话 return false)

```rust
/**
 * https://www.codewars.com/kata/60aee6ae617c26004717d257/solutions
 */
#[allow(dead_code)]
#[allow(unused_variables)]
pub mod de_bruijn_sequences{
    use std::collections::HashSet;
    pub fn de_bruijn_sequence(sequence: &str, n: usize) -> bool {
        let mut vec_sequence: Vec<u8> = sequence.bytes().collect();
        vec_sequence.extend(vec_sequence[..n - 1].to_vec());
        eprintln!("{:?}",vec_sequence);

        let mut seen: HashSet<Vec<u8>> = HashSet::new();
        for i in 0..sequence.len() {
            if !seen.insert(vec_sequence[i..(i + n)].to_vec()) {
                return false;
            }
        }
        //每n个位组合存到HashSet中,已存的值重复的话return false
        eprintln!("{:?}",seen);
        true
    }
    #[cfg(test)]
    mod tests {
    use super::*;
    #[test]
    fn sample_tests() {
        assert_eq!(de_bruijn_sequence("0011", 2), true);//01，00，11，10
        assert_eq!(de_bruijn_sequence("abcd", 2), true);
        assert_eq!(de_bruijn_sequence("0101", 2), false);
        assert_eq!(de_bruijn_sequence("11231", 2), false);
        assert_eq!(de_bruijn_sequence("aabca", 3), true);
        assert_eq!(de_bruijn_sequence("00000111011010111110011000101001", 5), true);
        assert_eq!(de_bruijn_sequence("11111000001110110011010001001010", 5), true);
        assert_eq!(de_bruijn_sequence("0011123302031321", 2), false);
        }
    }

}
```

## Kata 30 (很大数的乘积和很大数的幂)

```rust
/**
 * power function for large numbers,multiply large numbers
 * 很大数的乘积和很大数的幂
 */
#[allow(dead_code)]
#[allow(unused_variables)]
#[allow(unused_mut)]
pub mod power_function_for_large_numbers{
    pub fn power(a:String, b:String) -> String {
        let mut s = a.clone();
        for i in 0..b.parse::<i32>().unwrap()-1 {
            // println!("{}",s);
            s=mul(s.clone(),a.clone());
        }
        fn mul(a:String,aa:String)-> String {
            multiply_large_numbers(a.clone(),aa.clone())
        }
        s
    }
    pub fn multiply_large_numbers(num1:String, num2:String)->String{
        let len1 = num1.len();
        let len2 = num2.len();
        let num1_str:Vec<i32> = num1.split("")
                .filter(|s| !s.is_empty())
                .collect::<Vec<_>>().iter().map(|s| s.parse::<i32>().unwrap()).collect();
        let num2_str:Vec<i32> = num2.split("")
                .filter(|s| !s.is_empty())
                .collect::<Vec<_>>().iter().map(|s| s.parse::<i32>().unwrap()).collect();

        if len1 == 0 || len2 == 0 {
            return "0".into();
        }
        let mut  result:Vec<i32> = "0".repeat(len1+len2).split("")
                .filter(|s| !s.is_empty())
                .collect::<Vec<_>>().iter()
                .map(|s| s.parse::<i32>().unwrap()).collect();
        let mut i_n1 = 0;
        let mut i_n2 = 0;
        for i in 0..len1{
            let ii = len1-i-1;
            let mut carry = 0;
            let mut n1 = num1_str[ii];
            let mut i_n2 = 0;
            for j in 0..len2{
                let jj = len2-j-1;
                let mut n2 = num2_str[jj];
                let mut summ = n1 * n2 + result[i_n1 + i_n2] + carry;
                let carry = summ;
                let sum_i_n = i_n1+i_n2;
                result[sum_i_n] = summ % 10;
                i_n2 += 1;
            }
             if carry > 0{
                result[i_n1 + i_n2] += carry
             }
            i_n1 += 1;
        }
        let mut i:i32 = result.len() as i32 - 1;
        while i>=0 && result[i as usize] == 0{
            i -= 1
        }
        if i == -1{
            return "0".into()
        }
        let mut s:String = "".into();
        while i >= 0{
            s.push_str(&result[i as usize].to_string());
            i -= 1;
        }
        return s
    }

    #[cfg(test)]
    mod tests {
        use super::*;
        #[test]
        fn test_power() {
            assert_eq!(power(String::from("10"),String::from("7")),"10000000");
        }
    }
}
```

## Kata 31 (Merge Two Vec and Return median number)

```rust
pub mod mearge_two_vec_return_median{
    use std::convert::TryInto;
    pub fn mearge_vec<T:Clone+Ord>(a:Vec<T>,b:Vec<T>) -> T
    where
    T: std::ops::Add<Output = T>+Ord+Clone+Copy+std::ops::Div<Output = T>+std::convert::Into<T>+From<i32>,
    {
        let mut a = a.clone();
        for item in b.iter() {
            a.push(*item);
        }
        a.sort();
        let l = a.len();
        if l%2 !=0 {
        let mid = a.len()/2;
        let mid_num = a[mid];
        return mid_num;
        }else{
        let mid = a.len()/2;
        let mid_num = a[mid]+a[mid-1];
        return mid_num.into() /2.into();
        }
    }
}
```

## Kata 32 (String add split_to_vec tarit)

```rust
pub mod string_add_trait{
    trait SplitToVec{
        fn split_to_vec(self,word:String)->Vec<String>;
    }
    impl SplitToVec for String{
        fn split_to_vec(self,word:String)->Vec<String>{
            let v = self.split(&word).filter(|s|!s.is_empty()).collect::<Vec<&str>>();
            v.iter().map(|s| s.to_string()).collect::<Vec<_>>()
        }
    }
    pub fn run_string(){
        let s = String::from("name: alen andry");
        let v = s.split_to_vec(" ".into()); //["name:", "alen", "andry"]
        println!("{:?}", v);
    }
}
```

## Kata 33 (字符串中字符的出现次数统计)

```rust
// code war problems url :https://www.codewars.com/kata/57a6633153ba33189e000074/train/rust
// Example:
// ordered_count("abracadabra") == vec![('a', 5), ('b', 2), ('r', 2), ('c', 1), ('d', 1)]
#[allow(dead_code)]
#[allow(unused_variables)]
#[allow(unused_mut)]
use std::collections::BTreeMap;
fn ordered_count(sip: &str) -> Vec<(char, i32)> {
    let sip = sip.to_owned();
    let set_sip = sip.clone();
    let mut arr_sip: Vec<char> = set_sip.chars().collect();
    arr_sip.sort();
    arr_sip.reverse();
    // println!("{:?}", arr_sip);
    let mut bmap = BTreeMap::new();
    for x in arr_sip {
        bmap.insert(x, count_x_in_sip(&sip, x));
    }
    // println!("{:?}", bmap);
    fn count_x_in_sip(sip: &str, target: char) -> i32 {
        let mut c: i32 = 0;
        for x in sip.chars() {
            if target == x {
                c += 1;
            }
        }
        return c;
    }
    // bmap to tuple vec
    fn convert_bmap_to_vec(bmap: BTreeMap<char, i32>) -> Vec<(char, i32)> {
        let mut vec = vec![];
        for (v, k) in &bmap {
            vec.push((v.to_owned(), k.to_owned()));
        }
        return vec;
    }
    return convert_bmap_to_vec(bmap);
}
```

## Kata 34 (find most common element 找出出现次数最多的元素)

```rust
fn main() {
    /*{"a": 2, "b": 3, "m": 1, "s": 3}
    common item val :"b"
    common item index :1
    common item val :"s"
    common item index :3
    */
    let str = "aabbbssms";
    fn find_most_common(str: &str) -> [(&str, i32); 1] {
        let mut bmap = BTreeMap::new();
        let str_vec = str.split("").filter(|s| !s.is_empty()).collect::<Vec<_>>();
        for i in 0..str_vec.len() {
            if !bmap.contains_key(str_vec[i]) {
                bmap.insert(str_vec[i], 1);
            } else {
                let mut count = bmap
                    .get(str_vec[i])
                    .unwrap()
                    .to_string()
                    .parse::<i32>()
                    .unwrap();
                count += 1;
                bmap.insert(str_vec[i], count);
            }
        }
        fn find_max<I>(iter: I) -> Option<I::Item>
        where
            I: Iterator,
            I::Item: Ord,
        {
            iter.reduce(|a, b| if a >= b { a } else { b })
        }
        println!("{:?}", bmap);
        // println!("{:?}", bmap.keys());
        // println!("{:?}", bmap.values());
        for (index, item) in bmap.values().enumerate() {
            if item == find_max(bmap.values()).unwrap() {
                let vec: Vec<&str> = bmap.keys().cloned().collect();
                println!("common item val :{:?}", vec[index]);
                println!("common item index :{:?}", index);
            }
        }
        // println!("{:?}", find_max(bmap.values()).unwrap());
        return [("", find_max(bmap.values()).unwrap().to_owned())];
    }
    find_most_common(str);
}
```

## Kata 35 (Sort float Vec 从小到大 排序)

```rust
fn main() {
    //sort 从小到大 排序
    let mut vec = vec![100.1, 1.15, 5.5, 1.123, 2.0];
    vec.sort_by(|a, b| a.partial_cmp(b).unwrap());
    println!("{:?}", vec);
    assert_eq!(vec, vec![1.123, 1.15, 2.0, 5.5, 100.1]);
}
```

## Kata 36 (slice String, use input!() read string)

```rust
#[allow(unused_variables)]
        fn slice_string(in_string: String, start: i32, end: i32) -> String {
            let mut s = Vec::new();
            let in_string_vec = in_string
                .split("")
                .filter(|s| !s.is_empty())
                .collect::<Vec<_>>();
            if start < 0 && end > in_string_vec.len() as i32 {
                return "out of range".to_owned();
            } else {
                for i in start..end {
                    s.push(in_string_vec[i as usize]);
                }
            }
            return s.join("").to_string();
        }
```

## 自己定义的 input!() (快速 IO 输入值)

```rust
#[allow(unused_macros)]
macro_rules! input {
    () => {{
        let mut string = String::new();
        std::io::stdin().read_line(&mut string).unwrap();
        string
    }};
}
fn main() {
    let s = input!();
    println!("{:?}", s); //"alen andry\n"
    assert_eq!("alen andry\n".to_string(), s);
}
```

## Kata 37 (输出 String 的全排序)

```rust
  // input '123' 输出string的全排序
  // ["1", "12", "123", "2", "23", "3"]
pub mod c {
    pub fn run() {
        use proconio::{input, marker::*};
        input! {
            mut s: Chars,
        }
        let s = s.iter_mut().map(|x| x.to_string()).collect::<Vec<_>>();
        // println!("{:?}", s);
        #[allow(unused_variables)]
        fn slice_string(in_string: String, start: i32, end: i32) -> String {
            let mut s = Vec::new();
            let in_string_vec = in_string
                .split("")
                .filter(|s| !s.is_empty())
                .collect::<Vec<_>>();
            if start < 0 && end > in_string_vec.len() as i32 {
                return "out of range".to_owned();
            } else {
                for i in start..end {
                    s.push(in_string_vec[i as usize]);
                }
            }
            return s.join("").to_string();
        }
        // let some_string = slice_string(s_string, 0, 3);
        // println!("{:?}", some_string);
        let s_string = s.join("").to_string();
        let mut out_vec = Vec::new();
        for i in 0..s.len() + 1 {
            for j in i + 1..s.len() + 1 {
                out_vec.push(slice_string(s_string.clone(), i as i32, j as i32));
            }
        }
        println!("{:?}", out_vec);
        // input '123' 输出string的全排序
        // ["1", "12", "123", "2", "23", "3"]
    }
}

fn main() {
    c::run();
}
```

## Kata 38 (各位相加到小于 9 时输出合)

```rust
/*
各位相加到小于9 时输出
imput 15 ->6
imput 19 ->1
imput 238 ->4
*/

pub mod c {
    pub fn run() {
        use proconio::{input, marker::*};
        input! {
            mut s: Chars,
        }
        let s = s
            .iter_mut()
            .map(|x| x.to_string().parse::<i32>().unwrap())
            .collect::<Vec<_>>();
        // println!("{:?}", s);
        fn count(arr: Vec<i32>) -> i32 {
            let mut sum = 0;
            for i in 0..arr.len() {
                sum += arr[i];
            }
            if sum <= 9 {
                println!("{:?}", sum);
            } else {
                let arr = sum
                    .to_string()
                    .chars()
                    .map(|x| x.to_string().parse::<i32>().unwrap())
                    .collect::<Vec<_>>();
                // println!("{:?}", arr);
                count(arr);
            }
            return 0;
        }
        count(s);
    }
}


fn main() {
    c::run();
}
```

## Kata 39 (选择排序 slection_sort)

```rust
#[allow(dead_code)]
// code war problems url :https://www.codewars.com/kata/5861d28f124b35723e00005e/train/rust
pub fn slection_sort(arr: &Vec<i32>) -> Vec<i32> {
    // write code here
    let length = arr.len();
    let mut arr = arr.to_owned();
    let mut minindex;
    let mut temp;
    for i in 0..length - 1 {
        minindex = i;
        for j in i + 1..length {
            if arr[j] < arr[minindex] {
                minindex = j;
            }
        }
        temp = arr[i];
        arr[i] = arr[minindex];
        arr[minindex] = temp;
    }
    return arr;
}
```

## Kata 40 (vec 中删除重复的部分)

```rust
#[allow(dead_code)]
#[allow(unused_variables)]
#[allow(unused_mut)]

pub fn run() {
    fn unique_in_order<T>(sequence: T) -> Vec<T::Item>
    where
        T: std::iter::IntoIterator,
        T::Item: std::cmp::PartialEq + std::fmt::Debug,
    {
        let mut v: Vec<_> = sequence.into_iter().collect();
        v.dedup();
        v
    }
    let data = vec!["A", "A", "B", "b", "b", "b"];
    let data2 = "AAAABBBCCDAABBB".chars();
    println!("{:?}", unique_in_order(data));   //["A", "B", "b"]
    println!("{:?}", unique_in_order(data2));  //['A', 'B', 'C', 'D', 'A', 'B']
}
```

## Kata 41 (Rust implement fib function )

```rust
pub fn run() {
    //produce fib
    fn product_fib(prod: u64) {
        // your code
        let mut p: i64 = prod as i64;
        fn fib(n: u64) -> u64 {
            match n {
                0 => 1,
                1 => 1,
                _ => fib(n - 1) + fib(n - 2),
            }
        }
        let mut list: Vec<u64> = Vec::new();
        while p > -1 {
            list.push(fib(p as u64));
            p -= 1;
        }
        println!("{:?}", list);
    }
    product_fib(8); //produce 8 number
}
```

## Kata 42 (Lettcode two_sum problem solution in rust)

```rust
use std::collections::HashMap;

pub fn run(){
        fn two_sum(nums: Vec<i32>,taget:i32)-> Vec<i32>{
            let mut h_map = HashMap::new();
            for i in 0..nums.len(){
                if let Some(&j) = h_map.get(&(taget-nums[i])){
                    return vec![j as i32,i as i32];
                }
                else{
                    h_map.insert(nums[i],i);
                }
            }
            vec![]
        }
        let result = two_sum(vec![1,2,0,2],2);
        println!("{:?}",result);

}
```

## Kata 43 (Use mutex  多线程共享一个值)

```rust
pub mod mutex {
    pub fn run() {
        use std::sync::Mutex;
        let l: &'static _ = Box::leak(Box::new(Mutex::new(0.0)));
        let handlers = (0..999)
            .map(|_| {
                std::thread::spawn(move || {
                    for _ in 0..9999 {
                        *l.lock().unwrap() += 0.0001;
                    }
                })
            })
            .collect::<Vec<_>>();
        for handler in handlers {
            handler.join().unwrap();
        }
        assert_eq!(*l.lock().unwrap(), 999.0 * 9999.0);
    }
}
```

## Kata 44 (implment default for type)

```rust
pub mod implment_default {
    struct Grounded;
    impl Default for Grounded {
        fn default() -> Self {Grounded}
    }
    struct Launched;
    // and so on
    struct Rocket<Stage = Grounded> {
        stage: std::marker::PhantomData<Stage>,
    }
    impl Default for Rocket<Grounded> 
    where
        Grounded:Default,
    {
        fn default() -> Self {
            Rocket{stage:std::marker::PhantomData}
        }
    }
    impl Rocket<Grounded> {
        pub fn launch(self) -> Rocket<Launched> {
            Rocket{stage:std::marker::PhantomData}
        }
    }
    impl Rocket<Launched> {
        pub fn accelerate(&mut self) {}
        pub fn decelerate(&mut self) {}
    }
    struct Color;
    struct Kilograms;

    impl<Stage> Rocket<Stage> {
        pub fn color(&self) -> Color {Color}
        pub fn weight(&self) -> Kilograms {Kilograms}
    }
}

```

## Kata 45 (Use Cow)

```rust
#[allow(unused)]
pub mod use_cow {
    use std::borrow::Cow;
    use std::sync::Arc;
    fn test(ref a: String) {
        eprintln!("{:?}", a);
    }
    fn test1(v: &mut Vec<&str>) {
        v.push("z");
        v.push("x");
        v.push("y");
        for item in v.splitn(3, |s| *s == "x") {
            println!("split:  {:?}", item);
        }
        v.reverse();
        eprintln!("{:?}", v);
    }

    pub fn run() {
        let s = String::from("ok");
        test(Cow::from(&s).clone().to_string());
        eprintln!("{:?}", s);

        let mut v = vec!["a", "b"];
        test1(&mut Cow::from(&v).clone().to_vec());
        v.sort();
        eprintln!("{:?}", v.join(&" "));
        eprintln!("{:?}", v);
    }
}
```

## Kata 46 (二维Vec  sort_by_row)

```rust
pub fn sort_by_row(arr: Vec<Vec<f64>>,row:usize) -> Vec<Vec<f64>> {
        // write code here
        let length = arr[row].len();
        let mut arr = arr.to_owned();
        let mut minindex;
        for i in 0..length - 1 {
            minindex = i;
            for j in i + 1..length {
                if arr[row][j] > arr[row][minindex] {
                    minindex = j;
                }
            }
            for k in 0..row+1{
                arr[k].swap(minindex,i);
            }
        }
        return arr;
    }
```

## Kata 47 (*Implement clonal selection algorithm*)

```rust
pub mod clonal_selection_algorithm {
    use rand::{thread_rng, Rng};
    pub fn y(a: f64, b: f64) -> f64 {
        let aa = -30.0 * f64::powf(b, 4.0);
        let bb = 64.0 * f64::powf(b, 3.0);
        let cc = 43.8 * f64::powf(b, 2.0);
        let dd = 10.8 * f64::powf(b, 1.0);
        let ee = (aa + bb + cc + dd) * 1000.0 * f64::sin(5.0 * std::f64::consts::PI * a);
        let ff = 1.0 + 0.1 * f64::powf(a, 2.0);
        f64::abs(ee / ff)
    }
    pub fn cloning_number(beta: f64, population_number: f64, i: f64) -> f64 {
        f64::floor((beta * population_number) / i)
    }
    pub fn generate_three_random(population_number: i32) -> Vec<Vec<f64>> {

        fn generate() -> f64 {
            let mut rng = thread_rng();
            let m: f64 = rng.gen_range(0.0..1.0);
            m
        }
        let mut temp: Vec<f64> = Vec::new();
        let mut temp2: Vec<f64> = Vec::new();
        let mut temp_fitness: Vec<f64> = Vec::new();
        for i in 0..population_number as usize {
            temp.push(generate());
            temp2.push(generate());
            temp_fitness.push(y(temp[i], temp2[i]));
        }
        vec![temp, temp2, temp_fitness]
    }
    pub fn sort_by_row(arr: Vec<Vec<f64>>,row:usize) -> Vec<Vec<f64>> {
        // write code here
        let length = arr[row].len();
        let mut arr = arr.to_owned();
        let mut minindex;
        for i in 0..length - 1 {
            minindex = i;
            for j in i + 1..length {
                if arr[row][j] > arr[row][minindex] {
                    minindex = j;
                }
            }
            for k in 0..row+1{
                arr[k].swap(minindex,i);
            }
        }
        return arr;
    }
    pub fn mutaition(clon: Vec<&Vec<f64>>, theta: f64) -> Vec<Vec<f64>> {
        fn generate() -> f64 {
            let mut rng = thread_rng();
            let m: f64 = rng.gen_range(0.0..1.0);
            m
        }
        let mut mutation = vec![];
        let clon = clon;
        let mut clon1: Vec<Vec<f64>> = vec![];

        let len_clon = clon.len();
        for _ in 0..len_clon {
            let mut vec = vec![];
            for _ in 0..clon[0].len() {
                vec.push(generate());
            }
            mutation.push(vec.clone());
            clon1.push(vec.clone());
        }
        for i in 0..mutation.len() {
            for j in 0..mutation[0].len() {
                    clon1[i][j] = clon[i][j];
            }
        }
        for i in 0..mutation.len() {
            for j in 0..mutation[0].len() {
                if mutation[i][j] < theta {
                    clon1[i][j] = generate();
                }
            }
        }
        let mut yy = vec![];
        for j in 0..clon1[0].len() {
            yy.push(y(clon1.clone()[0][j],clon1.clone()[1][j]));    
        }
        clon1.push(yy);
        clon1
    }
    
    #[allow(unused)]
    pub fn run() {
        let mut iteration_number: i32 = 2;
        let mut population_number: i32 = 4;
        let mut n: usize = 10;
        let mut beta: f64 = 5.0;
        let mut theta: f64 = 0.2;
        let population = generate_three_random(population_number);
        let mut selected_population: Vec<f64> = vec![];
        let new_population = sort_by_row(population.clone(),2);
        let selected_population = vec![&new_population[0], &new_population[1]];
        // println!("population {:#?}", population.clone());
        // println!("new_population {:#?}", new_population.clone());
        // println!("selected_population {:#?}", selected_population.clone());
        let clone: Vec<&Vec<f64>> = selected_population.clone();
        let new_clone = new_population.clone();
        let last_population = new_clone.clone();
        // println!("clone:{:#?}", &clone);
        // println!("new_clone:{:#?}", &new_clone);
        // println!("new_clone:{:#?}", &last_population);
        let mutationed = mutaition(clone.clone(), theta);
        println!("mutationed:{:#?}", &mutationed);
        let mut sorted_mutation = sort_by_row(mutationed.clone(),2).to_owned();
        println!("sorted_mutation:{:#?}", &sorted_mutation);
    }
}

```

## Kata 48 (*Implement coin_change problem* 还钱问题)

```rust
pub mod coin_change{
    pub fn solution(coins:Vec<i32>,amount:i32)->i32{
        let mut max = amount+1; 
        let mut dp = (0..max).map(|_|{amount+1}).collect::<Vec<_>>();
        dp[0]=0;
        for i in 1..=amount as usize{
            for j in 0..coins.len(){
                if coins[j] as usize <= i{
                    dp[i]=std::cmp::min(dp[i], dp[i-coins[j] as usize]+1);
                }
            }
        }
        let mut re:i32;
        if dp[amount as usize]>amount{
            re = -1;
        }else{
            re = dp[amount as usize];
        }
        println!("{:?}", &dp);
        println!("{:?}", &re);
        re
    }
    pub fn run(){
        solution(vec![2], 3);//-1
        solution(vec![1,2,5], 11); //3
    }
}
```


## Kata 49 (use Atomic implement mutex)

```rust
pub mod implement_mutex {
    #[allow(dead_code)]
    #[allow(unused)]
    use std::cell::UnsafeCell;
    use std::sync::atomic::{AtomicBool, Ordering};
    const LOCKED: bool = true;
    const UNLOCKED: bool = false;
    pub struct Mutex<T> {
        locked: AtomicBool,
        v: UnsafeCell<T>,
    }

    impl<T> Mutex<T> {
        fn new(t: T) -> Self {
            Self {
                locked: AtomicBool::new(UNLOCKED),
                v: UnsafeCell::new(t),
            }
        }
        fn with_lock<R>(&self, f: impl FnOnce(&mut T) -> R) -> R {
            while self
                .locked
                .compare_exchange(UNLOCKED, LOCKED, Ordering::Acquire, Ordering::Acquire)
                .is_err()
            {
                while self.locked.load(Ordering::Relaxed) == LOCKED {
                    std::thread::yield_now();
                }
                std::thread::yield_now();
            }
            // self.locked.store(LOCKED,Ordering::Relaxed);
            let ret = f(unsafe { &mut *self.v.get() });
            self.locked.store(UNLOCKED, Ordering::Release);
            ret
        }
    }
    unsafe impl<T> Sync for Mutex<T> where T: Send {}
    unsafe impl<T> Send for Mutex<T> where T: Send {}
    pub fn thread_handlers() {
        let l: &'static _ = Box::leak(Box::new(Mutex::new(0)));

        let handlers = (0..999)
            .map(|_| {
                std::thread::spawn(move || {
                    for _ in 0..999 {
                        l.with_lock(|v| {
                            *v += 1;
                        });
                    }
                })
            })
            .collect::<Vec<_>>();

        for handler in handlers {
            handler.join().unwrap();
        }
        assert_eq!(l.with_lock(|v| *v), 999 * 999);
    }
    pub fn atomic_demo() {
        use std::sync::atomic::AtomicUsize;
        let x: &'static _ = Box::leak(Box::new(AtomicBool::new(false)));
        let y: &'static _ = Box::leak(Box::new(AtomicBool::new(false)));
        let z: &'static _ = Box::leak(Box::new(AtomicUsize::new(0)));

        let _tx = std::thread::spawn(move || {
            x.store(true, Ordering::SeqCst);
        });
        let _ty = std::thread::spawn(move || {
            y.store(true, Ordering::SeqCst);
        });
        let t1 = std::thread::spawn(move || {
            while !x.load(Ordering::Acquire) {
                if y.load(Ordering::Acquire) {
                    z.fetch_add(1, Ordering::Release);
                }
            }
        });

        let t2 = std::thread::spawn(move || {
            while !y.load(Ordering::Acquire) {
                if x.load(Ordering::Acquire) {
                    z.fetch_add(1, Ordering::Release);
                }
            }
        });

        t1.join().unwrap();
        t2.join().unwrap();

        let z = z.load(Ordering::SeqCst);
        eprintln!("{:?}", z);
    }

    pub fn run() {
        // thread_handlers();
        atomic_demo();
    }
}

```
