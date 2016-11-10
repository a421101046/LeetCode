## Intersection of Two Arrays

#### 原题地址：[Intersection of Two Arrays](https://leetcode.com/problems/intersection-of-two-arrays/)

#### 要求：求两个数组的交集，返回交集的数组。数组中的元素只能出现一次，数组可以以任意的次序

#### 例子:

```
nums1 = [1, 2, 2, 1], nums2 = [2, 2]
return [2]
```

***********



#### 解法一：

*    解题思路

     * 参考了归并排序中归并的思路，利用两个索引A，B分别指向两个数组的头部。当A所指向的小于B，说明A不是交集则A++。当B指向的小于A，同理。
     * 当A所指向的 == B，要分四种情况讨论。如下图，当符合这四种情况的时候要新数组中记录一下。

*    具体代码

                        // 时间复杂度  nlogn
                        // 空间复杂度  n
                        // 运行时间    3 ms
                        // 排名        beats 98.35% of java submissions O(∩_∩)O~
                        
                         public int[] intersection(int[] nums1, int[] nums2) {
               
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
                                      if (start1 == 0 && start2 == 0) { // 当双方的数字都是第一个 
                                      result[this.count]  = nums1[start1];
                                      this.count++;
                                  }
                                  }else if (start1 > 0 && start2 > 0) { // 对双方都不是第一个
                                  if ( nums1[start1 - 1] != nums1[start1] && nums2[start2 - 1]  
                                      !=nums2[start2]) {
                                          result[this.count]  = nums1[start1];
                                          this.count++;
                                  }
                                  }else if(start1 == 0){ // start1 是第一个
                                  if (nums2[start2 - 1] !=nums2[start2]) {
                                          result[this.count]  = nums1[start1];
                                          this.count++;
                                  }
                                 }else{ // start2是第一个
                                      if ( nums1[start1 - 1] !=nums1[start1]) {
                                      result[this.count]  = nums1[start1];
                                      this.count++;
                                       }
                                  }
                                 start1++;
                                 start2++;
                             }
                         }          


​                    

