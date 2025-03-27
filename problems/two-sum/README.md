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


## ✅ Approaches

### 1️⃣ Brute Force (O(n²))

- Iterate through every possible pair of numbers and check if their sum equals target.
- Time Complexity: O(n²) (Nested loop)
- Space Complexity: O(1) (No extra space used)

#### Implementation
```
public static int[] twoSum(int[] nums, int target) 
{
    for (int i = 0; i < nums.length; i++) 
    {
        for (int j = i + 1; j < nums.length; j++) 
        {
            if (nums[i] + nums[j] == target) 
            {
                return new int[]{i, j};
            }
        }
    }
    return new int[]{};
}
```
#### 💡 Why is this inefficient?

It checks all possible pairs, making it slow for large inputs.


### 2️⃣ Hash Map (O(n)) - Optimal Solution

- Use a HashMap to store previously seen numbers and their indices.
- For each number:
    - Compute its complement: complement = target - num
    - Check if the complement is already in the hash map:
        - ✅ If yes → Return the indices.
        - ❌ If no → Store the current number and its index in the map.
- Time Complexity: O(n) → Single pass through the array.
- Space Complexity: O(n) → Hash map storage.

#### Implementation
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
#### 💡 Why is this efficient?

It finds the solution in one pass instead of checking all pairs.


### 3️⃣ Two Pointers (O(n log n)) – If Sorted

- First, sort the array while keeping track of the original indices.
- Use the two-pointer technique:
  - Start with one pointer at the beginning and one at the end.
  - Move pointers based on the sum.
    - 🔼 If the sum is too small → Move the left pointer.
    - 🔽 If the sum is too large → Move the right pointer.
- Time Complexity: O(n log n) → Sorting + O(n) two-pointer search = O(n log n)
- Space Complexity: O(n) → To store original indices

#### Implementation
```
public static int[] twoSum(int[] nums, int target) 
{
    int[][] numsWithIndices = new int[nums.length][2];

    for (int i = 0; i < nums.length; i++) 
    {
        numsWithIndices[i][0] = nums[i];
        numsWithIndices[i][1] = i;
    }

    Arrays.sort(numsWithIndices, (a, b) -> Integer.compare(a[0], b[0]));

    int left = 0, right = nums.length - 1;

    while (left < right) 
    {
        int sum = numsWithIndices[left][0] + numsWithIndices[right][0];

        if (sum == target) 
        {
            return new int[]{numsWithIndices[left][1], numsWithIndices[right][1]};
        } 
        else if (sum < target) 
        {
            left++;
        } 
        else
        {
            right--;
        }
    }
    return new int[]{};
}
```
#### 💡 When should you use this?

If the array is already sorted or can be sorted without extra space concerns..

## 🥇 Best Approach

The hash map approach (O(n)) is the most efficient because:

✅ It finds the solution in a single pass.

✅ Uses a dictionary for quick lookups.

✅ Balances time and space complexity optimally.
