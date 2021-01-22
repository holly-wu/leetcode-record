## No.004 寻找两个正序数组的中位数
### Median of Two Sorted Arrays

* 给定两个大小为 m 和 n 的正序（从小到大）数组 nums1 和 nums2。请你找出并返回这两个正序数组的中位数。
* 进阶：你能设计一个时间复杂度为 O(log (m+n)) 的算法解决此问题吗？

```
示例 1：
输入：nums1 = [1,3], nums2 = [2]
输出：2.00000
解释：合并数组 = [1,2,3] ，中位数 2
```  
```
示例 2：
输入：nums1 = [1,2], nums2 = [3,4]
输出：2.50000
解释：合并数组 = [1,2,3,4] ，中位数 (2 + 3) / 2 = 2.5
```  
```
示例 3：
输入：nums1 = [0,0], nums2 = [0,0]
输出：0.00000
```  
```
示例 4：
输入：nums1 = [], nums2 = [1]
输出：1.00000
```  
```
示例 5：
输入：nums1 = [2], nums2 = []
输出：2.00000
```

> 提示：  
> 1. nums1.length == m  
> 2. nums2.length == n  
> 3. 0 <= m <= 1000  
> 4. 0 <= n <= 1000  
> 5. 1 <= m + n <= 2000  
> 6. -106 <= nums1[i], nums2[i] <= 106  

### 结果代码  1
*  运行时间：3 ms
*  内存消耗：39.9 MB
*  内存消耗略多，考虑更好方案

```
public static void main(String[] args) {
    int[] nums1 = {2};
    int[] nums2 = {1, 3};
    double result = findMedianSortedArrays(nums1, nums2);
    System.out.println(result);
}

public static double findMedianSortedArrays(int[] nums1, int[] nums2) {
    int i = 0;
    int j = 0;
    int fullLength = nums1.length + nums2.length;
    int centerPos = (fullLength + 1) / 2 - 1;
    int centerNum = 0;
    int centerRightNum = 0;
    Double result = 0d;
    while(i < nums1.length || j < nums2.length) {
        int pickNum = 0;
        if (i == nums1.length) {
            pickNum = nums2[j];
            j ++;
        }else if (j == nums2.length) {
            pickNum = nums1[i];
            i ++;
        } else if(nums1[i] > nums2[j]) {
            pickNum = nums2[j];
            j ++;
        } else if (nums1[i] <= nums2[j]) {
            pickNum = nums1[i];
            i ++;
        }

        int pos = i + j - 1;
        if (pos == centerPos) {
            centerNum = pickNum;
        } else if (pos == centerPos + 1) {
            centerRightNum = pickNum;
            break;
        }
    }
    // 偶数
    if (fullLength % 2 == 0) {
        result = (Double.valueOf(centerNum) + Double.valueOf(centerRightNum)) / 2;
    } else { // 奇数
        result = Double.valueOf(centerNum);
    }
    return result;
}
```

### English  
* Given two sorted arrays nums1 and nums2 of size m and n respectively, return the median of the two sorted arrays.
* Follow up: The overall run time complexity should be O(log (m+n)).

> Constraints:
> 1. nums1.length == m
> 2. nums2.length == n
> 3. 0 <= m <= 1000
> 4. 0 <= n <= 1000
> 5. 1 <= m + n <= 2000
> 6. -106 <= nums1[i], nums2[i] <= 106
