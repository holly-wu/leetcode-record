## No.005 最长回文子串
### Longest Palindromic Substring

* 给你一个字符串 s，找到 s 中最长的回文子串。

```
示例 1：
输入：s = "babad"
输出："bab"
解释："aba" 同样是符合题意的答案。
```  
```
示例 2：
输入：s = "cbbd"
输出："bb"
```  
```
示例 3：
输入：s = "a"
输出："a"
```  
```
示例 4：
输入：s = "ac"
输出："a"
```  

> 提示：  
> 1. 1 <= s.length <= 1000  
> 2. s 仅由数字和英文字母（大写和/或小写）组成

### 结果代码  1
*  运行时间：3 ms
*  内存消耗：39.9 MB

```
// 暴力算法，时间复杂度O(N^3)
public static void main(String[] args) {
    String result = longestPalindrome("ac");
    System.out.println(result);
}

public static String longestPalindrome(String s) {
    if (s.length() < 2) {
        return s;
    }

    char[] strArr = s.toCharArray();
    int maxLength = 1;
    int begin = 0;
    for (int i=0; i<strArr.length-1; i++) {
        for (int j=1; j<strArr.length; j++) {
            if (j - i + 1 > maxLength && checkPalindrome(strArr, i, j)) {
                maxLength = j - i + 1;
                begin = i;
            }
        }
    }
    return s.substring(begin, begin + maxLength);
}

public static boolean checkPalindrome(char[] param, int left, int right) {
    while (left < right) {
        if (param[left] != param[right]) {
            return false;
        }
        left ++;
        right --;
    }
    return true;
}
```

### 结果代码  2
*  运行时间：3 ms
*  内存消耗：39.7 MB
*  二分查找，第k个数字

```
// 二分查找，时间复杂度O(log(m+n))
public static void main(String[] args) {
        int[] nums1 = {2, 3, 5, 6};
        int[] nums2 = {1, 4};
        double result = findMedianSortedArrays(nums1, nums2);
        System.out.println(result);
    }

    public static double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int length1 = nums1.length;
        int length2 = nums2.length;
        int fullLength = length1 + length2;
        if (fullLength % 2 == 1) {
            int midIndex = fullLength / 2;
            double median = getKthElement(nums1, nums2, midIndex + 1);
            return median;
        } else {
            int midIndex1 = fullLength / 2 - 1, midIndex2 = fullLength / 2;
            double median = (getKthElement(nums1, nums2, midIndex1 + 1) + getKthElement(nums1, nums2, midIndex2 + 1)) / 2.0;
            return median;
        }
    }

    public static int getKthElement(int[] nums1, int[] nums2, int k) {
        int i = 0;
        int j = 0;
        while (true) {
            // 当k=1时先判断i或j是不是已经超过了数组索引
            if (i == nums1.length) {
                return nums2[j + k - 1];
            } else if (j == nums2.length) {
                return nums1[i + k - 1];
            }
            // 如果k=1，直接比较第一个数字的大小即可
            if (k == 1) {
                return Math.min(nums1[i], nums2[j]);
            }
            // position从1开始
            int position = k / 2;
            // 如果当前索引加上k超过了数组长度，那么将position定义为剩余的数组长度
            if (i + position > nums1.length || j + position > nums2.length) {
                position = Math.min(nums1.length - i, nums2.length - j);
            }
            // 对应position数字的索引，从0开始
            int m = i + position - 1;
            int n = j + position - 1;
            // 将数组索引定位到对应数字右边
            if (nums1[m] >= nums2[n]) {
                j = n + 1;
            } else {
                i = m + 1;
            }
            k = k - position;
        }
    }
```

### English  
* Given a string s, return the longest palindromic substring in s.

> Constraints:
> 1. 1 <= s.length <= 1000  
> 2. s consist of only digits and English letters (lower-case and/or upper-case)
