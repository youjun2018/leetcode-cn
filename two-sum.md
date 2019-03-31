# 两数之和

## 题目描述

原题链接：[两数之和](https://leetcode-cn.com/problems/two-sum/)

给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

示例:

给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]


## 解题思路
1. 创建一个 map，将来 map 中的 key 为数组中的值，value 为数组中值对应的位置。
2. 遍历数组，让 target 与数组当前的差值为 complement，如果 map 中的 key 含有 complement，则返回 complement 对应的 value 值，以及当前数组中值得位置。
3. 如果 map 中的 key 不包含 complement，则把 当前数组中值以及对应的位置放入到 map 中。重复步骤 2。


## 实现代码

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int i=0; i<nums.length; ++i){
            int complement = target-nums[i];
            if(map.containsKey(complement)){
                return new int[] {map.get(complement),i};
            }
            map.put(nums[i],i);
            
        }
        throw new IllegalArgumentException("No two Sum solution");
    }
}
```


## 总结归纳

拿到这个题目首先想到的是使用双重循环来做，但这样做的时间复杂度将达到 O(n^2)。使用 map 保存遍历过得元素，其查找时间复杂度为 O(1)。这样总的时间复杂度接近O(n)。

## 参考链接

[Java 集合系列10之 HashMap详细介绍(源码解析)和使用示例](https://www.cnblogs.com/skywang12345/p/3310835.html)
