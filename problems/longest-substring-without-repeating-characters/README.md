# Longest Substring Without Repeating Characters

## 🛠️ Problem Statement

Given a string s, find the length of the longest substring without duplicate characters.

## Example  

- Input: s = "abcabcbb"
- Output: 3
- Explanation: The answer is "abc", with the length of 3.

- Input: s = "bbbbb"
- Output: 1
- Explanation: The answer is "b", with the length of 1.

- Input: s = "pwwkew"
- Output: 3
- Explanation: The answer is "wke", with the length of 3. Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.

## Constraints

- 0 <= s.length <= 5 * 104
- s consists of English letters, digits, symbols and spaces.

## Implementation
```
public int lengthOfLongestSubstring(String s) 
{
    HashSet<Character> set = new HashSet<>();   // To store unique characters in the current window
    int MaxLength = 0;                          // Track the maximum length of unique substring
    int left = 0;                               // Left pointer for the sliding window

    for (int right = 0; right < s.length(); right++) // Iterate with the right pointer
    {   
        while (set.contains(s.charAt(right))) // If duplicate found, move the left pointer
        {          
            set.remove(s.charAt(left));                  // Remove the left character from the set
            left++;                                      // Shrink the window from the left
        }
        set.add(s.charAt(right));                        // Add the current character to the set
        MaxLength = Math.max(MaxLength, right - left + 1);  // Update max length
    }

    return MaxLength;                                   // Return the result
}
```

## Step-by-Step Explanation

- 🔥 ** Step 1: Initial Setup **
    - We start by initializing:
        - A HashSet<Character> → to store the unique characters in the current substring window.
        - MaxLength → keeps track of the maximum length of the substring with unique characters.
        - Two pointers:
            - left → marks the start of the current window.
            - right → iterates through the string (expanding the window).

- 🔥 ** Step 2: Iterate Through the String **
    - We use a for loop to iterate through the string using the right pointer:
        - for (int right = 0; right < s.length(); right++)
        - This loop moves the right pointer from 0 to the end of the string.
        - On each iteration:
            - The character at s.charAt(right) is considered.
            - We check if the current character is already in the set.
    
- 🔥 ** Step 3: Check for Duplicates **
    - The while loop handles repeated characters:
    - while (set.contains(s.charAt(right))) 
        {
            set.remove(s.charAt(left));   // Remove the leftmost character
            left++;                       // Move the left pointer
        }
    - If the character already exists in the set:
        - It means we have a repeating character.
        - We shrink the window by removing the leftmost character (s.charAt(left)) from the set.
        - We increment the left pointer by 1 to exclude the repeating character.
    - This continues until the window contains only unique characters.

- 🔥 ** Step 4: Expand the Window **
    - set.add(s.charAt(right));
    - After handling duplicates, we add the current character at s.charAt(right) to the set.
    - This expands the window, making it larger.

- 🔥 ** Step 5: Update the Maximum Length **
    - MaxLength = Math.max(MaxLength, right - left + 1);
    - We calculate the current length of the substring:
        - current length=right−left+1
    - We update MaxLength to store the maximum length so far.

- 🔥 ** Step 6: Return the Result **
    - return MaxLength;
    - After the loop finishes, we return the value of MaxLength, which contains the length of the longest substring without repeating characters.

## ✅ Example Walkthrough

Let's break it down with an example string:

Input: abcabcbb

Output: 3 → ("abc" is the longest substring without repeating characters)

### 💡 Step-by-Step Execution

Initial Setup:

- set = {} → HashSet to store unique characters.

- MaxLength = 0 → Keeps track of the longest substring length.

- left = 0 → Left pointer of the sliding window.

🔍 Iteration Walkthrough

![Screenshot 2025-03-27 183618](https://github.com/user-attachments/assets/48d8cc6e-d7c7-45c8-9896-226ed98ca248)

 Final Result:

 - The longest substring without repeating characters is "abc".
 - Output: 3

## Time and Space Complexity Analysis

✅ ** Time Complexity: O(n) **
- Each character is processed at most twice:
    - Once when expanding the window (right pointer).
    - Once when shrinking the window (left pointer).
- Hence, the time complexity is O(n).

✅ ** Space Complexity: O(min(n, m)) **
- n → length of the string.
- m → size of the character set (for ASCII: 256 or Unicode).
- The HashSet stores only unique characters, making the space complexity O(min(n, m)).

## 🔥 Edge Cases Covered

1️⃣ Empty String
```
Input: ""  
Output: 0  
```

2️⃣ Single Character
```
Input: "a"  
Output: 1   
```

3️⃣ All Unique Characters
```
Input: "abcdefg"  
Output: 7
```

4️⃣ All Repeating Characters
```
Input: "aaaaa"  
Output: 1  
```

5️⃣ Mixed Repeating and Unique Characters
```
Input: "pwwkew"  
Output: 3  // Longest substring: "wke"
```

6️⃣ Large Strings
- Handles large inputs efficiently with O(n) complexity.

7️⃣ Unicode Characters
- Works with Unicode strings as well.
