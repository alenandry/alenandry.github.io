# Rust learn notebook

## trait in rust

```rust
struct Person{
    name:String,
    age:i128
}

trait VoiceBox {
    // speak
    fn speak(&self);
    // can speak
    fn can_speak(&self) ->bool;
}

impl VoiceBox for Person{
    fn speak(&self) {
        println!("I am {}",self.name);
    }
    fn can_speak(&self) ->bool {
        if self.age>0{
            return true;
        }else{
            return false;
        }
    }
}

pub fn run(){
    let this_person = Person{name:String::from("Alen"),age:24};

    println!("{}can speak?{}",this_person.name,this_person.can_speak());
    this_person.speak();
}
```

## BTreeMap (类似于 python 的 map，js 的 Set) ，val 不能重复

```rust
#[allow(unused_variables)]
use std::collections::BTreeMap;

pub fn run() {
    let mut each_value = String::new();
    std::io::stdin().read_line(&mut each_value).unwrap();

    let mut bmap = BTreeMap::new();
    bmap.insert("A", 1);
    bmap.insert("B", 2);
    bmap.insert("C", 3);
    bmap.insert("D", 4);
    bmap.insert("E", 5);
    println!("{:?}", bmap);
    // remove key-value
    bmap.remove("C");
    println!("{:?}", bmap);

    // check for a specific one.
    if !bmap.contains_key("C") {
        //有的话return true 没有的话false
        println!("{:?}", "C not font");
    }

    let mut data_vector = vec!["A", "B", "D"];
    let str_value: &str = &each_value;
    data_vector.push(str_value);
    println!("{:?}", data_vector);
    let mut out = BTreeMap::new();
    for i in data_vector.iter() {
        if bmap.get(i) != None {
            let get_val = bmap.get(i);
            out.insert(get_val, get_val);
            println!("{:?}", get_val.to_owned());
        }
    }
}
```

## Types in rust

```rust
pub fn run() {
    // 默认情况下rust不需要声明
    let x = 3; //默认i32

    let y = 2.5; //默认f64

    //添加声明
    let k: i64 = 4515165161;

    // i8最大小值
    println!("MIN i8 {}", std::i8::MIN);
    println!("MAX i8 {}", std::i8::MAX);
    // i32最大小值
    println!("MIN i32 {}", std::i32::MIN);
    println!("MAX i32 {}", std::i32::MAX);

    // i64最大小值
    println!("MIN i64 {}", std::i64::MIN);
    println!("MAX i64 {}", std::i64::MAX);
    // i128最大小值
    println!("MIN i128 {}", std::i128::MIN);
    println!("MAX i128 {}", std::i128::MAX);

    // isize （有符合）
    let var_isize: isize = 9223372036854775807;
    println!("{}", var_isize);

    // usize (无符号)
    let var_usize: usize = 1515;
    println!("{}", var_usize);

    //布尔类型
    let name = true;
    //声明布尔类型
    let is_big: bool = 10 > 5;
    let face = '\u{1f151}';

    let a = 'a'; //char

    println!("{:?}", (x, y, k, name, is_big, a, face));

    // 无符号数
    let data: u8 = 150;
    println!("{:?}", data);
    let data: u16 = 150;
    println!("{:?}", data);
    let data: u32 = 150;
    println!("{:?}", data);
    let data: u64 = 150;
    println!("{:?}", data);
    let data: u128 = 150;
    println!("{:?}", data);

    // 浮点数
    let float_num: f32 = 2.;
    println!("{}", float_num);
    let float_num: f64 = 0.22222222;
    println!("{}", float_num);

    // char 字符
    let chars: char = 'A'; //need to  be '' ,not can be ""
    let cn_name: char = '艾';
    println!("{},{}", chars, cn_name);

    // change type in rust
    // int to float or u64,u32..
    // as
    let int_data: i32 = 2020;
    let float_data = int_data as f32;
    let u64_data: u64 = int_data as u64;
    println!("int to float:{}", float_data + 0.5);
    println!("int to u64:{}", u64_data);
}
```

## Vector in rust

```rust
//vector是向量
pub fn run() {
    let mut n: Vec<i32> = vec![1, 2, 3, 4, 5, 6, 7, 8, 9, 0]; //[元素属性；向量的元素个数]

    //改某一个元素值
    n[9] = 10;

    //添加元素
    n.push(23); //最后面添加元素
    n.push(15);
    //删除最后一个元素
    let popeditem = n.pop();
    // 输出删除的元素
    println!("poped itemis :{}", popeditem.unwrap());
    println!("{:#?}", n); //竖直输出
    println!("{:?}", n); //横向输出
                         //单一输出
    println!("frist value:{:?}", n[0]); //输出第一个元素
    println!("last value:{:?}", n[n.len() - 1]); //输出最后一个元素

    //向量长度
    println!("向量长度：{}", n.len());
    //向量所占空间
    println!("occupies {} byte", std::mem::size_of_val(&n)); //每一个元素占4byte

    //向量切片
    let s = &n[0..5]; //从第0到第4个元素
    println!("{:?}", s);

    //向量的遍历
    for x in n.iter() {
        println!("{}", x);
    }
    //向量遍历时改值
    for x in n.iter_mut() {
        *x *= 3; //每一个元素乘2
    }
    println!("{:?}", n);
}
```

## VecDeque （双向链表）

```rust
use std::{collections::VecDeque};

pub fn run(){
    let mut buff = VecDeque::new();
    // add to front buffer
    buff.push_front(1);
    buff.push_front(4);
    // add to end buffer
    buff.push_back(10);
    buff.push_back(40);
    println!("{:?}", buff);

    // Swaps elements at indices i and j.
    buff.swap(0, 2);
    println!("{:?}",buff);

    //get capacity 占的空间
    let len = buff.capacity();
    println!("{}",len);

    //get length
    let length = buff.len();
    println!("{}",length);

    buff.reserve_exact(len);
    println!("{:?}",buff);

    //to Vec
    let c: Vec<&i32> = buff.iter().collect();
    println!("vec: {:?}",c);

    //lop value
     for num in buff.iter() {
    let val = *num;
    println!("{}",val);
    }

    //loop value and change
    for num in buff.iter_mut() {
    *num = *num - 2;   }

    println!("{:?}",buff);


}
```

## enum in rust

```rust
#[allow(dead_code)]
enum Alphabet{
    A,
    B,
    C,
    D,
    E,
    Z,
    W
}
impl Alphabet {
    fn is_end_leter(&self) ->bool{
        match self {
        &Alphabet::Z =>return true,
        _ =>return false
        }
    }
}
pub fn run(){
    let d = Alphabet::Z;

    println!("{:?}",d.is_end_leter());

}



//another example

enum Colors {
    Red = 0xff0000,
    Black = 0x000fff,

}


struct Bank{
    pub cardnumber: String,
    pub amount: f32,

}


enum Payments {
    Cash(f32),
    CirditCard(String,f32),
    BankCard(Bank),
    OnlineCard{user:String,amount:f32},
}

pub fn run(){
    // use color enum
    println!("{:06x}",Colors::Red as i32);
    println!("{:06x}",Colors::Black as i32);

    //use Payments enum
    let cashpay = Payments::Cash(3000000.5);
    process_payment(cashpay);

    let cc_pay = Payments::CirditCard("jiaotong".to_owned(),1000000.66);
    process_payment(cc_pay);
    let bank_pay = Payments::BankCard(Bank{cardnumber:"622000111222111".to_owned(),amount:23000.});
    process_payment(bank_pay);

    let online = Payments::OnlineCard{user:"Alen".to_owned(),amount:600000.};
    process_payment(online);
}

fn process_payment(pay:Payments){
    match pay{
        Payments::Cash(amt)=> {println!("It is{}",amt);}
        Payments::CirditCard(_,amt)=> {println!("It is{}",amt);}
        Payments::BankCard(data)=> {println!("It is{} {}",data.cardnumber,data.amount);}
        Payments::OnlineCard{user,amount}=> {println!("It is{} {}",user,amount);}

    }
}
```

## sum up ascii_code

```rust
fn sum_up_ascii_code(b: String) -> f64 {
       let mut sum: u32 = 0;
       for i in b.chars() {
           sum += i as u32
       }
       return (sum as i32) as f64;
   }
   let result_1 = sum_up_ascii_code("AB".to_string());
   println!("{}", result_1);
```

## Cell in rust

```rust
#[allow(unused_variables)]
use std::cell::Cell;
/**
 * Cell 原生值可以改
*/
#[allow(dead_code)]
struct Book {
    name: String,
    price: Cell<u32>,
}
pub fn run() {
    let rust_book = Book {
        name: "rust-book".into(),
        price: Cell::new(99),
    };
    assert_eq!(rust_book.name, "rust-book");
    assert_eq!(rust_book.price.get(), 99);
    rust_book.price.set(199); //Cell 原生值可以改
    assert_eq!(rust_book.price.get(), 199);

    let s: String = "rust-book".into();
    let bar = Cell::new(s);
    bar.set("15".into()); //可以改值
    let x = bar.into_inner(); //Get String value from Cell
    println!("{}", x);
}
```

## RefCell in rust

```rust
#[allow(unused_variables)]
use std::cell::RefCell;
/**
 * RefCell 原生值可以改
*/
#[allow(dead_code)]
struct Book {
    name: String,
    price: RefCell<u32>,
}
pub fn run() {
    let mut rust_book = Book {
        name: "rust-book".into(),
        price: RefCell::new(99),
    };
    assert_eq!(rust_book.name, "rust-book");
    rust_book.price.borrow_mut(); //RefCell 原生值可以改
    println!("{:?}", rust_book.price.borrow()); //99
    println!("{:?}", rust_book.price.as_ptr()); //指针地址 0x7ffcb13f2c40
    println!("{:?}", *rust_book.price.get_mut() + 10); //99+10 =>109

    let s: String = "rust-book".into();
    let bar = RefCell::new(s);
    bar.borrow_mut().push_str(" 15"); //可以改值 为rust-book 15
    let x = bar.into_inner(); //Get String value from refCell
    println!("{}", x);
}
```

## generic in rust

```rust
#[allow(dead_code)]
// structF32 Point{
//     x:i32,
//     y:i32,
// }
// structF64 Point{
//     x:i32,
//     y:i32,
// }  //为了 通用不同的type 可以用以下的操作

//struct can be generic
struct Point<T, U> {
    x: T,
    y: U, //要是x y 的type不一样 <T,U>
}
// enum canbe generic
enum Selection<T> {
    // OptionA(T),
    OptionB(T),
    // OptionC,
}
//function can be generic
// std::ops::Add is a trait
// fn dog<T:std::ops::Add<Output=T> + std::ops::Sub<Output=T> + std::fmt::Debug>(dog_age:T,father_age:T,child_age:E) -> T{
//    println!("{:?}",father_age);
//    let sub = dog_age-father_age;
// //    let add = dog_age+father_age;
//    sub
// } //这样写代码太长 下面做一些改善
fn dog<T, E>(dog_age: T, father_age: T, child_age: E) -> T
where
    T: std::ops::Add<Output = T> + std::ops::Sub<Output = T> + std::fmt::Debug,
    E: std::fmt::Debug,
{
    println!("{:?}", father_age);
    println!("{:?}", child_age);
    dog_age + father_age
}

// create owen trait
// add str to string
trait AddStr {
    fn add(&self, a: &str, b: &str) -> String;
}
#[allow(non_snake_case)]
#[allow(dead_code)]
// use trait
fn add_str_to_String<T>(var: &T) -> String
where
    T: AddStr + std::fmt::Debug,
{
    println!("{:?}", var);
    var.add("Alen", "Andry")
}

// sttuct can be generic
struct Person<T, U>
where
    T: std::fmt::Debug,
    U: std::fmt::Debug,
{
    name_t: T,
    age_u: U,
}

impl<T, U> Person<T, U>
where
    T: std::fmt::Debug,
    U: std::fmt::Debug,
{
    fn log(&self) {
        println!("{:?} {:?}", self.name_t, self.age_u);
    }
}

pub fn run() {
    // generic struct
    let a = Point {
        x: 10_f32,
        y: 30_i32,
    }; //f32
    println!("{} {}", a.x, a.y);
    let a = Point {
        x: 10.10_f32,
        y: 30.6_f64,
    }; //f64
    println!("{} {}", a.x, a.y);

    // generic enum

    let s = Selection::OptionB("sting");

    match s {
        // Selection::OptionA(e)=> println!("{}",e),
        Selection::OptionB(f) => println!("{}", f),
        // Selection::OptionC => println!("option c"),
    }

    // generic function
    let f = dog(10, 20, 5);
    println!("{:?}", f);

    // add_str_to_String

    // use  struct generic
    let alen = Person {
        name_t: "23",
        age_u: "11",
    };
    alen.log();
}
```

## LinkedList (链表)

```rust
use std::collections::LinkedList;

// 链表
pub fn run() {
    let mut list = LinkedList::new();
    list.push_front("1");
    list.push_front("2");
    list.push_front("3");
    list.push_back("10");
    list.push_back("20");
    list.push_back("30");
    println!("{:?}", list);

    // change list item type Sting ti int
    let mut str_to_int = LinkedList::new();
    for item in list.iter() {
        str_to_int.push_back(item.parse::<i32>().unwrap());
    }
    println!("to int:{:?}", str_to_int);

    let mut new_list = LinkedList::new();
    new_list.push_front(1);
    new_list.push_front(2);
    new_list.push_front(3);
    new_list.push_back(10);
    new_list.push_back(20);
    new_list.push_back(30);
    println!("{:?}", new_list);

    //change new_list type int to String
    let mut int_to_string = LinkedList::new();
    for item in new_list.iter() {
        int_to_string.push_back(item.to_string());
    }

    println!("to str:{:?}", int_to_string);

    // append Moves all elements from list2 to the end of the list.
    // list.append(list2)  list2 become empty

    // convert a &str to a String is to_owned
    // list 中的元素是&str int_to_string 是String 所以会出错
    let mut list_sting = LinkedList::new();
    for item in list.iter_mut() {
        let new_item: String = item.to_owned(); //&str converto string
        list_sting.push_back(new_item);
    }
    list_sting.append(&mut int_to_string); //int_to_string to the end of list_sting
    println!("{:?}", list_sting);

    // pub fn back(&self) -> Option<&T>
    // assert_eq!(list_sting.back(),Some(&Sting::from("30")));
}
```

## module in rust

```rust
// 可以直接定义mod
mod printer{
    pub fn print(data:String){
        println!("{}",data);
    }
    // 也可以在mod 里面定义mod
    pub mod show{
        pub fn show_age(age:&str){
            println!("age :{}",age);
        }
    }
}


pub fn run(){

    printer::print("Alen".to_string());
    printer::show::show_age("24");

}
```

## options in rust

```rust
pub fn run() {
    println!(
        "job is {}",
        match get_job("Alen") {
            Some(j) => j,
            None => "no find",
        }
    );
}
fn get_job(name: &str) -> Option<&str> {
    match name {
        "Alen" => Some("Software developer"),
        "Andry" => Some("Web Disigner"),
        _ => None,
    }
}
```

## parse json in rust

```rust
extern crate serde;
extern crate serde_json;
// #[macro_use]
// extern crate serde_derive;
#[allow(unused_imports)]
use serde_json::Value as jsonvalue;

// #[derive(Serialize,Deserialize)]
#[allow(dead_code)]
// struct Person {
//     name: String,
//     age: u32,
//     is_male: bool,
//     language: String,
// }

pub fn run() {
    let json_string = r#"
        {
            "name":"Alen Andry",
            "age":"24",
            "is_male":true,
            "language":"English"
        }
        "#;
    let res = serde_json::from_str(json_string);
    if res.is_ok() {
        let p: jsonvalue = res.unwrap();
        println!("name = {:?}", &p["name"].as_str().unwrap());
        println!("age = {:?}", &p["age"].as_str().unwrap());
        println!("is_male = {:?}", &p["is_male"]);
        println!("language = {:?}", &p["language"]);
    } else {
        println!("not get json");
    }
}
```

## generate random number in rust

```rust
extern crate rand;
use rand::Rng;
pub fn run() {
    {
        //range random num
        let random_num = rand::thread_rng().gen_range(10, 25); //1-24
        println!("{}", random_num);
    }
    {
        //randim boolean value
        let bool = rand::thread_rng().gen_weighted_bool(2); //概率0.5 为true
        let bool1 = rand::thread_rng().gen_weighted_bool(5); //概率1/5=0.2 为true
        println!("random boolean {} {}", bool, bool1);
    }
}
```

## read file in rust

```rust
use std::fs::File;
use std::io::prelude::*;
#[allow(unused_imports)]
use std::io::{BufRead, BufReader, Error, Write};
#[allow(dead_code)]
pub fn run() {
    {
        //read toml file
        let mut toml_file = File::open("toml_file.toml").expect("Can't open");
        let mut content = String::new();
        toml_file
            .read_to_string(&mut content)
            .expect("Can't to string");

        println!("toml file content:{}", content);
    }

    {
        //read txt file
        let mut txt_file =
            File::open("/home/alen/code/rust_code/rust_grammar/txt_file.txt").expect("Can't open");
        let mut content = String::new();
        txt_file
            .read_to_string(&mut content)
            .expect("Can't to string");

        println!("txt file content:{}", content);
    }


}
```

## write file in rust

```rust
use std::fs::File;
use std::io::prelude::*;

pub fn run() {
    {
        //write toml
        let mut toml_file = File::create("output.toml").expect("can't create file");
        toml_file
            .write_all(b"[output]\ndata = \"output.toml\"")
            .expect("can't write");
    }
    {
        //write txt
        let mut txt_file = File::create("output.txt").expect("can't create file");
        txt_file
            .write_all(b"txt file\ndata = \"output.txt\"")
            .expect("can't write");
    }
}
```

## regex in rust

```rust
extern crate regex;
use regex::Regex;
```

```rust
pub fn run() {

    {//captures
    let re = Regex::new(r"(?x)(?P<year>\d{4})-(?P<month>\d{2})-(?P<day>\d{2})").unwrap();
    let caps = re.captures("2010-03-1400").unwrap();

    dbg!(&caps[0]);
    dbg!(&caps["year"]);
    }

     {//captures_iter 可遍历
        let re = Regex::new(r"(?x)(?P<year>\d{4})-(?P<month>\d{2})-(?P<day>\d{2})").unwrap();
        let caps = re.captures_iter("2010-03-1400");

        for  i in caps {
            dbg!(&i);
        }
    }

    {
      let re = Regex::new(r"(\d{5})").unwrap(); //match 5个数
      let txt = "12345";
      println!("{}", re.is_match(txt));
      match re.captures(txt) {
          Some(val) => println!("{}", &val[0]),
          None => println!("none"),
          }
	  }

     {//str to vec! split str to Vec
        let re = Regex::new(r"[ \t]+").unwrap();
        let fields: Vec<&str> = re.split("a b \t  c\td    e").collect();
        dbg!(&fields);
        assert_eq!(fields, vec!["a", "b", "c", "d", "e"]);

    }

     {//is match 返回 true flase
       let text = "I categorically deny having";
       dbg!(Regex::new(r"\b\w{4}\b").unwrap().is_match(text)); //regex 匹配四个字母 存在的话返回true
        assert!(Regex::new(r"\b\w{4}\b").unwrap().is_match(text));
    }

    {//find
        let text = "I alen categorically deny having triskaidekaphobia.";
        let mat = Regex::new(r"\b\w{4}\b").unwrap().find(text).unwrap(); //从左开始匹配 返回满足条件的开始 结束index
        dbg!(mat);

    }

      {//NoExpand
        use regex::NoExpand;

        let re = Regex::new(r"(?P<last>[^,\s]+),\s+(\S+)").unwrap();
        let result = re.replace("^Springsteen, Bruce", NoExpand("$2 $last"));
        dbg!(result);
    }

    {//返回first match 的位置
        let text = "aaaaa";
        let pos = Regex::new(r"a+").unwrap().shortest_match(text);
        dbg!(pos.unwrap());
    }





}
```

## 字符串反转 reverse string

```rust
  fn reverse(phrase:&str)-> String {
        let mut i = phrase.len();
        let mut reversed = String::new();
        while i > 0 {
            reversed.push(phrase.chars().nth(i - 1).unwrap());
            i -= 1;
        }
        reversed

    }
```

## 等待执行 函数

```rust
use std::thread;
use std::time::{Duration, Instant};

fn expensive_function() {
    //一秒后执行的函数
    thread::sleep(Duration::from_secs(1));
}

pub fn run() {
    let start = Instant::now(); //开始计时
    expensive_function();
    expensive_function();
    expensive_function();
    expensive_function();
    expensive_function();
    let duration = start.elapsed(); //停止计时

    println!("Time elapsed in expensive_function() is: {:?}", duration); //run expensive_function() 经历的时间
}
```

## String in rust

```rust
#[allow(unused_variables)]

pub fn run() {
    // str 不可变
    let str: &str = "Hello";
    println!("{}", str);
    // string 可变
    let string = String::from("Hello world");
    println!("{}", string);

    // convert &srt to String    &str转化为string
    let some_str: &str = "data";
    let sring_from_str = some_str.to_owned();
    assert_eq!(sring_from_str, String::from("data"));

    {
        // string to &str
        let name = String::from("Alen Andry");
        let name_str: &str = name.as_str();
        println!("&str:{}", name_str);
    }

    let i = 5;
    let five = String::from("5");
    assert_eq!(five, i.to_string());

    let mut name = String::from("Alen ");
    //添加char
    name.push('A');
    //添加string
    name.push_str("ndry");
    //长度
    let length = name.len();
    //所占字节
    let capacity = name.capacity();
    // 字符串是否空
    let is_empty = name.is_empty();
    //是否包含子串
    let contains = name.contains("Andry");
    //交换子串
    let change = name.replace("Andry", "Dnrops"); // Andry->Dnrops
    println!("name:{:?}\nlength:{:?}", (name), (length));
    println!("capacity:{:?}\nis_empy:{:?}", (capacity), (is_empty));
    println!("Is Andry contains  name:{:?}", (contains));
    println!("{}", change);

    //遍历string (按空格)
    for word in name.split_whitespace() {
        println!("{}", word);
    }
    // 按字节新建string
    let mut s = String::with_capacity(10); //新建大小为10字节的string
    s.push('a'); //在string里添加元素
    s.push('B');
    println!("{}", s);

    //断言测试 (测试左右值是否相等)
    //assert_eq!(1,2);
    //只有不相等时提示错误
    assert_eq!(2, s.len());
    assert_eq!(10, s.capacity());

    // push
    let mut some_string = String::new();
    some_string.push('a');
    some_string.push('a');
    some_string.push('a');
    some_string.push('a');
    // push_str
    some_string.push_str("\tmy name is alen");

    println!("{}", some_string);

    //combine two string
    let new_some_string = String::from(" mali");
    let mut_string = String::from(" Andry");
    let my_mali: String = String::from("I LOVE MICHELLE");
    let combined_string = some_string + &new_some_string + &mut_string + &my_mali;
    println!("{}", combined_string);

    // substring
    let sub_string = &combined_string[..5]; //0-4
    let sub_string1 = &combined_string[16..]; //16-end
    let sub_string2 = &combined_string[16..20]; //16-20
    println!("{}\n{}\n{}", sub_string, sub_string1, sub_string2);

    // get char by index
    let mali: String = String::from("I LOVE MICHELLE");
    let get_char_index2 = &mali.chars().nth(2).unwrap();
    println!("{}", get_char_index2);

    // for 遍历 String
    for item in 0..mali.len() {
        println!("{}", &mali.chars().nth(item).unwrap());
    }

    // match Sting
    let get_char_index3 = &mali.chars().nth(5);
    match get_char_index3 {
        Some(i) => println!("It is {}", i),
        None => {}
    }
    // if let  跟 match 一样
    if let Some(i) = &mali.chars().nth(5) {
        println!("It is {}", i);
    }
    //删除俩端的空格
    {
        let name = "  Alen  ".to_string();
        println!("before :{}", name);
        let after = name.trim();
        println!("after:{}", after);
    }

    {
        //转化为大写
        let mut s = String::from("foobar");
        let s_mut_str = s.as_mut_str();

        s_mut_str.make_ascii_uppercase();

        println!("uppercase :{}", s_mut_str);
    }

    {
        //转化为ascii码
        let s = String::from("hello");
        let s_ascii_str: &[u8] = s.as_bytes();
        println!("ascii:{:?}", s_ascii_str);
    }

    {
        //string 反转化

        let mut s = String::from("hello");
        unsafe {
            let vec = s.as_mut_vec();
            assert_eq!(&[104, 101, 108, 108, 111][..], &vec[..]);

            vec.reverse();
        }
        assert_eq!(s, "olleh");
        println!("reversed:{}", s);
    }

    {
        //清空string
        let mut s = String::from("foo");

        s.clear();
        assert!(s.is_empty());
        assert_eq!(0, s.len());
        assert_eq!(3, s.capacity());
    }
}
```

## struct 结构体

```rust
//结构体(name field struct)
// struct name 第一个字母必须得大写
struct Book {
    name: String,
    athur: String,
}

//tuple struct  (元组结构体)
struct Cellphone(&'static str, String, u64);

//单元结构体
struct Empty;

//结构体创建函数
struct Person {
    f_name: String,
    l_name: String,
}

//结构体创建函数
impl Person {
    //
    fn new_str(m: &str, n: &str) -> Person {
        // return Person{name:f_name,lname:l_name};
        Person {
            f_name: m.to_string(),
            l_name: n.to_string(),
        }
    }

    //full name  // 使用在impl里面
    fn full_name(&self) -> String {
        format!("{}  {}", self.f_name, self.l_name)
    }

    //set last name
    fn set_last_name(&mut self, last: &str) {
        self.l_name = last.to_string();
    }
    //name to tuple(转化为元组)
    fn to_tuple(self) -> (String, String) {
        (self.f_name, self.l_name)
    }
}

// define some struct
struct FrameworkAndCompany {
    msn: String,
    pytorch: String,
    tensorflow: String,
}

pub fn run() {
    //调用(name field struct)
    let mut c = Book {
        name: "RUST".to_string(),
        athur: String::from("Alen"),
    };
    c.athur = String::from("Andry");
    println!("{}  {}", c.name, c.athur);

    //调用(tuple struct)
    let mut phone = Cellphone("redmi", String::from("alen"), 2019);

    phone.1 = String::from("Alen");
    println!("marka is {}  owener: {} year:{}", phone.0, phone.1, phone.2);

    //调用单元结构体
    let x = Empty;
    println!("{:p}", &x); //输出X的内存地址

    //调用结构体创建函数
    let mut p = Person::new_str("marry", "tusun");
    println!("{}  {}", p.f_name, p.l_name);
    println!("full name: {}", p.full_name());
    p.set_last_name("abduginy");
    println!("full name: {}", p.full_name());
    println!("full name to tuple: {:?}", p.to_tuple());

    // use framework struct
    let mut frames = FrameworkAndCompany {
        tensorflow: "google".to_owned(),
        msn: "MSN".to_owned(),
        pytorch: "facebook".to_owned(),
    };
    //change name
    frames.tensorflow = String::from("GOOGLE");

    println!(" {:?}", frames.tensorflow);
    println!(" {:?}", frames.msn);
    println!(" {:?}", frames.pytorch);

    let frames2 = FrameworkAndCompany {
        msn: String::from("Dark Commany"),
        ..frames // 来填充剩下的 struct element
    };
    println!("{:?}", frames2.pytorch);
}
```

## Test code in rust

```rust
//结构体(name field struct)
// struct name 第一个字母必须得大写
struct Book {
    name: String,
    athur: String,
}

//tuple struct  (元组结构体)
struct Cellphone(&'static str, String, u64);

//单元结构体
struct Empty;

//结构体创建函数
struct Person {
    f_name: String,
    l_name: String,
}

//结构体创建函数
impl Person {
    //
    fn new_str(m: &str, n: &str) -> Person {
        // return Person{name:f_name,lname:l_name};
        Person {
            f_name: m.to_string(),
            l_name: n.to_string(),
        }
    }

    //full name  // 使用在impl里面
    fn full_name(&self) -> String {
        format!("{}  {}", self.f_name, self.l_name)
    }

    //set last name
    fn set_last_name(&mut self, last: &str) {
        self.l_name = last.to_string();
    }
    //name to tuple(转化为元组)
    fn to_tuple(self) -> (String, String) {
        (self.f_name, self.l_name)
    }
}

// define some struct
struct FrameworkAndCompany {
    msn: String,
    pytorch: String,
    tensorflow: String,
}

pub fn run() {
    //调用(name field struct)
    let mut c = Book {
        name: "RUST".to_string(),
        athur: String::from("Alen"),
    };
    c.athur = String::from("Andry");
    println!("{}  {}", c.name, c.athur);

    //调用(tuple struct)
    let mut phone = Cellphone("redmi", String::from("alen"), 2019);

    phone.1 = String::from("Alen");
    println!("marka is {}  owener: {} year:{}", phone.0, phone.1, phone.2);

    //调用单元结构体
    let x = Empty;
    println!("{:p}", &x); //输出X的内存地址

    //调用结构体创建函数
    let mut p = Person::new_str("marry", "tusun");
    println!("{}  {}", p.f_name, p.l_name);
    println!("full name: {}", p.full_name());
    p.set_last_name("abduginy");
    println!("full name: {}", p.full_name());
    println!("full name to tuple: {:?}", p.to_tuple());

    // use framework struct
    let mut frames = FrameworkAndCompany {
        tensorflow: "google".to_owned(),
        msn: "MSN".to_owned(),
        pytorch: "facebook".to_owned(),
    };
    //change name
    frames.tensorflow = String::from("GOOGLE");

    println!(" {:?}", frames.tensorflow);
    println!(" {:?}", frames.msn);
    println!(" {:?}", frames.pytorch);

    let frames2 = FrameworkAndCompany {
        msn: String::from("Dark Commany"),
        ..frames // 来填充剩下的 struct element
    };
    println!("{:?}", frames2.pytorch);
}
```

## 数组中找到最小的

```rust
pub fn find_smallest_int(arr: &[i32]) -> i32 {
    let mut arr_vec = arr.to_vec();  //to_vec 是 arr转化为 vec
    arr_vec.sort();
    println!("{}", arr_vec[0]);
    arr_vec[0]
}
```

## fib in rust

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

## rust 数组中删除重复的部分

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

## enumerate (遍历)

```rust
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
        let mut items = Vec::new();
        let mut indexs = Vec::new();
        for (index, item) in s.iter().enumerate() {
            items.push(item.to_string());
            indexs.push(index.to_string());
            // println!(
            //     "{} {}",
            //     s.len() as i32 - index.to_owned() as i32,
            //     item.to_owned()
            // );
        }
        //if s = 145
        println!("{:?}", indexs); //["0", "1", "2"]
        println!("{:?}", items); //["1", "4", "5"]
    }
}

fn main() {
    c::run();
}
```

## quick start iter fold()

```rust
let a = [1, 2, 3];
// the sum of all of the elements of the array
let sum = a.iter().fold((0,0), |init, x|
{
    let n = init.0+*x;
    let m = init.1+*x;
    (n,m)
}
);
eprintln!("{:?}",sum);
```

## Select Mul (Atcoder_abc_221_C)

```rust
Sample Input 1
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
```

```rust
//solution for problem C
/*
input: 123
out: 63
{"1": "23", "12": "3", "3": "21", "31": "2", "32": "1"}
[23, 32, 36, 62, 63] ->out max value
*/

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

fn main() {
    c::run();
}
```

## Online games (Atcoder_abc_221_D)

```rust
//solution for problem D
// 3
// 1 2
// 2 3
// 3 1
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
        let mut d = vec![0; n + 1];
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
fn main() {
    d::run();
}
```
