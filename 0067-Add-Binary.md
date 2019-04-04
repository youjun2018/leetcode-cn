# 二进制求和 Add Binary

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
a.charAt(index) 不是 a.CharAt(index)

```java
class Solution {
    public String addBinary(String a, String b) {
        int aFlag = a.length() - 1;
        int bFlag = b.length() - 1;

        System.out.println("a.length() = " + a.length());
        char[] aStr = a.toCharArray();
        System.out.println(aStr.length);

        int loopTime = (aFlag > bFlag)? aFlag : bFlag;

        int carry = 0;

        String retStr = "";

        while(loopTime >= 0){
            // int x = (aFlag >= 0) ? a.charAt(aFlag) - '0' : 0;  // 不能使用自动强制类型转换  当a.charAt(aFlag) 为 '1' 时，x 为14
            // int y = (bFlag >= 0) ? b.charAt(bFlag) - '0' : 0;  // 自动强制类型转换

            // int x = (aFlag >= 0) ? Integer.parseInt(String.valueOf(a.charAt(aFlag))) : 0;  // 不能使用自动强制类型转换 java.lang.NumberFormatException: For input string: """
            // int y = (bFlag >= 0) ? Integer.parseInt(String.valueOf(b.charAt(bFlag))) : 0;  // 自动强制类型转换

            System.out.println(aFlag);
            System.out.println(a.charAt(aFlag));

            int x = (aFlag >= 0) ? Integer.parseInt("" + a.charAt(aFlag)) : 0;  // 不能使用自动强制类型转换
            int y = (bFlag >= 0) ? Integer.parseInt("" + b.charAt(bFlag)) : 0;  // 自动强制类型转换

            int sum = carry + x + y;

            System.out.println("x: " + x);
            System.out.println("y: " + y);

            if(sum < 2){
                retStr += String.valueOf(sum);
                carry = 0;
            }
            else {
                retStr += String.valueOf(sum - 2);
                carry = 1;
            }
            System.out.println("retStr: " + retStr);
            System.out.println("sum: " + sum);

            --loopTime;
            aFlag--;
            bFlag--;
        }
        return retStr;
    }
}

public class MainClass {
    public static String stringToString(String input) {
        if (input == null) {
            return "null";
        }
        return Json.value(input).toString();
    }

    public static void main(String[] args) throws IOException {
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        String line;
        while ((line = in.readLine()) != null) {
            String a = stringToString(line);
            line = in.readLine();
            String b = stringToString(line);

            String ret = new Solution().addBinary(a, b);

            String out = (ret);

            System.out.print(out);
        }
    }
}
```

输出
执行完成，耗时：N/A
a.length() = 10
10
9
"
java.lang.NumberFormatException: For input string: """
  at line 65, java.lang.NumberFormatException.forInputString
  at line 569, java.lang.Integer.parseInt
  at line 615, java.lang.Integer.parseInt
  at line 26, Solution.addBinary
  at line 113, MainClass.main


输入：
"1111"
"1"



## 参考链接
[一个学习网站](http://c.biancheng.net/sitemap/)

[Java获取字符串长度（length()）](http://c.biancheng.net/view/827.html)

[java中char类型转换成int类型的两种方法](https://www.cnblogs.com/daleyzou/p/9510334.html)

[java如何把char型数据转换成int型数据(转)](https://www.cnblogs.com/softidea/p/4158401.html)

[Java 中int、String的类型转换](https://www.cnblogs.com/bluestorm/p/3698810.html)

[Java反转字符串的10种方法（代码段）](http://www.importnew.com/30579.html)

[Java实现字符串反转](https://www.cnblogs.com/binye-typing/p/9260994.html)

[Java字符串处理](https://www.cnblogs.com/xujian2014/p/4437748.html)

[JAVA基础，字符串](https://www.cnblogs.com/fangzuchang/p/5911168.html)


## 知识延伸



end of this page
