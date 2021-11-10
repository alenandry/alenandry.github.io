# Java Codewar Solutions && Java grammar

## Java 多个线程同步运行

```java
class Counter{
int count;
public synchronized void increment(){ //两个线程不能同步执行该方法 加 synchronized
    count++;
	}
}
class RunSyncThread{
public void run() throws Exception{
    Counter c = new Counter();

        Thread t1 = new Thread(new Runnable() {
            @Override
            public void run() {
                for (int i = 0;i<1000;i++){
                    c.increment();
                }
            }
        });
        Thread t2 = new Thread(new Runnable() {
            @Override
            public void run() {
                for (int i = 0;i<1000;i++){
                    c.increment();
                }
            }
        });
    t1.run();
    t2.run();
    t1.join();
    t2.join();
    System.out.println(c.count);
	}
}

public class kata {
    public static void main(String[] args) throws Exception {
        RunSyncThread run_sync_thread = new RunSyncThread();
        run_sync_thread.run();
    }
}
```

## Java Streams

```java
import java.util.List;
import java.util.Set;
import java.util.Objects;
import java.util.stream.Collectors;

import static Streams._Stream.Gender.*;

public class _Stream {
    public static void main(String[] args) {
        List<_Stream.Person> people = List.of(
                new _Stream.Person("Alen", MALE),
                new _Stream.Person("Andrey", MALE),
                new _Stream.Person("Alex", FEMALE),
                new _Stream.Person("Amili", FEMALE),
                new _Stream.Person("Mali", PREFER_NOT_TO_SAY)
        );
//      [MALE, FEMALE]
       Set<Gender> genders =  people.stream()
                .map(person -> person.gender)
                .collect(Collectors.toSet());
       System.out.println(genders);

//    [Anana, Alex, Andrey, Alen, Amili]
        Set<String> names =  people.stream()
                .map(person -> person.name)
                .collect(Collectors.toSet());
        System.out.println(names);

//  filter some people in List
        List<Person> the_people_of_DONT_WANT_TO_SAY = people.stream().filter(ITEM ->ITEM.gender.equals(PREFER_NOT_TO_SAY)).collect(Collectors.toList());
        System.out.println("the_people_of_DONT_WANT_TO_SAY: "+the_people_of_DONT_WANT_TO_SAY);
        System.out.println("the_people_of_DONT_WANT_TO_SAY COUNT : "+people.stream().filter(ITEM ->ITEM.gender.equals(PREFER_NOT_TO_SAY)).count()); //count 满足条件的元素

//  Determine the presence or absence
//        .anyMatch(ITEM->ITEM.gender.equals(PREFER_NOT_TO_SAY)); //存在一个 就返回true
//        .allMatch(ITEM->ITEM.gender.equals(PREFER_NOT_TO_SAY)); //所有都满足 就返回true else 返回false
//        .noneMatch(ITEM->ITEM.gender.equals(PREFER_NOT_TO_SAY)); //与allMatch相反，判断条件里的元素，所有的都不是，返回true
        Boolean presence_SOME_PEOPLE_DONT_WANT_TO_SAY = people.stream().anyMatch(ITEM->ITEM.gender.equals(PREFER_NOT_TO_SAY)); //存在一个 就返回true
        System.out.println("presence_SOME_PEOPLE_DONT_WANT_TO_SAY： "+presence_SOME_PEOPLE_DONT_WANT_TO_SAY);
    }
    record Person(String name, Gender gender) {

        @Override
        public String toString() {
            return "Person{" +
                    "name='" + name + '\'' +
                    ", gender=" + gender +
                    '}';
        }

        @Override
        public int hashCode() {
            return Objects.hash(name, gender);
        }

    }
    enum Gender{
        MALE,FEMALE,PREFER_NOT_TO_SAY,
    }
}
```

## Java StringBuffer

```java
public class _StringBuffer {
    public static void main(String[] args) {
        StringBuffer sb = new StringBuffer();
        sb.append(15);  //add int
        sb.append("string");
        sb.append(true);
        sb.append(15);
        sb.append(15);
        sb.append(15);
        sb.append(15);
        sb.append(15);

        sb.insert(0, "first "); //0 index insert value

        sb.reverse(); //反转所有字符

        sb.delete(0, 5); //delete index 0..=4

        sb.replace(5, 8, "are"); //replace index 5..=7

        System.out.println("Print StingBuffer : "+sb);  //convert to string
        System.out.println(sb.charAt(0)); //get 0 index item
        System.out.println(sb.length()); //length
        System.out.println(sb.indexOf("string"));  //get string index
    }
}
```

## Java Math

```java
public class _Math {
    public static void main(String[] args) {
        // print the absolute value
        System.out.println(Math.abs(-7.89));

        // create long variable
        long c = 12345678l;
        long d = 987654321l;

        // addExact() with long arguments
        System.out.println(Math.addExact(c, d));  // 999999999

        // compute square root of 25
        System.out.println(Math.sqrt(25));

        // create a double variable
        double value2 = 27.0; //三次根号
        System.out.println(Math.cbrt(value2));  // 3.0

        // computes 5 raised to the power 3
        System.out.println(Math.pow(5, 3));

        // Math.min() with float arguments
        float num5 = 4.5f;
        float num6 = 9.67f;
        System.out.println(Math.min(num5, num6));  // 4.5

        // Math.min() with double arguments
        double num7 = 23.44d;
        double num8 = 32.11d;
        System.out.println(Math.min(num7, num8));  // 23.44

        // compute max of 88 and 98
        System.out.println(Math.max(88, 98));

        // Math.ceil() method (1.0 大 返回2.0）
        // value greater than 5 after decimal
        double a = 1.878;
        System.out.println(Math.ceil(a));  // 2.0

        // value equals to 5 after decimal
        double b = 1.5;
        System.out.println(Math.ceil(b));  // 2.0

        // value less than 5 after decimal
        double c1 = 1.34;
        System.out.println(Math.ceil(c1));  // 2.0

        //Math.floor() 向下取整
        double a1 = 3.8;
        System.out.println(Math.floor(a1)); //3

        //Math.round() 向上取整
        double a2 = 3.8;
        System.out.println(Math.round(a2)); //4

        //Ganerate Random number between 10 and 20
        int upperBound = 20;
        int lowerBound = 10;
        // upperBound 20 will also be included
        int range = (upperBound - lowerBound) + 1;
        System.out.println("Random Numbers between 10 and 20:");
        for (int i = 0; i < 10; i ++) {
            // generate random number
            // (int) convert double value to int
            // Math.round() generate value between 0.0 and 1.0
            int random = (int)(Math.random() * range) + lowerBound;
            System.out.print(random + ", ");
        }
        // Math.rint()
        // value greater than 5 after decimal
        System.out.println(Math.rint(1.878));  // 2.0

        // value less than 5 after decimal
        System.out.println(Math.rint(1.34));   // 1.0

        // value equal to 5 after decimal
        System.out.println(Math.rint(1.5));    // 2.0

        // value equal to 5 after decimal
        System.out.println(Math.rint(2.5));    // 2.0

    }
}

```

## Java Read File

```java
import java.io.*;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Paths;
import java.util.Collections;
import java.util.Iterator;
import java.util.List;
import java.util.Scanner;


public class _Read_File {

    public static void ReadFile_Use_BufferedReader() throws IOException {
        // We need to provide file path as the parameter:
        // double back quote is to avoid compiler interpret words
        // like \test as \t (ie as escape sequence)
        File file = new File("/home/alen/code/java_code/learn/src/File/test.txt");

        BufferedReader br = new BufferedReader(new FileReader(file));

        String st;
        while ((st = br.readLine()) != null) {
            System.out.println(st);
        }
    }

    public static void ReadFile_Use_FileReader() throws IOException {
        // pass the path to the file as a parameter
        FileReader fr =
                new FileReader("/home/alen/code/java_code/learn/src/File/test.txt");

        int i;
        while ((i=fr.read()) != -1)
            System.out.print((char) i);
    }

    public static void ReadFile_Use_Scanner() throws IOException {
        // pass the path to the file as a parameter
        {
            File file =
                    new File("/home/alen/code/java_code/learn/src/File/test.txt");
            Scanner sc = new Scanner(file);

            while (sc.hasNextLine())
                System.out.println(sc.nextLine());
        }

        {
            //without loop
            File file = new File("/home/alen/code/java_code/learn/src/File/test.txt");
            Scanner sc = new Scanner(file);

            // we just need to use \\Z as delimiter
            sc.useDelimiter("\\Z");

            System.out.println(sc.next());
        }
    }


    public static List<String> readFileInList(String fileName)
    {

        List<String> lines = Collections.emptyList();
        try
        {
            lines =
                    Files.readAllLines(Paths.get(fileName), StandardCharsets.UTF_8);
        }

        catch (IOException e)
        {

            // do something
            e.printStackTrace();
        }
        return lines;
    }
    public static void ReadFileIntoList(){
        List l = readFileInList("/home/alen/code/java_code/learn/src/File/test.txt");

        Iterator<String> itr = l.iterator();
        while (itr.hasNext())
            System.out.println(itr.next());
    }

    public static String readFileAsString(String fileName)throws Exception
    {
        String data;
        data = new String(Files.readAllBytes(Paths.get(fileName)));
        return data;
    }

        public static void main(String[] args) throws Exception {
            System.out.println("ReadFile_Use_BufferedReader:");
            ReadFile_Use_BufferedReader();

            System.out.println("ReadFile_Use_FileReader:");
            ReadFile_Use_FileReader();

            System.out.println("ReadFile_Use_Scanner:");
            ReadFile_Use_Scanner();

            System.out.println("ReadFileIntoList:");
            ReadFileIntoList();


            System.out.println("readFileAsString:");
            String data = readFileAsString("/home/alen/code/java_code/learn/src/File/test.js");
            System.out.println(data);

    }

}

```

## Java  Write File

```java
import java.io.*;

public class _Write_File {
    public static void Write_File_Use_BufferedWriter(){
        try {
            BufferedWriter out = new BufferedWriter(new FileWriter("/home/alen/code/java_code/learn/src/File/wrote_file.txt"));
            out.write("a String");
            out.close();
            System.out.println("File created successfully");
        }
        catch (IOException e) {
        }
    }
    public static void main(String[] args) {
        Write_File_Use_BufferedWriter();
    }
}

```

## Java Run Command (cmd)

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class _Run_py {
    public static void run_py(){
        try {
            Process p = Runtime.getRuntime().exec("python /home/alen/code/java_code/learn/src/exec/test.py");
            BufferedReader in = new BufferedReader(
                    new InputStreamReader(p.getInputStream()));
            String line = null;
            while ((line = in.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    public static void run_ls(){
        try {
            Process p = Runtime.getRuntime().exec("ls -lha");
            BufferedReader in = new BufferedReader(
                    new InputStreamReader(p.getInputStream()));
            String line = null;
            while ((line = in.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    public static void main(String[] args) throws IOException {
        run_py();
        run_ls();
    }
}
```

## Java CallBack

```java
import java.util.function.Consumer;
public class _CallBack {
    public static void main(String[] args) {
        hello("Alen",null,value->System.out.println("use Consumer: last_name not defined for :"+value));
        hello1("Alen",null,()->System.out.println(" use Runnable: last_name not defined"));
    }
//   用Consumer 跟javascript 的callback 一样 使用 callback
    static void hello(String fist_name, String lat_name, Consumer<String> callback){
        System.out.println(fist_name);
        if (lat_name !=null){
            System.out.println(lat_name);
        }else {
            callback.accept(fist_name);
        }
    }
//   用Runnable 跟javascript 的callback 一样 使用 callback
    static void hello1(String fist_name, String lat_name, Runnable callback){
        System.out.println(fist_name);
        if (lat_name !=null){
            System.out.println(lat_name);
        }else {
            callback.run();
        }
    }
}

```

## Java  Consumer

```java
package FunctionalInterface;

import java.util.function.BiConsumer;//take two argument return void
import java.util.function.Consumer;//take one argument return void

public class _Consumer {
    public static void main(String[] args) {

        System.out.println("//          normal function");
        greetingCustomer(new Customer("Alen", "15354843621"));

        System.out.println("//          Customer Function");
        greetingCustomer_ByConsumer.accept(new Customer("Andry", "19909284728"));

        System.out.println("//          BiCustomer Function");
        greetingCustomer_ByBiConsumer.accept((new Customer("Andry", "19909284728")),false);
    }
//    use Consumer
    static Consumer<Customer> greetingCustomer_ByConsumer = consumer->
        System.out.println("Hello "+consumer.CustomerName+"  Thanks for registering phone number  "+consumer.CustomerPhoneNumber);



// use void function
    static void greetingCustomer(Customer customer){
        System.out.println("Hello "+customer.CustomerName+"  Thanks for registering phone number  "+customer.CustomerPhoneNumber);
    }


// BiConsumer
    static BiConsumer<Customer,Boolean> greetingCustomer_ByBiConsumer = (customer,showPhoneNumber) ->
        System.out.println("Hello "+customer.CustomerName+"  Thanks for registering phone number  "+ (showPhoneNumber ? customer.CustomerPhoneNumber:"***************"));


    static class Customer{
        private final String CustomerName;
        private final String CustomerPhoneNumber;

        public Customer(String customerName, String customerPhoneNumber) {
            CustomerName = customerName;
            CustomerPhoneNumber = customerPhoneNumber;
        }
    }
}

```

## Java Function

```java
package FunctionalInterface;

import java.util.function.BiFunction; //take two argument return one
import java.util.function.Function; //take one argument return one

public class _Function {
    public static void main(String[] args) {
        System.out.println("***function***");
        int inc = increment(0);
        System.out.println(inc);

        System.out.println("***Function***");
        int inc1 = incrementFunction.apply(0);
        System.out.println(inc1);

        //合并两个Function
        Function<Integer,Integer> mergeFunction = incrementFunction.andThen(multipleBy10);

        int mergeResult = mergeFunction.apply(0);
        System.out.println(mergeResult);
        System.out.println(incrementFunction.andThen(multipleBy10).apply(0));

        //BIFunction
        System.out.println("***BiFunction***");
        BiFunction<Integer,Integer,Integer> multipleBiFunction = (num,numToMultipleBy)  //2个输入参数 1个输出参数
                ->(num +1)*numToMultipleBy;
        System.out.println(multipleBiFunction.apply(4,100));
    }
//    function
    static int increment(int num){
        num++;
        return num;
    }
//    Function
    static Function<Integer,Integer> incrementFunction = num -> num+1;

    static Function<Integer,Integer> multipleBy10 = num -> num*10;
}

```

## Java  Predicate

```java
package FunctionalInterface;

import java.util.function.BiPredicate; //take Two argument return Boolean
import java.util.function.Predicate;//take one argument return Boolean

public class _Predicate {
    public static void main(String[] args) {
        System.out.println(isPhoneNumberValid("15354843621"));
        System.out.println(isPhoneNumberValid("153548436201"));

        System.out.println(isPhoneNumberValid_ByUse_Predicate.test("15354843621"));

//        合并组合使用Predicate  and 同时满足为true
        System.out.println("//       Predicate");
        Boolean result = isPhoneNumberValid_ByUse_Predicate.and(containsNumber).test("15354843621");
        System.out.println(result);

//          合并组合使用Predicate 和 BiPredicate   && 同时满足为true
        System.out.println("//    BiPredicate");
        Boolean result1 = (isPhoneNumberValid_ByUse_Predicate.test("15354843621") &&containsNumber_Use_BiPredicate.test("15354843621",'9') );
        System.out.println(result1);
    }

    static  boolean isPhoneNumberValid(String phoneNumber){
        return phoneNumber.startsWith("1") && phoneNumber.length() ==11;
    }

    static Predicate<String> isPhoneNumberValid_ByUse_Predicate = phoneNumber->
                    phoneNumber.startsWith("1") && phoneNumber.length() ==11;

    static Predicate<String> containsNumber = phoneNumber ->
            phoneNumber.contains("3");

    static BiPredicate<String,Character> containsNumber_Use_BiPredicate = (phoneNumber,num) ->
            phoneNumber.contains(num.toString());

}
```

## Java  Supplier

```java
package FunctionalInterface;

import java.util.List;
import java.util.function.Supplier;//do not take any argument

public class _Supplier {
    public static void main(String[] args) {
        System.out.println("normal function");
        System.out.println(getConnectionUrl());

        System.out.println("use Supplier ");
        System.out.println(getConnectionUrl_Use_Supplier.get());
    }
    static String getConnectionUrl(){
        return "jdbc://localhost5432/user";
    }
    static Supplier<List<String>> getConnectionUrl_Use_Supplier = ()->
            List.of("jdbc://localhost5432/user",
                    "jdbc://localhost5432/user",
                    "jdbc://localhost5432/user"
            );
}
```



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

## Kata6 （统计元素出现次数，输出奇数次数的元素）

```java
import java.util.*;
import java.util.stream.Collectors;
import java.util.function.*;
class FindOdd {
    public static int findIt(int[] a) {
        HashMap<String, Integer> hashMap = new HashMap<>();
        for (Integer s : a){
            if(!hashMap.containsKey(s.toString())) {
                hashMap.put(s.toString(), 0);
            }
        }
        for (Integer s : a){
            if(hashMap.containsKey(s.toString())) {
                Integer value = hashMap.get(s.toString());
                value = value+1;
                hashMap.put(s.toString(),value);
            }
        }
//        System.out.println(hashMap);  //{1=2, 2=2, 3=2, 4=2, 5=3, 20=2}
//        System.out.println(hashMap.values());
        Integer oddIndex =0;
        for(Integer s : hashMap.values()) {
            oddIndex++;
            if(s%2!=0){
//                System.out.println(s);
                break;
            }
        }
//        System.out.println(hashMap.keySet()); //return key set
//        System.out.println(hashMap.keySet().toArray()[oddIndex-1]);
//        System.out.println(oddIndex);
//        System.out.println(FindOdd.findIt(new int[]{2,2,3,4,55,55,55})); // 输出出现次数 {55=3, 2=2, 3=1, 4=1}
        Integer oddNumber = Integer.parseInt((String) hashMap.keySet().toArray()[oddIndex-1]);
        return oddNumber;
    }
}

//solution 2
class FindOdd1 {
    public static int findIt(int[] A) {
        final TreeSet<Integer> set = new TreeSet<>();
        for (int x : A) {
            if (set.contains(x)) {
                set.remove(x);  //because return odd frequency so remove even frequency
            } else {
                set.add(x);
            }
        }
//        System.out.println(set); //[5]
        return set.first();
    }
}

```

## Kata7 (输出子字符串)

```java
/***
 *Which are in?
 *Given two arrays of strings a1 and a2 return a sorted array r in lexicographical order of the strings of a1 which are substrings of strings of a2.
 *
 * Example 1:
 * a1 = ["arp", "live", "strong"]
 *
 * a2 = ["lively", "alive", "harp", "sharp", "armstrong"]
 *
 * returns ["arp", "live", "strong"]
 */
import java.util.*;
import java.util.stream.Collectors;
import java.util.function.*;
class WhichAreIn {
    public static String[] inArray(String[] array1, String[] array2) {
        return Arrays.stream(array1)
                .filter(str -> Arrays.stream(array2).anyMatch(s -> s.contains(str)))
                .distinct()
                .sorted()
                .toArray(String[]::new);
    }
}

```

## Kata8 (判断出现o,x次数是否相同)

```java

/***
 *Exes and Ohs (if O和X的出现次数相同=>true)
 * Examples input/output:
 *
 * XO("ooxx") => true
 * XO("xooxx") => false
 * XO("ooxXm") => true
 * XO("zpzpzpp") => true // when no 'x' and 'o' is present should return true
 * XO("zzoo") => false
 */
class XO {
    public static boolean getXO (String str) {
        str = str.toLowerCase(Locale.ROOT); //转化为小写
        HashMap<String, Integer> hashMap = new HashMap<>();
        for (String s : str.split("")){
            if(!hashMap.containsKey(s.toString())) {
                hashMap.put(s, 0);
            }
        }
        for (String s : str.split("")){
            if(hashMap.containsKey(s.toString())) {
                Integer value = hashMap.get(s.toString());
                value = value+1;
                hashMap.put(s,value);
            }
        }
        String str1 = String.valueOf(hashMap.get("o"));
        String str2 = String.valueOf(hashMap.get("x"));
//        System.out.println(str1);
//        System.out.println(str2);

            if (hashMap.get("o")== null && hashMap.get("x")==null) {
                return true;
            }
            else if(hashMap.get("o")!= null && hashMap.get("x")!=null && hashMap.get("o").equals(hashMap.get("x"))) {
                return true;
            }
            else {
                return false;
            }


    }
}
```

## Kata9 (Count the smiley faces(用正则表达式))

```java
/**
 *Count the smiley faces!
 * Rules for a smiling face:
 * Each smiley face must contain a valid pair of eyes. Eyes can be marked as : or ;
 * A smiley face can have a nose but it does not have to. Valid characters for a nose are - or ~
 * Every smiling face must have a smiling mouth that should be marked with either ) or D
 * Example
 * countSmileys([':)', ';(', ';}', ':-D']);       // should return 2;
 * countSmileys([';D', ':-(', ':-)', ';~)']);     // should return 3;
 * countSmileys([';]', ':[', ';*', ':$', ';-D']); // should return 1;
 * Valid smiley face examples: :) :D ;-D :~)
 * Invalid smiley faces: ;( :> :} :]
 */
import java.util.*;
import java.util.stream.Collectors;
import java.util.function.*;
import java.util.TreeSet;
import java.util.stream.Stream;
class SmileFaces {
    public static int countSmileys(List<String> arr) {
        return (int)arr.stream().filter( x -> x.matches("[:;][-~]?[)D]")).count();
    }
}
```

## Kata10 (Merge Two list use stream)

```java
/***
 * Merge Two list use stream
 */
import java.util.*;
import java.util.stream.Collectors;
import java.util.function.*;
import java.util.TreeSet;
import java.util.stream.Stream;
class Merge{
    public static List run(List<String> List1, List<String> List2){
        // convert both lists into stream
        Stream<String> list1 = List1.stream();
        Stream<String> list2 = List2.stream();

        // merge two streams
        Stream<String> merged = Stream.concat(list1, list2);

        // convert the merged stream into list
        List<String> numbers = merged.collect(Collectors.toList());

        System.out.println("Merged List: " + numbers);
        return numbers;
    }
}
```

## Kata11 (Stack Application 栈的实现)

```java
/**
 *  包含min函数的栈
 */
import java.util.*;
import java.util.stream.Collectors;
import java.util.function.*;
import java.util.TreeSet;
import java.util.stream.Stream;
import java.util.Stack;
class StackApplication {
    private Stack<Integer> dataStack = new Stack<>(); // 数据栈
    private Stack<Integer> minStack = new Stack<>(); // 维护min函数的栈

    public void push(int node) {
        dataStack.push(node);

        if (minStack.isEmpty() || minStack.peek() > dataStack.peek()) {
            minStack.push(dataStack.peek()); // 当前minStack的栈顶元素大于数据栈的栈顶元素
        } else {
            minStack.push(minStack.peek()); // 当前minStack的栈顶元素小于数据栈的栈顶元素
        }
    }
    public void pop() {
        if (!dataStack.isEmpty()) {
            dataStack.pop();
        }
        if (!minStack.isEmpty()) {
            minStack.pop();
        }
    }
    public int top() {
        // 取出数据栈的栈顶元素
        return dataStack.peek();
    }
    public int min() {
        // 取出维护min函数的栈的栈顶元素
        return minStack.peek();
    }
}

public class kata {
    public static void main(String[] args) throws Exception {
        StackApplication st = new StackApplication();
        st.push(15);
        st.push(11);
        st.push(12);
        st.push(110);
        st.push(100);
        st.push(1515);
        st.pop(); //delete 1515
        System.out.println(st.top()); //100
        System.out.println(st.min());  //11
    }
}

```

## Kata12 (findKth Solution ,查找第K元素) 

```java
/**
 *findKth Solution
 */
class findKthSolution {
    public static int findKth(int[] a, int n, int K) {
        Arrays.sort(a);
        return(a[n-K]);
    }
}
```

## Kata15 (Largest Element Of Array 数组中最大的数)

```java

public class LargestElementOfArray {
    public static void main(String[] args){
        // Initialize array
        int[] arr = new int[] { 25, 11, 7, 75, 56 };
        // Initialize max with first element of array.
        int max = arr[0];
        // Loop through the array
        for (int i = 0; i < arr.length; i++) {
            // Compare elements of array with max
            if (arr[i] > max)
                max = arr[i];
        }
        System.out.println(max);

    }
}

```

## Kata16 （找出字符串中最长的回文子串长度）

```java

/**
 * 找出字符串中最长的回文子串长度
 */
public class longestPalindromeSequence {

    public static int longestPalindrome(String s) {
        int len = s.length();
        int [][] dp = new int[len][len];
        for(int i = len - 1; i>=0; i--){
            dp[i][i] = 1;
            for(int j = i+1; j < len; j++){
                if(s.charAt(i) == s.charAt(j))
                    dp[i][j] = dp[i+1][j-1] + 2;
                else
                    dp[i][j] = Math.max(dp[i+1][j], dp[i][j-1]);
            }
        }
        return dp[0][len-1];
    }

    public static void main(String[] args) {
        System.out.println(longestPalindromeSequence.longestPalindrome("bbbabaaabcdabcd")); //9

    }
}

```

## Kata17 (判断是否有重复部分)

```java
import java.util.HashSet;

public class _isDuplicate {
    public static void main(String[] args) {
        int[] arr = {1,9,2,3,5,4};
        System.out.println(containsDuplicate(arr));
    }
    public static boolean containsDuplicate(int[] nums) {
        HashSet<Integer> set = new HashSet<>();
        for (int i = 0; i < nums.length; i++) {
            if (set.contains(nums[i])) {
                return true;
            }
            set.add(nums[i]);
        }
        return false;
    }
}
```

## Kata18 (数组元素出现频度统计)

```java
public class arrayFrequency {
    public static void main(String[] args) {
        // Initialize array
        int[] chars = new int[] { 1, 2, 8, 3, 2, 2, 2, 5, 1 };
        // Array fr will store frequencies of element
        int[] fr = new int[chars.length];
        for (int i = 0; i < chars.length; i++) {
            int count = 1;
            for (int j = i + 1; j < chars.length; j++) {
                if (chars[j] == chars[i]) {
                    count++;
                    fr[j] = -1;

                }
            }
            if (fr[i] != -1) {
                fr[i] = count;
            }
        }
        for (int i = 0; i < fr.length; i++) {
            if (fr[i] != -1)
                System.out.println("    " + chars[i] + "    |    " + fr[i]);
        }
       
    }
}

/**
*输出
*   1    |    2
    2    |    4
    8    |    1
    3    |    1
    5    |    1
*/
```

## Kata19 (java 生成随机数)

```java
import java.util.Random;
import java.util.function.Consumer;
/**
 * 生成随机数
 */
public class random {
	public static void main(String[] args) {
		Consumer<Integer> print = name-> {System.out.println(name);};
		Random random = new Random();
		int int_random = random.nextInt(); //输出int 范围内的 random number
		print.accept(int_random);

		int int_random1 = random.nextInt(6); //输出范围0-6
		System.out.println(int_random1);
		
		double double_random = random.nextDouble(); //输出double 范围 0-1 之间的 double number
		System.out.println(double_random);
		
		float float_random = random.nextFloat(); //输出float 范围 0-1 之间的 float number
		System.out.println(float_random);
		
		boolean boolean_random = random.nextBoolean(); //输出boolean 范围
		System.out.println(boolean_random);
	}
}

```

## Kata20 (Java Reverse Array 数组反转)

```java
import java.util.Arrays;
public class ReverseArray {
    public static void main(String[] args) {
        int[] array = new int[] { 1, 2, 3, 4, 5, 6, 7 };
        int[] reverse_array = new int[array.length];
        System.out.println("orignal arr:"+ Arrays.toString(array));
        for (int i = 0; i < array.length; i++) {
//            System.out.println(array[array.length - 1 - i]);
            reverse_array[i] = array[array.length - 1 - i];
        }
//        orignal arr:[1, 2, 3, 4, 5, 6, 7]
//        reversed arr:[7, 6, 5, 4, 3, 2, 1]
        System.out.println("reversed arr:" + Arrays.toString(reverse_array));
    }   
}
```

## Kata 21 (PasrInt String use Java 转化为Int)

```java
public class StrToInt {
    public static int StrToInt(String str) {
        if (str.length() == 0)
            return 0;
        char[] chars = str.toCharArray();
        // 判断是否存在符号位
        int flag = 0;
        if (chars[0] == '+')
            flag = 1;
        else if (chars[0] == '-')
            flag = 2;
        int start = flag > 0 ? 1 : 0;
        int res = 0;// 保存结果
        for (int i = start; i < chars.length; i++) {
            if (Character.isDigit(chars[i])) {// 调用Character.isDigit(char)方法判断是否是数字，是返回True，否则False
                int temp = chars[i] - '0';
//                System.out.println(temp);
                res = res * 10 + temp;
//                System.out.println(res);
            } else {
                return 0;
            }
        }
        return flag != 2 ? res : -res;

    }

    public static void main(String[] args) {
        // TODO Auto-generated method stub
        String s = "-1231231225";
        System.out.println("使用库函数转换：" + Integer.valueOf(s));
        int res = StrToInt(s);
        System.out.println("使用自己写的方法转换：" + res);
//        使用库函数转换：-1231231225
//        使用自己写的方法转换：-1231231225
    }
}
```

## Kata 22 (查找返回Index，binarySearch )

```java
/***
 * 小到大排序的数组返回index (binarySearch)
 * in:{1,5,9,15,20,23},15
 * out:target index 3
 * can't find target return -1
 * 时间复杂度 log(n)
 */

class binarySearch{
    public static int search(int[] values,int target){
        int left = 0;
        int right = values.length-1;
        int result = -1;
        while(left <=right){
            Integer mid = (left + right)/2;
            if(values[mid]==target){
                result = mid;
                break;
            }
            else if(values[mid] <target){
                left=mid+1;
            }else {
                right=mid-1;
            }
        }
        return result;

    }
}
```

## Kata 23 ( List 交换相邻的元素 返回交换的List)

```java
/**
 * List 交换相邻的元素 返回交换的List
 *out:[2, 1, 4, 3, 6,5]
 *in:[1, 2, 3, 4, 5,6]
 */
class reverse_neighbours
{
    public static List<Integer> reverse_(List<Integer> array) {
        List<Integer> list3 = new ArrayList<Integer>();
        for (int i = 0; i < array.size(); i++) {
            list3.add(0);
        }
        if(array.size()%2==0){
            for(int i=0;i<list3.size();i++){
                if(i%2==0)list3.set(i,array.get(i+1));
                if(i%2==0)list3.set(i+1,array.get(i));
            }
        }else {
            for(int i=0;i<list3.size()-1;i++){
                if(i%2==0)list3.set(i,array.get(i+1));
                if(i%2==0)list3.set(i+1,array.get(i));
            }
            list3.set(list3.size()-1,array.get(list3.size()-1));
        }
        System.out.println(list3);
        return list3;
    }
}
//System.out.println(reverse_neighbours.reverse_(Arrays.asList(new Integer[]{1, 2, 3, 4, 5})));
```

## Kata 24 (slice List)

```java
/**
 *         input:(["python", "pip", "ok","java","rust","cpp","kotlin"],3,5);
 *         output:[java, rust, cpp]
 */
class slice_list{
    public static <T> List<String> slice(List<T> asList,Integer start, Integer end) {
        List<String> list1 = new ArrayList();
        for(Integer s=start; s<=end; s++) {
            list1.add((String) asList.get(s));
        }
        return list1;
    }
}
//System.out.println(slice_list.slice(Arrays.asList(new String[]{"python", "pip", "ok","java","rust","cpp","kotlin"}),3,5));
```

## Kata 25 (高精度计算,BigDecimal)

```java
/**
 *java浮点数运算精度损失，用BigDecimal 解决
 */
class sumBigDecimal{
    public static double sum(double value1,double value2){
        java.math.BigDecimal big_val1 = new java.math.BigDecimal(Double.toString(value1));
        java.math.BigDecimal big_val2 = new java.math.BigDecimal(Double.toString(value2));
        double result = big_val1.add(big_val2).doubleValue();
        return result;
    }
}
//System.out.println(sumBigDecimal.sum(1.21,3.51)); //4.72
```

## Kata 26 (求一个数的平方根)

```java
/**
 * 求一个数的平方根
 */
class sqrt{
    public static double sqrt(int x){
        if(x==0 ||x==1)return x;
        double r = x;
        while(r*r>x){
            r = (r+x/r)/2;
        }
        return r;
    }
}
```

## 

