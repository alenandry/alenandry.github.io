## vec 删除重复的元素,返回 Unique Vec

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

## 