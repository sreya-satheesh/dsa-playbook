# Two Sum 

## Problem  
Given an array nums and an integer target, return indices of the two numbers such that they add up to target.

- Each input has exactly one solution.
- You may not use the same element twice.
- The answer can be returned in any order.

## Example  

Input: nums = [2,7,11,15], target = 9
Output: [0,1]

Input: nums = [3,2,4], target = 6
Output: [1,2]

Input: nums = [3,3], target = 6
Output: [0,1]

## Constraints

- 2 <= nums.length <= 10^4
- -10^9 <= nums[i] <= 10^9
- -10^9 <= target <= 10^9

Only one valid answer exists.


## Approaches

### 1️⃣ Brute Force (O(n²))

- Iterate through every possible pair of numbers and check if their sum equals target.
- Time Complexity: O(n²) (Nested loop)
- Space Complexity: O(1) (No extra space used)

#### Implementation
`
def two_sum_brute_force(nums, target):
    for i in range(len(nums)):
        for j in range(i + 1, len(nums)):
            if nums[i] + nums[j] == target:
                return [i, j]
    return []
`
#### 💡 Why is this inefficient?

It checks all possible pairs, making it slow for large inputs.


### 2️⃣ Hash Map (O(n)) - Optimal Solution

- Use a hash map (dictionary) to store previously seen numbers and their indices.
- Time Complexity: O(n) (Single pass)
- Space Complexity: O(n) (Hash map storage)

#### Implementation
`
def two_sum_hashmap(nums, target):
    num_map = {}  # Stores number and its index
    for i, num in enumerate(nums):
        complement = target - num
        if complement in num_map:
            return [num_map[complement], i]
        num_map[num] = i
    return []
`
#### 💡 Why is this efficient?

It finds the solution in a single pass instead of checking all pairs.


### 3️⃣ Two Pointers (O(n log n)) – If Sorted

- First, sort the array while keeping track of original indices.
- Use the two-pointer technique:
  - Start with one pointer at the beginning and one at the end.
  - Move pointers based on the sum.
- Time Complexity: O(n log n) (Sorting) + O(n) (Two-pointer search) = O(n log n)
- Space Complexity: O(n) (Sorting may require extra space)

#### Implementation
`
def two_sum_two_pointers(nums, target):
    nums_with_indices = [(num, i) for i, num in enumerate(nums)]
    nums_with_indices.sort()  # Sorting based on values
    left, right = 0, len(nums) - 1

    while left < right:
        curr_sum = nums_with_indices[left][0] + nums_with_indices[right][0]
        if curr_sum == target:
            return [nums_with_indices[left][1], nums_with_indices[right][1]]
        elif curr_sum < target:
            left += 1
        else:
            right -= 1
    return []
`
#### 💡 When should you use this?

If the array is already sorted or can be sorted without extra space concerns.

## 🚀 Best Approach

The hash map approach (O(n)) is the most efficient because:

✅ It finds the solution in a single pass.
✅ It uses a dictionary for quick lookups instead of checking all pairs.
✅ It has the best balance of time and space complexity.
