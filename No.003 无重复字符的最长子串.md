## No.003 无重复字符的最长子串
### Longest Substring Without Repeating Characters

* 给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。

```
示例 1：
输入: s = "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```  
```
示例 2：
输入: s = "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```  
```
示例 3：
输入: s = "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```  
```
示例 4：
输入: s = ""
输出: 0
```

> 提示：  
> 1. 0 <= s.length <= 5 * 104  
> 2. s 由英文字母、数字、符号和空格组成

### 结果代码  1  
*  运行时间：17 ms
*  内存消耗：39.5 MB
*  运行时间太久，需要修改，字符串的相加既耗费时间，也耗费空间

```
public static void main(String[] args) {
    int result = lengthOfLongestSubstring("a");
    System.out.println(result);
}

public static int lengthOfLongestSubstring(String s) {
    String temp = "";
    char[] strArr = s.toCharArray();
    int maxLength = 0;
    for (char c : strArr) {
        int cIndex = temp.indexOf(String.valueOf(c));
        if (cIndex >= 0) {
            maxLength = temp.length() > maxLength ? temp.length() :maxLength;
            temp = temp.substring(cIndex + 1);
        }
        temp = temp + c;
    }
    // 一个字符的字符串，maxLength需要另外判断
    maxLength = temp.length() > maxLength ? temp.length() :maxLength;
    return maxLength;
}
```
### 结果代码  2  
*  运行时间：7 ms
*  内存消耗：38.7 MB
*  移动窗口

```
public static void main(String[] args) {
    int result = lengthOfLongestSubstring("a");
    System.out.println(result);
}

public static int lengthOfLongestSubstring(String s) {
   if (s.length() == 0) {
        return 0;
    }
    char[] strArr = s.toCharArray();
    int left = 0; // 左窗口
    int right = 0; // 右窗口
    int maxLength = 0;
    Map<Character, Integer> posMap = new HashMap<>();
    for (int i=0; i<strArr.length; i++) {
        char temp = strArr[i];

        if (posMap.containsKey(temp)) {
            // 窗口只能往右移动
            left = posMap.get(temp) + 1 > left ? posMap.get(temp) + 1 : left;
        }
        posMap.put(temp, i);
        right = i;
        maxLength = right - left + 1 > maxLength ? right - left + 1 :maxLength;
    }
    return maxLength;
}
```

### English  
* Given a string s, find the length of the longest substring without repeating characters.

> Constraints:  
> 1. 0 <= s.length <= 5 * 104
> 2. s consists of English letters, digits, symbols and spaces.
