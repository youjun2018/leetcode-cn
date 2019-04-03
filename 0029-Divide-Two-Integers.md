# 两数相加 Add Two Numbers

## 题目描述



## 解题思路



## 实现代码
### 自己的代码
#### java 代码


##### 自己 java 代码分析
###### 时间复杂度


###### 空间复杂度



### 大神的代码
#### java 代码


##### 大神 java 代码分析
###### 时间复杂度


###### 空间复杂度



## 总结归纳



## 遇到的问题



## 参考链接



## 知识延伸



end of this page


```Java
class Solution {
    public int divide(int dividend, int divisor) {
        int sign = 1;  // 符号
        int quotien = 0;  // 商
        int remainder = 0;  // 余数

        int idividend = 0;
        int idivisor = 0;

        if (dividend < 0) {
            sign *= -1;
            idividend = -1 * dividend;
        }
        if (divisor < 0) {
            sign *= -1;
            idivisor = -1 * divisor;
        }
        System.out.println("sign: " + sign);

        while (idividend >= idivisor) {
            idividend -= idivisor;
            quotien += 1;
            System.out.println("idividend: " + idividend);
            System.out.println("quotien: " + quotien);
        }

        return sign * quotien;

    }
}

```

```Java
public int divide(int dividend, int divisor) {
        int sign = 1;  // 符号
        int quotien = 0;  // 商
        int remainder = 0;  // 余数

        int idividend = 0;
        int idivisor = 0;

        if (dividend < 0) {
            sign *= -1;
            idividend = -1 * dividend;
        } else {
            idividend = dividend;
        }

        if (divisor < 0) {
            sign *= -1;
            idivisor = -1 * divisor;
        } else {
            idivisor = divisor;
        }

        while (idividend >= idivisor) {
            idividend -= idivisor;
            quotien += 1;
        }

        return sign * quotien;

    }
```

```Java
class Solution {
    public int divide(int dividend, int divisor) {
        double sign = 1;  // 符号
        double quotien = 0;  // 商

        double idividend = 0;
        double idivisor = 0;

        if (dividend < 0) {
            System.out.println("dividend < 0");
            sign *= -1.0;
            idividend = -1.0 * dividend;
        } else {
            System.out.println("dividend >= 0");
            idividend = dividend;
        }

        if (divisor < 0) {
            sign *= -1;
            idivisor = -1 * divisor;
        } else {
            idivisor = divisor;
        }

        if(idivisor == 1.0) {
            quotien = idividend;
        } else {
            while (idividend >= idivisor) {
            idividend -= idivisor;
            quotien += 1;
            }
        }


        quotien *= sign;

        if(quotien > (double)Integer.MAX_VALUE || quotien < (double)Integer.MIN_VALUE)
            quotien = (double)Integer.MAX_VALUE;

        System.out.println("---------------");
        return (int)(quotien);

    }
}
```

```Java
// 超出时间限制
class Solution {
    public int divide(int dividend, int divisor) {
        long sign = 1;  // 符号
        long quotien = 0;  // 商

        long idividend = 0;
        long idivisor = 0;

        if (dividend < 0) {
            sign *= (long)(-1);
            idividend = (long)(-1) * dividend;
        } else {
            idividend = dividend;
        }

        if (divisor < 0) {
            sign *= (long)(-1);
            idivisor = (long)(-1) * divisor;
        } else {
            idivisor = divisor;
        }

        if(idivisor == (long)(1)) {
            quotien = idividend;
        } else {
            while (idividend >= idivisor) {
            idividend -= idivisor;
            quotien += (long)1;
            }
        }


        quotien *= sign;

        if(quotien > (long)Integer.MAX_VALUE || quotien < (long)Integer.MIN_VALUE)
            quotien = (long)Integer.MAX_VALUE;

        return (int)(quotien);

    }
}
```

```java
/**
     * 解题思路：这题是除法，所以先普及下除法术语
     * 商，公式是：(被除数-余数)÷除数=商，记作：被除数÷除数=商...余数，是一种数学术语。
     * 在一个除法算式里，被除数、余数、除数和商的关系为：(被除数-余数)÷除数=商，记作：被除数÷除数=商...余数，
     * 进而推导得出：商×除数+余数=被除数。
     *
     * 要求商，我们首先想到的是减法，能被减多少次，那么商就为多少，但是明显减法的效率太低
     *
     * 那么我们可以用位移法，因为计算机在做位移时效率特别高，向左移1相当于乘以2，向右位移1相当于除以2
     *
     * 我们可以把一个dividend（被除数）先除以2^n，n最初为31，不断减小n去试探,当某个n满足dividend/2^n>=divisor时，
     *
     * 表示我们找到了一个足够大的数，这个数*divisor是不大于dividend的，所以我们就可以减去2^n个divisor，以此类推
     *
     * 我们可以以100/3为例
     *
     * 2^n是1，2，4，8...2^31这种数，当n为31时，这个数特别大，100/2^n是一个很小的数，肯定是小于3的，所以循环下来，
     *
     * 当n=5时，100/32=3, 刚好是大于等于3的，这时我们将100-32*3=4，也就是减去了32个3，接下来我们再处理4，同样手法可以再减去一个3
     *
     * 所以一共是减去了33个3，所以商就是33
     *
     * 这其中得处理一些特殊的数，比如divisor是不能为0的，Integer.MIN_VALUE和Integer.MAX_VALUE
     *
     */

    public int divide(int dividend, int divisor) {
        if (dividend == 0) {
            return 0;
        }
        if (dividend == Integer.MIN_VALUE && divisor == -1) {
            return Integer.MAX_VALUE;
        }
        boolean negative;
        negative = (dividend ^ divisor) <0;//用异或来计算是否符号相异
        long t = Math.abs((long) dividend);
        long d= Math.abs((long) divisor);
        int result = 0;
        for (int i=31; i>=0;i--) {
            if ((t>>i)>=d) {//找出足够大的数2^n*divisor
                result+=1<<i;//将结果加上2^n
                t-=d<<i;//将被除数减去2^n*divisor
            }
        }
        return negative ? -result : result;//符号相异取反
    }
```
