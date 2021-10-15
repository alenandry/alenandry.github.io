# Generate .jar in java && run

### example code

```java
//package exec;

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

    public static void main(String[] args) throws IOException {
        run_py();
    }
}
```

1.create MANIFEST.MF file

```
Manifest-Version: 1.0
Main-Class: _Run_py
```

2.get class file

```java
javac _Run_py.java
```

3.generage .jar by the command

```
jar cmf ./MANIFEST.MF run_py.jar ./_Run_py.class
```

4.run .jar file

```java
java -jar ./run_py.jar
```
