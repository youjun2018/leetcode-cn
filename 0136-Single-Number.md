## 只出现一次的数字 Single Number

### 题目描述

给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

说明：

你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

示例 1:

输入: [2,2,1]

输出: 1

示例 2:

输入: [4,1,2,1,2]

输出: 4

### 解题思路

本题的数组很特殊，只有一个数字出现一次，其余的数字均出现两次，考虑用异或运算。

* 交换律：a ^ b ^ c <=> a ^ c ^ b

* 任何数于0异或为任何数 0 ^ n => n

* 相同的数异或为0: n ^ n => 0

* 即异或：相同为0，不同为1. 异或同一个数两次，原数不变。

### 实现代码

```java
class Solution {
    public int singleNumber(int[] nums) {
        int a = 0;
        for(int num : nums) {
            a = a ^ num;
        }
        return a;
    }
}

public class MainClass {
    public static int[] stringToIntegerArray(String input) {
        input = input.trim();
        input = input.substring(1, input.length() - 1);
        if (input.length() == 0) {
          return new int[0];
        }
    
        String[] parts = input.split(",");
        int[] output = new int[parts.length];
        for(int index = 0; index < parts.length; index++) {
            String part = parts[index].trim();
            output[index] = Integer.parseInt(part);
        }
        return output;
    }
    
    public static void main(String[] args) throws IOException {
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        String line;
        while ((line = in.readLine()) != null) {
            int[] nums = stringToIntegerArray(line);
            
            int ret = new Solution().singleNumber(nums);
            
            String out = String.valueOf(ret);
            
            System.out.print(out);
        }
    }
}
```

#### 时间复杂度

时间复杂度 O(n), n 为数组的长度。

#### 空间复杂度

空间复杂度 O(1), 没使用额外的空间。
