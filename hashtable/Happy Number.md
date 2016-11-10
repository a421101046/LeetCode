# Happy Number

#### 原题地址：[Happy Number ](https://leetcode.com/problems/happy-number/)

#### 要求：给定一个数判断其是不是幸运数

#### 例子:

```
数为19，最后结果为1，所以19为幸运数
1 ^ 2 + 9 ^2 = 82
8 ^ 2 + 2 ^ 2 = 68
6 ^ 2 + 8 ^ 2 = 100
1 ^ 2 + 0 ^ 2 + 0 ^ 2 = 1
```

***********



#### 解法一：

*    解题思路

     * 什么时候出现循环？ 假设是一个三位数，那么其各位平方求和不会超过三百。若每次的数字都不一样，则肯定会遍历到100，此时退出循环。所以导致循环的原因是数字重复。
     * 创建一个set集合保存每次的数字
     * 这里把每个数字计算完成之后，判断这个数字是否为幸运数，判断这个数字是否已在set集合中，若在集合中直接return false 即可

*    具体代码

               // 时间复杂度  不明
               // 空间复杂度  不明
               // 运行时间    4 ms
               // 排名        beats 66.35% of java submission
         
               @param 目标数
               @return 是否Happy Number
         
               public boolean isHappy(int n) {
                  if (n <= 0) return false;
                  // 存放已经出现过的数的集合
                  HashSet<Integer>  set = new HashSet<Integer>();
                  int sum = 0;   // 存放和
                  int pre = n;   // 存放之前的数
                  while (true) {
                    // 对数的每一个位求和
                    int dis = n % 10;
                    sum += (dis * dis);
                    n = (n - dis) / 10;
         
                    // 已对当前数完成求和
                    if (n <= 0) {
                        // 当sum为1时，说明是happy number
                        if (sum == 1) {
                            return true;
                        }
                        // 不为1，且set中已经包含该number，说明重复
                        if (set.contains(sum)) {
                            return false;
                        }else{
                            // 没有重复，继续遍历
                            set.add(pre);
                            pre = sum;
                            n = sum
                            sum = 0;
                        }
                     }
                   }
                 }


​              



#### 解法二：

- 解题思路

  - 利用解决链表重复的思路，来解决这个问题。
  - 定义两个索引A、B，让索引A先走一步。如果没有循环，那么索引A肯定会得到1。若有循环则 A与B总有一次会相等。

- 具体代码

                 // 时间复杂度  不明
                 // 空间复杂度  不明
                 // 运行时间    2 ms
                 // 排名        Your runtime beats 84.42% of java submissions.
                 // 参考：https://discuss.leetcode.com/topic/12587/my-solution-in-c-o-1-space-and-no-magic-math-property-involved/2
      
                 @param 目标数
                 @return 是否Happy Number
      
                public boolean isHappy1(int n) {
                    int index1 = n;
                    int index2 = n;
                    do {
                        index1 = this.nextNum(index1);
                        index2 = this.nextNum(index2);
                        index2 = this.nextNum(index2);
                    } while (index1 != index2);
      
                    if (index1 == 1) {
                        return true;
                    }else{
                        return false;			
                    }
                }
      
                @param 当前的数
                @return 返回下一个数
      
                public int nextNum(int curNum){
                    int sum = 0;
                    while(curNum > 0){
                        int remain = curNum % 10;
                        sum += remain * remain;
                        curNum = curNum / 10;
                    }
                    return sum;
                }
  ​

