## 两数之和

### 问题描述

给定一个整数数组 `nums` 和一个整数目标值 `target`，请你在该数组中找出 **和为目标值** *`target`* 的那 **两个** 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。

 

**示例 1：**

```
输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
```

**示例 2：**

```
输入：nums = [3,2,4], target = 6
输出：[1,2]
```

**示例 3：**

```
输入：nums = [3,3], target = 6
输出：[0,1]
```

### 解题

```java
public  int[] twoSum(int[] nums, int target) {
		 Map<Integer,Integer> map = new HashMap<>();
		 //遍历数组
		 for (int i = 0 ;i < nums.length;i++) {
			 //当前元素不满足条件时，将元素的值作为键，下标作为值存入map
			int a= nums[i];
			if(map.containsKey(target - a)) {
				//满足条件则返回结果
				return new int[] {map.get(target - a),i};
			}
			map.put(a , i );
		}
		 //没有符合条件的数时返回空数组
		 return new int[0];
	 }
```



### 思考

键重复问题：题目假定只有唯一解，那么重复键不为结果时没有影响；重复键为结果，如3+3=6（target）时，if判断会直接返回结果，因此数组元素即键重复不会影响结果
