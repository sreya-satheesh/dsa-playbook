# Two Sum 

## 🛠️ Problem Statement
Given an array nums and an integer target, return indices of the two numbers such that they add up to target.

- Each input has exactly one solution.
- You may not use the same element twice.
- The answer can be returned in any order.

## Example  

- Input: nums = [2,7,11,15], target = 9
- Output: [0,1]

- Input: nums = [3,2,4], target = 6
- Output: [1,2]

- Input: nums = [3,3], target = 6
- Output: [0,1]

## Constraints

- 2 <= nums.length <= 10^4
- -10^9 <= nums[i] <= 10^9
- -10^9 <= target <= 10^9

Only one valid answer exists.

## ✅ Solution: Hash Map (O(n)) – Optimal Solution

### 💡 Approach

- Use a HashMap to store previously seen numbers and their indices.
- For each number in the array:
    - Compute its complement → complement = target - nums[i]
    - Check if the complement is already in the hash map:
        - ✅ If yes → Return the indices of the complement and the current number.
        - ❌ If no → Store the current number and its index in the hash map.
- Time Complexity: O(n) → Single pass through the array.
- Space Complexity: O(n) → To store the hash map.

### 🔥 Implementation

```
public static int[] twoSum(int[] nums, int target)
{
    HashMap<Integer, Integer> numMap = new HashMap<>();

    for (int i = 0; i < nums.length; i++)
    {
        int complement = target - nums[i];
        if (numMap.containsKey(complement))
        {
            return new int[]{numMap.get(complement), i};
        }
        numMap.put(nums[i], i);
    }
    return new int[]{};
}
```

### ✅ Step-by-Step Execution
**Input**: nums = [2, 7, 11, 15], target = 9

**Goal**: Find two indices where the numbers add up to the target.

#### 🛠️ Initial Setup
- nums = [2, 7, 11, 15]
- target = 9
- numMap = {} → Empty hash map

#### 🔥 Iteration 1
- Current number: 2
- Complement: 9 - 2 = 7
- Check hash map:
    - numMap does NOT contain 7
- Store current number in map:
    - numMap = {2 → 0}
- Move to the next iteration

#### 🔥 Iteration 2
- Current number: 7
- Complement: 9 - 7 = 2
- Check hash map:
    - numMap contains 2
- Return the result:
    - return [numMap.get(2), 1] → [0, 1]
- Output: [0, 1]

#### 🔥 Final Hash Map State
numMap = { 2 → 0, 7 → 1}

### ✅ Why is this approach optimal?

**Time Complexity**: O(n) - Single pass through the array.
**Space Complexity**: O(n) Uses a hash map to store previously seen elements.
**Efficient Lookup**: HashMap provides O(1) average time complexity for lookups, making it faster than the brute-force solution.

## 🚦 Other Approaches

**Brute Force (O(n²))**
- Use nested loops to check all pairs.
- Time Complexity: O(n^2) → Inefficient for large inputs.
- Space Complexity: O(1) → No extra space used.
- Why avoid this? Slow for larger datasets due to nested loops.

**Two Pointers (O(n log n))**
- Sort the array and use two pointers.
- Time Complexity: O(n log n)
- Space Complexity: O(n) → To store original indices.
- When to use? If the array is already sorted.

