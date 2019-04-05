## 爬楼梯 Climbing Stairs

### 题目描述

假设你正在爬楼梯。需要 n 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

注意：给定 n 是一个正整数。

示例 1：

输入： 2
输出： 2
解释： 有两种方法可以爬到楼顶。
1.  1 阶 + 1 阶
2.  2 阶
示例 2：

输入： 3
输出： 3
解释： 有三种方法可以爬到楼顶。
1.  1 阶 + 1 阶 + 1 阶
2.  1 阶 + 2 阶
3.  2 阶 + 1 阶

### 解题思路

本题可以使用斐波那契数求解。

```
Fib(n)=Fib(n-1)+Fib(n-2) Fib(n)=Fib(n−1)+Fib(n−2)
```

现在我们必须找出以 1 和 2 作为第一项和第二项的斐波那契数列中的第 nn 个数，也就是说 Fib(1)=1Fib(1)=1 且 Fib(2)=2Fib(2)=2。

### 实现代码

```java
class Solution {
    public int climbStairs(int n) {
        if (n == 1) {
            return 1;
        }
        int first = 1;
        int second = 2;
        for (int i = 3; i <= n; i++) {
            int third = first + second;
            first = second;
            second = third;
        }
        return second;
        
    }
}

public class MainClass {
    public static void main(String[] args) throws IOException {
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        String line;
        while ((line = in.readLine()) != null) {
            int n = Integer.parseInt(line);
            
            int ret = new Solution().climbStairs(n);
            
            String out = String.valueOf(ret);
            
            System.out.print(out);
        }
    }
}
```

#### 时间复杂度

时间复杂度：O(n)O(n)。单循环到 nn，需要计算第 nn 个斐波那契数。

#### 空间复杂度

空间复杂度：O(1)O(1)。使用常量级空间。 
