

找出数组中重复的数字。

在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。


输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 

    解法一 额外数组空间 python3

class Solution:
    def findRepeatNumber(self, nums: List[int]) -> int:
        num_record = [0]*len(nums)
        for i in nums: 
            if num_record[i]==1:
                return i
            num_record[i]=1

    解法二 set解法 python3
class Solution:
    def findRepeatNumber(self, nums: List[int]) -> int:
        num_record = set()
        for i in nums:            
            temp = len(num_record)
            num_record =num_record|set([i])
            #print(num_record)
            if temp==len(num_record):
                return i


    解法三 鸽巢原理 python3 如果没有重复数字，那么正常排序后，数字i应该在下标为i的位置，所以思路是重头扫描数组，遇到下标为i的数字如果不是i的话，（假设为m),那么我们就拿与下标m的数字交换。在交换过程中，如果有重复的数字发生，那么终止返回ture

class Solution:
    def findRepeatNumber(self, nums: List[int]) -> int:
        for i in range(len(nums)):
            #print(nums)
            if nums[i]!=i:
                if nums[i] == nums[nums[i]]:
                    return nums[i]
                temp = nums[nums[i]]
                nums[nums[i]] = nums[i]
                nums[i] = temp
            

    解法四 python3 也可以用sort函数进行排序后，取相邻相同数返回
class Solution:
    def findRepeatNumber(self, nums: List[int]) -> int:
        nums = sorted(nums)
        for i in range(1,len(nums)):
            if nums[i-1] == nums[i]:
                return nums[i]
