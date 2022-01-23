# encryption data  加密数据

```rust
#[allow(unused)]
pub mod encryption_string {
    use std::collections::BTreeSet;
    pub fn run() {
        let encode: Vec<(char, usize, usize, &str)> = Vec::from([
            ('a', 97, 1, "["),
            ('b', 98, 2, ")"),
            ('c', 99, 3, "{"),
            ('d', 100, 4, "^"),
            ('e', 101, 5, "*"),
            ('f', 102, 6, "("),
            ('g', 103, 7, "]"),
            ('h', 104, 8, "`"),
            ('i', 105, 9, "_"),
            ('j', 106, 10, "!"),
            ('k', 107, 11, "%"),
            ('l', 108, 12, "&"),
            ('m', 109, 13, "+"),
            ('n', 110, 14, "#"),
            ('o', 111, 15, "$"),
            ('p', 112, 16, "<"),
            ('q', 113, 17, "}"),
            ('r', 114, 18, "~"),
            ('s', 115, 19, "@"),
            ('t', 116, 20, "?"),
            ('u', 117, 21, "|"),
            ('v', 118, 22, "."),
            ('w', 119, 23, "-"),
            ('x', 120, 24, ":"),
            ('y', 121, 25, "/"),
            ('z', 122, 26, ">"),
            (',', 44, 44, "="),
            (' ', 32, 32, " "),
            ('0', 48, 48, "0"),
            ('1', 49, 49, "1"),
            ('2', 50, 50, "2"),
            ('3', 51, 51, "3"),
            ('4', 52, 52, "4"),
            ('5', 53, 53, "5"),
            ('6', 54, 54, "6"),
            ('7', 55, 55, "7"),
            ('8', 56, 45, "8"),
            ('9', 57, 42, "9"),
            ('*', 42, 42, "a"),
            ('/', 47, 47, "h"),
            ('+', 43, 43, "e"),
            ('-', 45, 45, "s"),
        ]);
        let sentense = "Alen Andey";
        fn get_acsii_vec(ref s: &str) -> Vec<u8> {
            let mut v = s.to_string().into_bytes();
            let mut v1 = vec![];
            for item in v.iter_mut() {
                v1.push(item.to_ascii_lowercase());
            }
            v1
        }

        let ass = get_acsii_vec(sentense);
        println!("{}", &sentense);
        println!("{:?}", &ass);
        let mut re = String::new();
        fn get_en_char(vec: &Vec<(char, usize, usize, &str)>, ch: u8) -> String {
            let mut re = String::new();
            for i in vec.iter() {
                if i.1 == ch as usize {
                    re = i.3.to_string();
                    break;
                } else {
                    re = (ch as char).to_string();
                }
            }
            return re;
        }
        for i in ass.iter() {
            re.push_str(&get_en_char(&encode, *i));
        }
        println!("{:?}", &re);
        let encode1 = encode.clone();
        fn get_decode_char(ch: &str, encode: Vec<(char, usize, usize, &str)>) -> String {
            let mut re = String::new();
            for (index, item) in encode.iter().enumerate() {
                if ch == item.3 {
                    re = item.0.to_string();
                }
            }
            re
        }
        fn decode_s(s: String, encode1: Vec<(char, usize, usize, &str)>) -> String {
            let mut re = String::new();
            for item in s.split("").filter(|s| !s.is_empty()).collect::<Vec<&str>>() {
                re.push_str(&get_decode_char(item, encode1.clone()));
            }
            re
        }
        let re1 = decode_s(re, encode1);
        println!("{:?}", &re1);
    }
}
```
