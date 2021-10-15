# Algorithm Solution



## String 中部分字母替换成大写

```js
let inputArray = "Who Love Solo OOO".split(" ");
let lower = ["a", "e", "i", "o", "u"]; //替换这些字母为大写
function doFunc(arr) {
  let new_arr = [];
  let new_arr_join = arr.join().toLowerCase().split("");
  // console.log(new_arr_join);
  for (let i = 0; i < new_arr_join.length; i++) {
    if (lower.includes(new_arr_join[i])) {
      new_arr.push(new_arr_join[i].toUpperCase());
    } else {
      new_arr.push(new_arr_join[i]);
    }
  }
  console.log(new_arr.join("").replace(/,/g, " "));
}

doFunc(inputArray); //whO lOvE sOlO OOO
```

## 用 String 加很大的书树

```js
let sum_string = function (num1, num2) {
  let i = num1.length - 1,
    j = num2.length - 1,
    add = 0;
  const ans = [];
  while (i >= 0 || j >= 0 || add != 0) {
    let a = 0,
      b = 0;
    if (i >= 0) {
      a = num1.charAt(i) - "0";
    } else {
      a = 0;
    }
    if (j >= 0) {
      b = num2.charAt(j) - "0";
    } else {
      b = 0;
    }
    let re = a + b + add;
    ans.push(re % 10);
    add = Math.floor(re / 10);
    i -= 1;
    j -= 1;
  }
  return ans.reverse().join("");
};

let a = "99999999999999999999999999999999999999999999999999999999999";
let b = "999999999999999999999999999999999999999999999999999999999";

let result = sum_string(a, b);

console.log(result);
```

## 数组反转

```js
const reverse = (arr) => {
  return arr.reverse().join("");
};
```

## 对 string 全排列 并删除 相同（重复）元素，输出最终不同的全排列个数

```js
let inputArray = "ABCDEFGHHA".split("");
//删除数组中相同（重复）的元素
function remove(arr) {
  return Array.from(new Set(arr));
}
//全排列
function permutate(str) {
  var result = [];
  if (str.length == 1) {
    return [str];
  } else {
    var preResult = permutate(str.slice(1));
    for (var j = 0; j < preResult.length; j++) {
      for (var k = 0; k < preResult[j].length + 1; k++) {
        var temp = preResult[j].slice(0, k) + str[0] + preResult[j].slice(k);
        result.push(temp);
      }
    }
    return result;
  }
}
//n！ jiecheng
function n_(x) {
  if (x < 2) {
    return 1;
  } else {
    return x * n_(x - 1);
  }
}

function doFunc(arr) {
  let join_arr = arr.join("");
  console.log(remove(permutate(join_arr)).length);
}

doFunc(inputArray);

// ABA,AAB,BAA
```

## 数组小到大排序

```js
function(arr){
    return arr = arr.sort((a, b) => a[0] - b[0]);
}
```

## 输出数的因子乘积等于该数的 数组

```js
const readline = require("readline");

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});

rl.question("", function (line) {
  let number = parseInt(line);
  factor(number);
  rl.close();
});

function factor(num) {
  let result = "";
  for (let i = 2; i * i <= num && i <= num; i++) {
    while (num % i === 0) {
      result += i + " ";
      num /= i;
    }
  }
  if (num > 1) result += num + " ";

  console.log(result);
}
```

## 给定一个数组和一个目标和，从数组中找两个数字相加等于目标和，输出这两个数字的下标。

```js
function twoSum(nums, target) {
  let ans = [];
  for (let i = 0; i < nums.length; i++) {
    for (let j = i + 1; j < nums.length; j++) {
      if (nums[i] + nums[j] == target) {
        ans[0] = [i, nums[i]];
        ans[1] = [j, nums[j]];
        return ans;
      }
    }
  }
  return ans;
}

let nums = [0, 0, 0, 5, 6, 7, 8];

let target = 9;

console.log(twoSum(nums, target));
```

## 插入排序

```js
//小到大
function insertionSort(arr) {
  var len = arr.length;
  var preIndex, current;
  for (var i = 1; i < len; i++) {
    preIndex = i - 1;
    current = arr[i];
    while (preIndex >= 0 && arr[preIndex] > current) {
      arr[preIndex + 1] = arr[preIndex];
      preIndex--;
    }
    arr[preIndex + 1] = current;
  }
  return arr;
}

let nums = [0, 20, 0, 5, 6, 7, 8];
console.log(insertionSort(nums));
```

## 选择排序

```js
function selectionSort(arr) {
  var len = arr.length;
  var minIndex, temp;
  for (var i = 0; i < len - 1; i++) {
    minIndex = i;
    for (var j = i + 1; j < len; j++) {
      if (arr[j] < arr[minIndex]) {
        // 寻找最小的数
        minIndex = j; // 将最小数的索引保存
      }
    }
    temp = arr[i];
    arr[i] = arr[minIndex];
    arr[minIndex] = temp;
  }
  return arr;
}
```

## 进制转换

```js
// 如果要处理2进制到10进制，16进制到10进制，8进制到10进制， 需要用了paresInt这个方法

//2进制到10进制；
parseInt(10, 2); //=>2
//2进制到10进制；
parseInt(100, 2); //=>4
//16进制到10进制
parseInt(12, 16); //=>18
//8进制到10进制
parseInt(12, 8); //=>10

//js的进制转换， 分为2进制，8进制，10进制，16进制之间的相互转换， 我们直接利用 对象.toString()即可实现：
//10进制转为16进制
(10)
  .toString(16)(
    // =>"a"
    //8进制转为16进制
    012
  )
  .toString(16)(
    // =>"a"
    //16进制转为10进制
    0x16
  )
  .toString(10)(
    // =>"22"
    //16进制转为8进制
    0x16
  )
  .toString(8)(
    // =>"26"
    //10进制转为2进制 //=>
    1111
  )
  .toString(2)(
    // => "10001010111"
    //8进制转为2进制 //=>
    01111
  )
  .toString(2)(
    //=>"1001001001"
    //16进制转为2进制 //=>
    0x16
  )
  .toString(2); // => "10110"
```

## 删除数组中相同（重复）的元素

```js
const arr = [5, 1, 5, 7, 7, 5];
const unique = [...new Set(arr)]; // [ 5, 1, 7 ]
```

## js 中能改变值的二进制数组

```js
// Element type	Bytes	Description	C type
// Int8	   1	8-bit signed integer	signed char
// Uint8	1	8-bit unsigned integer	unsigned char
// Uint8C	1	8-bit unsigned integer (clamped conversion)	unsigned char
// Int16	2	16-bit signed integer	short
// Uint16	2	16-bit unsigned integer	unsigned short
// Int32	4	32-bit signed integer	int
// Uint32	4	32-bit unsigned integer	unsigned int
// Float32	4	32-bit floating point	float
// Float64	8	64-bit floating point	double

const typedArray = new Float64Array([0, 1, 2]); //64位 8byte
console.log(typedArray.length); // 3
typedArray[0] = 5;
const normalArray = [...typedArray]; // [5,1,2]

// The elements are stored in typedArray.buffer.
// Get a different view on the same data:
const dataView = new DataView(typedArray.buffer);
console.log(dataView.getUint8(0)); // 5
```

## 按照从右向左的阅读顺序，返回一个不含重复数字的新的整数

### HJ9 提取不重复的整数

```js
let line = "2752771".split("").reverse().join("").split("");
while ((line = readline())) {
  var lines = line.split("").reverse().join("").split("");
  function remove(arr) {
    return [...new Set(arr)];
  }
  print(remove(lines).join(""));
}
```

## 字符转化为按 ascii 码(ASCII 码)

```js
let str = "a".charCodeAt();
console.log(str); //97
```

## HJ10 字符个数统计

### 对于字符串 abaca 而言，有 a、b、c 三种不同的字符，因此输出 3。

### 输出 输入字符串 中范围在(0~127，包括 0 和 127)字符的种数。

```js
while ((line = readline())) {
  var lines = line.split("");
  let count = 0;
  function remove(arr) {
    return [...new Set(arr)];
  }
  lines = remove(lines);
  for (let i = 0; i < lines.length; i++) {
    if (lines[i].charCodeAt() >= 0 && lines[i].charCodeAt() <= 127) {
      // console.log(lines[i]);
      count++;
    }
  }
  print(count);
  // console.log(count);
}
```

## 数字颠倒

```js
while ((line = readline())) {
  var lines = line.split("");
  console.log(lines.reverse().join(""));

  // print();
}
```

## HJ12 字符串反转

### node.js 实现

```js
const readline = require("readline");

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});
rl.on("line", function (line) {
  const tokens = line.split("");
  console.log(tokens.reverse().join(""));
});

const reverse = (arr) => {
  return arr.reverse().join("");
};
```

## HJ13 句子逆序

输入一个英文语句，每个单词用空格隔开。保证输入只包含空格和字母。

输出描述：
得到逆序的句子

```js
const readline = require("readline");

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});
rl.on("line", function (line) {
  const tokens = line.split(" ");
  console.log(tokens.reverse().join(" "));
});

const reverse = (arr) => {
  return arr.reverse().join("");
};
```

## HJ14 字符串排序

```js
const readline = require("readline");

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});
let i = 0;
var long = 0;
rl.question("", function (line) {
  long = parseInt(line);
});
var arr = [];
rl.on("line", function (line) {
  i += 1; //每输入完一行i++
  arr.push(line);
  if (i == long) {
    //等于第一行的输入值的时候停止输入
    for (var j = 0; j < arr.length; j++) {
      console.log(sort_arr(arr)[j]);
    }
    rl.close();
  }
});
const sort_arr = (arr) => {
  return arr.sort(); //按字母排序
};
```

## HJ15 求 int 型正整数在内存中存储时 1 的个数

```js
//node.js 
const readline = require("readline");

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});
let i;
rl.question("", (line) => {
  i = parseInt(line).toString(2); //转化为2进制
  let count = 0;
  i.toString()
    .split("")
    .forEach((e) => {
      if (e === "1") {
        count += 1;
      }
    });
  console.log(count);
  rl.close();
});

//rust
fn main() {
    println!("{}",count4(300));
    println!("");
}
fn count4(mut n:i32) -> i32 {
    n = (n & 0x55555555) +((n>>1)&0x55555555);
    n = (n & 0x33333333) +((n>>2)&0x33333333);
    n = (n & 0x0f0f0f0f) +((n>>4)&0x0f0f0f0f);
    n = (n & 0x00ff00ff) +((n>>8)&0x00ff00ff);
    n = (n & 0x0000ffff) +((n>>16)&0x0000ffff);
    return n
}
```



## 合并两个有序链表

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    ListNode h = new ListNode(0);
    ListNode ans=h;
    while (l1 != null && l2 != null) {
        if (l1.val < l2.val) {
            h.next = l1;
            h = h.next;
            l1 = l1.next;
        } else {
            h.next = l2;
            h = h.next;
            l2 = l2.next;
        }
    }
    if(l1==null){
        h.next=l2;
    }
    if(l2==null){
        h.next=l1;
    }
    return ans.next;
}
}
```

## 数组中删除 element

```java
public int removeElement(int[] nums, int val) {
    int i = 0;
    int n = nums.length;
    while (i < n) {
        if (nums[i] == val) {
            nums[i] = nums[n - 1];
            n--;
        } else {
            i++;
        }
    }
    return n;
}
```

## List 全排列

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
    List<List<Integer>> all = new ArrayList<>();
    //从下标 0 开始的所有组合
    upset(nums, 0, all);
    return all;
}
private void upset(int[] nums, int begin, List<List<Integer>> all) {
    if (begin == nums.length) {
        ArrayList<Integer> temp = new ArrayList<Integer>();
        for (int i = 0; i < nums.length; i++) {
            temp.add(nums[i]);
        }
        all.add(new ArrayList<Integer>(temp));
        return;
    }
    for (int i = begin; i < nums.length; i++) {
        swap(nums, i, begin);
        upset(nums, begin + 1, all);
        swap(nums, i, begin);
    }
}
private void swap(int[] nums, int i, int begin) {
    int temp = nums[i];
    nums[i] = nums[begin];
    nums[begin] = temp;
}
}
```

## 给两个有序数组，把第二个数组合并到第一个数组中，保持有序。

```java
class Solution {
   public void merge(int[] nums1, int m, int[] nums2, int n) {
    int i = m - 1; //从末尾开始
    int j = n - 1; //从末尾开始
    int k = m + n - 1; //从末尾开始
    while (j >= 0) {
        if (i < 0) {
            while (j >= 0) {
                nums1[k--] = nums2[j--];
            }
            return;
        }
        //哪个数大就对应的添加哪个数。
        if (nums1[i] > nums2[j]) {
            nums1[k--] = nums1[i--];
        } else {
            nums1[k--] = nums2[j--];
        }
    }
}
}
```

## 判断是否有重复数字。

```java
public boolean containsDuplicate(int[] nums) {
    HashSet<Integer> set = new HashSet<>();
    for (int i = 0; i < nums.length; i++) {
        if (set.contains(nums[i])) {
            return true;
        }
        set.add(nums[i]);
    }
    return false;
}
```

## 给一个二叉搜索树，找到树中第 k 小的树。二叉搜索树的定义如下：

若任意节点的左子树不空，则左子树上所有节点的值均小于它的根节点的值；
若任意节点的右子树不空，则右子树上所有节点的值均大于它的根节点的值；
任意节点的左、右子树也分别为二叉查找树；
没有键值相等的节点。

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */

int num = 0;
int res;
public int kthSmallest(TreeNode root, int k) {
    inorderTraversal(root, k);
    return res;
}
private void inorderTraversal(TreeNode node, int k) {
    if (node == null) {
        return;
    }
    inorderTraversal(node.left, k);
    num++;
    if (num == k) {
        res = node.val;
        return;
    }
    inorderTraversal(node.right, k);
}
```

## 最长上升子序列的长度。

```java
public int lengthOfLIS(int[] nums) {
    int n = nums.length;
    if (n == 0) {
        return 0;
    }
    int dp[] = new int[n];
    int len = 0;
    for (int i = 0; i < n; i++) {
        int start = 0;
        int end = len;
        while (start < end) {
            int mid = (start + end) >>> 1;
            if (dp[mid] < nums[i]) {
                start = mid + 1;
            } else {
                end = mid;
            }
        }
        dp[start] = nums[i];
        if (start == len) {
            len++;
        }
    }
    return len;
}
```

## 将所有的 0 移动到末尾，并且保持其他数字的相对顺序不变。

```java
public void moveZeroes(int[] nums) {
    int j = 0;
    for (int i = 0; i < nums.length; i++) {
        //不等于 0 就交换
        if (nums[i] != 0) {
            int temp = nums[j];
            nums[j] = nums[i];
            nums[i] = temp;
            j++;
        }
    }
}
```

## 数组nums包含从0到n的所有整数，但其中缺了一个。请编写代码找出那个缺失的整数。在O(n)时间内完成

~~~javascript
```js
数组nums包含从0到n的所有整数，但其中缺了一个。
请编写代码找出那个缺失的整数。在O(n)时间内完成
```
const readline = require("readline");

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});
let long = [];
rl.question("", function (line) {
  long = line.split(",");
  console.log(miss_one(long));
  rl.close();

});


function miss_one(arr) {
  let data = 0;
  for (let i = 0; i < arr.length; i++) {
      //先用0异或0~nums.length的下标
      data ^= i;
      //再异或元素，一个数字出现两次，异或后为0，而异或最终的结果值为出现一次的数，即为缺失的元素
    data ^= parseInt(arr[i]);
    // console.log(data);
  }
  data ^= arr.length;
  return data;

}
      

~~~

## 数组求最大值

```javascript
function getMax(arr) {
        return Math.max.apply(null, arr);
}
```

## 统计数组中的元素出现次数

```javascript
let data =[1,1,2,3,1,2,45,21]; 
let objGroup = data.reduce(function (obj, name) {
        obj[name] = obj[name] ? ++obj[name] : 1;
        return obj;
 }, {});
 console.log(objGroup);  //{ "1": 3, "2": 2, "3": 1, "21": 1, "45": 1 }
 console.log(Object.entries(objGroup));  //[ [ "1", 3 ], [ "2", 2 ], [ "3", 1 ], [ "21", 1 ], [ "45", 1 ] ]
 console.log(Object.keys(objGroup));   //[ "1", "2", "3", "21", "45" ]
 console.log(Object.values(objGroup));  //[ 3, 2, 1, 1, 1 ]

```

## 已知圆中心,求半径问题

```javascript
const readline = require("readline");
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});
let i = 0;
var long = 0;
rl.question("", function (line) {
  long = parseInt(line);
});
var x = [];
var y = [];
rl.on("line", function (line) {
  i += 1;
  x.push(parseInt(line.split(" ")[0]));
  y.push(parseInt(line.split(" ")[1]));
  if (i == long) {
    console.log(main(x,y));
    rl.close();
  }
});

function main(_x,_y) {
    // let _x = [2, -2, 3, -3, 1,2,-1];
    // let _y = [-3, -3, 0, -1, -2, -2, 0];
    let result = [];
    for (let i = 0; i < _x.length; i++){
        for (let j = 0; j < _x.length; j++) {
                result.push(Math.pow((Math.pow((_x[i] - _x[j]),2)+Math.pow((_y[i] - _y[j]),2)),0.5)/2);
        }
    }
    let radius = result.filter((x) => { return x !== 0 }).sort();
    const unique = [...new Set(result.filter((x) => { return x !== 0 }).sort())];
    console.log(unique);
    let objGroup = radius.reduce(function (obj, name) {
        obj[name] = obj[name] ? ++obj[name] : 1;
        return obj;
      }, {});
    console.log(Object.entries(objGroup));

    function getMax(arr) {
        return Math.max.apply(null, arr);
    }
    let max_count = getMax(Object.values(objGroup));
    let max_index = Object.values(objGroup).lastIndexOf(max_count);

    return Object.entries(objGroup)[max_index][0];
   
}
```

## 位数相加，直到和位个位数

```js
function digital_root(n) {
  // ...
  let data = n
    .toString()
    .split("")
    .map((x) => {
      return parseInt(x);
    });
  let sum = 0;
  data.forEach((x) => {
    sum += x;
  });
  return sum < 9 ? sum : digital_root(sum);
}
//1+6+4=11
//1+1=2
//return 2
console.log(digital_root(164));

```

