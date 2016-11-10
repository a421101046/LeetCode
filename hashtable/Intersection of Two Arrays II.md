## Intersection of Two Arrays  II

#### 原题地址：[Intersection of Two Arrays  II](https://leetcode.com/problems/intersection-of-two-arrays-ii/)

#### 要求：求两个数组的交集，返回交集的数组。返回数组中但凡重复的元素均可以出现，数组可以以任意的次序

#### 例子:

```
nums1 = [1, 2, 2, 1], nums2 = [2, 2]
return [2,2]
```

***********



#### 解法二：

*    解题思路

     * 参考了归并排序中归并的思路，利用两个索引A，B分别指向两个数组的头部。当A所指向的小于B，说明A不是交集则A++。当B指向的小于A，同理。
     * 当A所指向的 == B， 新数组中记录一下，A++ B++

*    具体代码

                // 时间复杂度  nlogn
                // 空间复杂度  n
                // 运行时间    3 ms
                // 排名       beats 95.61% of java submissions  感觉一般但却击败这么多人。O(∩_∩)O~
            
                @param nums1 数组一
                @param nums2 数组二
                @return 返回重复的数组
                public int[] intersect(int[] nums1, int[] nums2) {
            		if (nums1.length + nums2.length <= 0) return new int[]{};
            		
            		// 先对两个数组进行升序
                    Arrays.sort(nums1);
                    Arrays.sort(nums2);
                    // 将两个数组中重复的元素，归并到result中
                    int []result = new int[nums1.length + nums2.length];
                    merge(nums1,nums2,result);
                    
                    // 将result中的元素copy到tmp数组
                    int[]tmp = new int[this.count];
                    for (int i = 0; i < this.count; i++) {
            			tmp[i] = result[i];
            		}
                    return tmp;
                }
                
                 对两个数组进行归并，得到重复的元素
                 @param nums1 数组一
                 @param nums2 数组二
                 public void merge(int []nums1,int []nums2,int []result){
                     int start1 = 0;
                     int end1 = nums1.length - 1;
                     int start2 = 0;
                     int end2 = nums2.length - 1;
         
                     while (start1 <= end1 && start2 <= end2) {
                         if (nums1[start1] < nums2[start2]) {
                             start1++;
                         }else if(nums1[start1] > nums2[start2]){
                             start2++;
                         }else{ // 当双方的数字相同
                             result[this.count++]  = nums1[start1++];
                             start2++;
                         }
                     }
                  }



