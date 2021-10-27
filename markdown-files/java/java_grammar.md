# Java Codewar Solutions && Java grammar

## Kata1 （用ASCII码加密 数据）

```java
/*
*Encrypt this!
 *Examples:
Kata.encryptThis("Hello") => "72olle"
Kata.encryptThis("good") => "103doo"
Kata.encryptThis("hello world") => "104olle 119drlo"
 */
import java.util.*;
import java.util.stream.Collectors;
import java.util.function.*;

class Kata1 {
    public static String encryptThis(String text) {
        UnaryOperator<String> encrtyper = s -> {
            switch (s.length()) {
                case 0:
                    return s;
                case 1:
                    return String.valueOf((int) s.charAt(0));
                case 2:
                    return (int) s.charAt(0) + s.substring(s.length()-1);
                default:
                    return (int) s.charAt(0) + s.substring(s.length()-1) + s.substring(2, s.length()-1) + s.substring(1, 2);
            }
        };
        return Arrays.stream(text.split(" "))
                .map(s -> encrtyper.apply(s))
                .collect(Collectors.joining(" "));
    }
}

```

## Kata2  （转化为二进制 ，数1的个数）

```java
/***
 * Bit Counting (转化为二进制 ，数1的个数)
 * Example: The binary representation of 1234 is 10011010010, so the function should return 5 in this case
 */
import java.util.*;
import java.util.stream.Collectors;
import java.util.function.*;
class BitCounting1 {
    public static int countBits(int n){
        // Show me the code!
        String binary = String.valueOf(Integer.toBinaryString(n));
        int count = 0;
        for(String s : binary.split("")){
            if(s.equals("1")){
                count++;
            }
        }
        return count;
    }
}
class BitCounting2 {
    public static int countBits(int n){
        return Integer.bitCount(n);
    }
}

```

## Kata3 （返回，最小和最大数）

```java
/***
 * The highest profit wins!(返回，最小和最大数)
 * Examples
 * MinMax.minMax(new int[]{1,2,3,4,5}) == {1,5}
 * MinMax.minMax(new int[]{2334454,5}) == {5, 2334454}
 * MinMax.minMax(new int[]{1}) == {1, 1}
 */
import java.util.*;
import java.util.stream.Collectors;
import java.util.function.*;
class MinMax {
    public static int[] minMax(int[] arr) {
        // Your awesome code here
        int min = Arrays.stream(arr)
                .min()
                .getAsInt();
        int max = Arrays.stream(arr)
                .max()
                .getAsInt();
        return new int[]{min, max};
    }
}
```

## Kata4 （排序array）

```java
/***
 * Array Sort (数组小到大排序) int
 */
import java.util.*;
import java.util.stream.Collectors;
import java.util.function.*;
class Sort1{
    public static int[] ArraySort(int[] arr){
        Arrays.sort(arr);
        return arr;
    }
//System.out.println(Arrays.toString(Sort.ArraySort(new int[]{51,26,6,14,2}))); //[2, 6, 14, 26, 51]
}

/***
 * Array Sort (数组小到大排序) String
 */
class Sort2{
    public static String[] ArraySort(String[] arr){
        Arrays.sort(arr);
        return arr;
    }
//        System.out.println(Arrays.toString(Sort2.ArraySort(new String[]{"d","a","c"}))); //[a, c, d]
}
```

## Kata5 （卡号部分模糊显示）

```java

/**
 *Credit Card Mask  (卡号模糊显示)
 * Examples
 * Maskify.Maskify("4556364607935616"); // should return "############5616"
 * Maskify.Maskify("64607935616");      // should return "#######5616"
 * Maskify.Maskify("1");                // should return "1"
 * Maskify.Maskify("");                 // should return ""
 * // "What was the name of your first pet?"
 * Maskify.Maskify("Skippy");                                   // should return "##ippy"
 * Maskify.Maskify("Nananananananananananananananana Batman!"); // should return "####################################man!"
 */
import java.util.*;
import java.util.stream.Collectors;
import java.util.function.*;
class Maskify {
    public static String maskify(String str) {
        List<String> list = new ArrayList<String>();
        for (String s : str.split("")){
            list.add(s);
        }
        if(list.size()>4){
            for (int i = 0; i < list.size()-4; i++) {
                list.set(i,"*");
            }
        }
//        System.out.println(list.stream().collect(Collectors.joining(" ")));
        return list.stream().collect(Collectors.joining(""));
    }
}

```

## Kata6 （）

```java

```

