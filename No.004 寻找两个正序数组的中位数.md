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
*  考虑O(log (m+n)) 的算法

```
// 数组长度固定，可以计算出中位数的最终位置，遍历两个数组，获取到对应位置的数字即可，时间复杂度O(m+n)
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
* Given two sorted arrays nums1 and nums2 of size m and n respectively, return the median of the two sorted arrays.
* Follow up: The overall run time complexity should be O(log (m+n)).

> Constraints:
> 1. nums1.length == m
> 2. nums2.length == n
> 3. 0 <= m <= 1000
> 4. 0 <= n <= 1000
> 5. 1 <= m + n <= 2000
> 6. -106 <= nums1[i], nums2[i] <= 106
