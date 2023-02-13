### This is a weak password data-set, not a full random string data-set.

> ⚠️Attention!
>
> - The compressed package contains a file sorted by length, and the file  size after decompression is close to `3GB`.
> - The compressed package uses `.7z` format, because the average user github allows  uploading files with a size of `100M`, and the compressed package in `.7z` format  will be smaller.

- 123456
- 1234567
- 12345678
- hua1997
- hua20041223
- ming1998
- ming20041223
- 💥💥💥



##### 一、Reference example（Java）

```java
import net.lingala.zip4j.ZipFile;
import net.lingala.zip4j.exception.ZipException;

import java.io.*;
import java.time.LocalDateTime;
import java.util.Comparator;

public class Main {
    public static void main(String[] args) throws IOException {
        System.out.println("Process Start: >>>" + LocalDateTime.now());
        final int PASSWORD_COUNT = 250_003_832;

        int i = 0;
        try (BufferedReader bfr = new BufferedReader(new FileReader("G:\\weak_password_length_sorted.data"));
             ZipFile zipFile = new ZipFile("C:\\Users\\abc\\Desktop\\abc1.zip");) {
            while (i < PASSWORD_COUNT) {
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
//        try (BufferedReader br = new BufferedReader(new FileReader("G:\\weak_password_length_sorted.data"));
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

