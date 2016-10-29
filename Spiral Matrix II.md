## Spiral Matrix II

#### 要求：给定一个整数n，返回一个n行n列的顺时针旋转的矩阵



#### 例子

```
给定二维数组
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]

返回 [1,2,3,6,9,8,7,4,5].
```

原题地址：[Spiral Matrix II](https://leetcode.com/problems/spiral-matrix-II/)

### 解题思路：

- 沿用之前Spiral Matrix遍历思路，只不过把打印数组元素改成打印数组元素的值

   

    

### 具体代码：

```
   //  Spiral Matrix  顺时针遍历数组
	public int[][] generateMatrix(int n) {
		// 当n < 1时，直接返回null
		if (n < 1) return new int[][]{};
		
		// 初始化数组
		int [][]matrix = new int[n][n];
		
		// 矩阵的高度
		int height = matrix.length;
		// 矩阵的宽度
		int width = height;
				
		// 遍历次数
		int count = Math.min(height, width);
		count = (count % 2 == 0) ? count / 2 : count / 2 + 1;
		
		int tmpCount = count;	
		while (count > 0) {
			int startX = tmpCount - count;
			int startY = tmpCount - count;
			int endX = width - startX - 1;
			int endY = height - startY - 1;
		
			addNumInRound(startX, startY, endX, endY, matrix);
			count--;
		}
		
		// 重置index
		this.index = 1;
		return matrix;
	}
	
	// 添加一圈矩阵的数字
	private void addNumInRound(int startX,int startY,int endX,int endY,int[][] matrix ){
		
		if(addSingleRowORCol(startX, startY, endX, endY, matrix)){
			return;
		}
		
		// 打印上面的部分
		for (int i = startX;i <= endX - 1; i++) {
			matrix[startY][i] = this.index++; 
		}
		
		// 打印右边的部分
		for (int j = startY; j <= endY - 1; j++) {
			matrix[j][endX] = this.index++;
		}
		
		// 打印下面的部分
		for (int i = endX; i >= startX + 1; i--) {
			matrix[endY][i] = this.index++;
		}
		
		// 打印左边的部分
		for (int j = endY;  j >= startY + 1 ; j--) {
			matrix[j][startX] = this.index++;
		}
	}	
	
	// 判断是否有出现 一行  或一列 ，有则添加返回true。  否则返回false
	private boolean addSingleRowORCol(int startX,int startY,int endX,int endY,int[][] matrix){
		boolean isOK = false;
		if (startY == endY) { // 一行
			isOK = true;
			for (int i = startX; i <= endX; i++) {
				matrix[startY][i] = this.index++;
			}
		}else if (startX == endX ) { // 一列
			if (isOK) return isOK;
			isOK = true;
			for (int i = startY; i <= endY; i++) {
				matrix[i][startX] = this.index++;
			}
		}
		return isOK;
	}
```



### 

   

