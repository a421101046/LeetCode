## 119. Pascal's Triangle II

#### 要求：给定一个行号，返回帕斯卡三角中对应的行

#### 例子

```
k = 3,
返回 [1,3,3,1].
```

原题地址：[Pascal's Triangle II](https://leetcode.com/problems/pascals-triangle-ii/)

### 解题思路：

- 相对上一题来说，不需要在记录每行的元素。只需要记录当前行和之前的行 

### 具体代码：

```
    public List<Integer> getRow(int numRows) {
		if (numRows < 0) return new ArrayList<>();
		
		List<Integer> pre = null;
		List<Integer> cur = null;


		for (int row = 0; row <= numRows; row++) {
			
			// 获取当前的行
			cur = new ArrayList<>(row + 1);
			for (int col = 0; col < row + 1; col++) {
				if (col == 0 || col == row) {
					cur.add(1);
				} else {
					cur.add(pre.get(col) + pre.get(col - 1));
				}
			}
			// 设置之前的行
			pre = cur;
			cur = null;
		}
		return pre;
	}
```



### 不清楚有没有更好的方法，未完待续。

   

