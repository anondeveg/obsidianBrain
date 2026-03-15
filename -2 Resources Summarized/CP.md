---
tags:
  - Resources_Summarized
---



[Duplicate emails (leet)](https://leetcode.com/problems/duplicate-emails/submissions/1850430207/)

```MYSQL
select Email from Person

GROUP BY Email

HAVING count(email) > 1
```
using count to remove duplicates


[two sum (leet)](https://leetcode.com/problems/two-sum/submissions/1851513552/)
```cpp
class Solution {
public:
	vector<int> twoSum(vector<int>& nums, int target) {
		for(int i = 0; i < nums.size(); i++){
			for(int j=1; j < nums.size(); j++){
				if ((nums[i] + nums[j]) == target && i != j){
						return {i,j};}
			}
		}
		return {};}};
```

**Nested loops are _mostly_ O(n^2)**

[Second Highest Salary](https://leetcode.com/submissions/detail/1851502903/)
```mysql
SELECT MAX(salary) AS SecondHighestSalary FROM Employee

WHERE salary < (SELECT MAX(salary) FROM Employee)
```
nice trick something like recursion.

