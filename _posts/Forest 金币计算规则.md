# Forest

目前金币计算方式如下：

假设总时长为 t：

📍大树

**4** + **1 / 5 t** + **5 \* ( t-30 ) / 30**

举例来说，65分钟可以获得4 + 13 + 5 = 22金币

📍小树

**1 + 1 / 5分钟**

举例来说，15分钟的树可以获得 1 + 3 = 4 金币



## TreeMap

``` java
import java.util.Map;
import java.util.Scanner;
import java.util.TreeMap;

public class Main {
    public static void main(String[] args) {
        int max = 180;
        TreeMap<Integer, Integer> map = new TreeMap<>();
        for (int t = 10; t <= max; t += 5) {
            map.put(t, fun(t));
        }
        for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
            int key = entry.getKey();
            int value = entry.getValue();
            float percent = (float) value / key;
            System.out.printf("%3d min %3d coins %.3f\n", key, value, percent);
        }
        Scanner scanner = new Scanner(System.in);
        while (scanner.hasNextInt()) {
            System.out.println(map.getOrDefault(scanner.nextInt() / 5 * 5, -1));
        }
    }

    private static Integer fun(int t) {
        if (t <= 20) {
            return 1 + t / 5;
        }
        return 4 + t / 5 + (t - 30) / 30 * 5;
    }
}
```



## 数组



```
 10 min   3 coins 0.300
 15 min   4 coins 0.267
 20 min   5 coins 0.250
 25 min   9 coins 0.360
 30 min  10 coins 0.333
 35 min  11 coins 0.314
 40 min  12 coins 0.300
 45 min  13 coins 0.289
 50 min  14 coins 0.280
 55 min  15 coins 0.273
 60 min  21 coins 0.350
 65 min  22 coins 0.338
 70 min  23 coins 0.329
 75 min  24 coins 0.320
 80 min  25 coins 0.313
 85 min  26 coins 0.306
 90 min  32 coins 0.356
 95 min  33 coins 0.347
100 min  34 coins 0.340
105 min  35 coins 0.333
110 min  36 coins 0.327
115 min  37 coins 0.322
120 min  43 coins 0.358
125 min  44 coins 0.352
130 min  45 coins 0.346
135 min  46 coins 0.341
140 min  47 coins 0.336
145 min  48 coins 0.331
150 min  54 coins 0.360
155 min  55 coins 0.355
160 min  56 coins 0.350
165 min  57 coins 0.345
170 min  58 coins 0.341
175 min  59 coins 0.337
180 min  65 coins 0.361
```

