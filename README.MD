### This is a weak password data-set, not a full random string data-set.

> ⚠️Attention!
>
> - The compressed package contains three files with different sorted versions, and  the data are consistent. 
> - Each file is close to the size of 3GB. If your computer  has limited storage space, please just extract one of the files.

- 123456
- 1234567
- 12345678
- hua1997
- hua20041223
- ming1998
- ming20041223
- 💥💥💥



#### 一、Reference example（Java）

```java
import net.lingala.zip4j.ZipFile;
import net.lingala.zip4j.exception.ZipException;

import java.io.*;
import java.time.LocalDateTime;
import java.util.Comparator;

public class Main {
    public static void main(String[] args) throws IOException {
        System.out.println("Process Start: >>>" + LocalDateTime.now());

        int i = 1;
        try (BufferedReader bfr = new BufferedReader(new FileReader("G:\\weak_password_length_sorted.data"));
             ZipFile zipFile = new ZipFile("C:\\Users\\abc\\Desktop\\abc1.zip");) {
            while (i <= 249945593) {
                zipFile.setPassword(bfr.readLine().toCharArray());
                try {
                    zipFile.extractAll("destination_directory");
                    break;
                } catch (ZipException e) {
                    i++;
                }
                if (i % 100000 == 0) System.out.println("已经检索" + i / 10000 + "W条数据了，请稍后！");
            }
        }

        System.out.println("Process End: >>>" + i);
        System.out.println(LocalDateTime.now());
    }

//    public static void main(String[] args) throws IOException {
//        try (BufferedReader br = new BufferedReader(new FileReader("G:\\常见弱口令\\weak_password_name_sorted_desc.data"));
//             BufferedWriter bw = new BufferedWriter(new FileWriter("weak_password_length_sorted.data"))) {
//
//            br.lines().map(String::strip).filter(x -> x.length() <= 32).sorted(Comparator.comparingInt(String::length)).distinct().forEach(x -> {
//            // br.lines().map(String::strip).filter(x->x.length()<=32).sorted().distinct().forEach(x->{
//            // br.lines().map(String::strip).filter(x -> x.length() <= 32).sorted(Comparator.reverseOrder()).distinct().forEach(x -> {
//                try {
//                    bw.write(x);
//                    bw.newLine();
//                } catch (IOException e) {
//                    throw new RuntimeException(e);
//                }
//            });
//        }
//    }
}
```

```xml
<!-- zip4j -->
<dependency>
    <groupId>net.lingala.zip4j</groupId>
    <artifactId>zip4j</artifactId>
    <version>2.11.4</version>
</dependency>
```

