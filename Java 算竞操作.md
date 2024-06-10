# Java 算竞操作

****

## 输入输出

****

### 简单写法

****

数据量不大：

```java
Scanner sc = new Scanner(System.in);
int a = sc.nextInt();
char op = sc.nextLine().charAt(0);
```

如果比较大可以换：

```java
Scanner sc = new Scanner(new BufferedInputStream(System.in))
```

不嫌麻烦可以写：

```java
public class Main {

    static BufferedReader cin = new BufferedReader(new InputStreamReader(System.in));
    static PrintWriter cout = new PrintWriter(new OutputStreamWriter(System.out));

    public static void main(String[] args) throws IOException {
        int a = Integer.parseInt(cin.readLine());
        cout.println(a);
//        cin.close();
        cout.flush();
        cout.println(a);
        cout.flush();
    }
}
```

****

### 快读板子

****

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.util.StringTokenizer;

public class Main {
    static Cin cin = new Cin();
    static PrintWriter cout = new PrintWriter(System.out);

    static void solve() {
        int n = cin.nextInt();
        for (int i = 0; i < n; i ++) {
            char op = cin.nextChar();
            cout.println(op);
        }
    }

    public static void main(String[] args) {
        int t = 1;
//        t = cin.nextInt();
        for (int i = 0; i < t; i ++) {
            solve();
        }
        cout.flush();
    }

    static class Cin {

        static BufferedReader br;
        static StringTokenizer st;

        Cin() {
            br = new BufferedReader(new InputStreamReader(System.in));
        }

        String next() {
            String s = "";
            while (st == null || !st.hasMoreElements()) {
                try {
                    s = br.readLine();
                } catch (IOException e) {
                    throw new RuntimeException(e);
                }
                st = new StringTokenizer(s);
            }
            return st.nextToken();
        }

        int nextInt() {
            return Integer.parseInt(next());
        }

        double nextDouble() {
            return Double.parseDouble(next());
        }

        long nextLong() {
            return Long.parseLong(next());
        }

        char nextChar() {
            return next().charAt(0);
        }

    }

}
```

****

### 多实例输入

****

```java
public class Main {

    static Scanner sc = new Scanner(new BufferedInputStream(System.in));

    public static void main(String[] args) {
        while (sc.hasNext()) {
            int a = sc.nextInt();
            System.out.println(a);
        }
    }
}
```

****

## BigInteger 常用 API







































