### Leetcode 978 湍流数组

当 A 的子数组 A[i], A[i+1], ..., A[j] 满足下列条件时，我们称其为湍流子数组：

若 i <= k < j，当 k 为奇数时， A[k] > A[k+1]，且当 k 为偶数时，A[k] < A[k+1]；
或 若 i <= k < j，当 k 为偶数时，A[k] > A[k+1] ，且当 k 为奇数时， A[k] < A[k+1]。
也就是说，如果比较符号在子数组中的每个相邻元素对之间翻转，则该子数组是湍流子数组。

#### 解题思路

考虑到问题的描述，因为只需要比较大小，所以可以把原本不确定的数组二进制化，并通过设置锚点来确定每一个湍流数组在数组中的位置，判断是否湍流数组结束是通过将一个数和左右数的关系相乘是否等于-1来确定。

返回 A 的最大湍流子数组的长度。

```java
class Solution {
    public int maxTurbulenceSize(int[] A) {
        int length = A.length;
        int anchor = 0;
        int ans = 0;
        for(int i = 1; i < length; i++){
            int c = Integer.compare(A[i-1], A[i]);
            if(i==length-1 || c * Integer.compare(A[i], A[i+1]) != -1){
                if(c!=0){
                    ans = Math.max(ans, i - anchor + 1);
                }
                anchor = i;
            }
        }
        return ans;
    }
}
```

