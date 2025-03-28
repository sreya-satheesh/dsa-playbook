# Capacity To Ship Packages Within D Days

## 🛠️ Problem Statement

Imagine you have a conveyor belt with several packages, each having a specific weight. You need to ship all the packages from one place to another within D days.

### ✅ Rules:

- The packages must be shipped in the given order.

- The ship has a maximum capacity it can carry each day.

- The goal is to find the minimum capacity required to ship all the packages within D days.

### 🛠️ Example

```
Input:  
weights = [3, 2, 2, 4, 1, 4]  
days = 3  

Output:  
6  
```

### 🚢 Explanation:

We need to ship all packages in 3 days with the smallest possible ship capacity.

We can split the shipment like this:

- Day 1: 3 + 2 → total = 5

- Day 2: 2 + 4 → total = 6

- Day 3: 1 + 4 → total = 5

✅ The minimum capacity to successfully ship in 3 days is 6.


## 🚀 Approach: Binary Search + Greedy Simulation

### 🔥 Why Binary Search?

If we try every possible capacity from the heaviest package to the sum of all weights, it would take too long. 

Instead, we use binary search to quickly find the smallest valid capacity.

#### ✅ Step 1: Define the Capacity Range

We need to determine the possible capacity range:

- Minimum Capacity (left) → The ship must carry at least the heaviest package.
    - left=max(weights)
- Maximum Capacity (right) → If the ship carries all packages in one day, its capacity must be the sum of all weights.
    - right=∑(weights)

- ⚙️ For the example:
    - weights = [3, 2, 2, 4, 1, 4]  
    - Minimum capacity → max(3, 2, 2, 4, 1, 4) = 4
    - Maximum capacity → 3 + 2 + 2 + 4 + 1 + 4 = 16
    - The capacity range → [4, 16]

#### ✅ Step 2: Binary Search for Minimum Capacity

We perform binary search on the capacity range to find the smallest capacity that ships all packages within D days.

##### 💡 How It Works:

- Pick the middle capacity → mid = (left + right) / 2
- Simulate the shipping process with this capacity:
    - Start adding packages until the total weight exceeds the capacity.
    - Once it does, start a new day.
    - Count how many days it takes.
- If it fits within D days → Try a smaller capacity (move right closer).
- If it takes more than D days → Increase the capacity (move left closer).

#### ✅ Step 3: Simulation Example

For the capacity range [4, 16]:

- Mid = 10
    - Check with capacity = 10:
        - Day 1 → 3 + 2 + 2 → 7 ✅
        - Day 2 → 4 + 1 + 4 → 9 ✅
        - ✅ Shipped in 2 days → Try smaller capacity → right = 10

- Mid = 7
    - Check with capacity = 7:
        - Day 1 → 3 + 2 → 5 ✅
        - Day 2 → 2 + 4 → 6 ✅
        - Day 3 → 1 + 4 → 5 ✅
        - ✅ Shipped in 3 days → Try smaller capacity → right = 7
    
- Mid = 5
    - Check with capacity = 5:
        - Day 1 → 3 + 2 → 5 ✅
        - Day 2 → 2 + 4 → 6 ❌ → New day
        - Day 3 → 4 → 4 ✅
        - Day 4 → 1 + 4 → 5 ✅
        - ❌ Too many days → Increase capacity → left = 6

- Mid = 6
    - Check with capacity = 6:
        - Day 1 → 3 + 2 → 5 ✅
        - Day 2 → 2 + 4 → 6 ✅
        - Day 3 → 1 + 4 → 5 ✅
        - ✅ Exactly 3 days → Try smaller capacity → right = 6

- ✅ Binary Search Ends
    - Since left == right, the minimum capacity required is 6.

## 🚀 Code Implementation

```
public int shipWithinDays(int[] weights, int days) 
{
    int left = 0, right = 0;

    // Step 1: Define capacity range
    for (int w : weights) 
    {
        left = Math.max(left, w);  // Lower bound = max weight
        right += w;                // Upper bound = sum of weights
    }

    // Step 2: Binary search for the minimum capacity
    while (left < right) 
    {
        int mid = left + (right - left) / 2;

        if (canShipInDays(weights, days, mid)) 
        {
            right = mid;   // Try smaller capacity
        } 
        else
        {
            left = mid + 1;  // Increase capacity
        }
    }
    return left;
}

// Helper method to check if given capacity works
private boolean canShipInDays(int[] weights, int days, int capacity) 
{
    int currentWeight = 0;
    int requiredDays = 1;

    for (int w : weights) 
    {
        if (currentWeight + w > capacity) 
        {
            requiredDays++;      // Start a new day
            currentWeight = w;   // Reset current day’s weight
            if (requiredDays > days) 
            {
                return false;    // Too many days needed
            }
        } 
        else 
        {
            currentWeight += w;  // Add package to current day
        }
    }
    return true;   // Fits within the given days
}
```

## ✅ Complexity Analysis

**Time Complexity**: O(N×log(∑(weights)−max(weights))) (N → length of the `weights` array)
**Space Complexity:**: O(1) (No extra space used)