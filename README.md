### **Day 1: Arrays, Strings, and Two Pointers**

1. **Sliding Window:**
   - A sliding window is a technique where you maintain a window (a subset of elements) within an array or string, and adjust the window size dynamically.
   - It helps in optimizing problems where you need to check for subarrays or substrings meeting certain criteria.

2. **Two Pointers (Sorted Array Problems):**
   - The two-pointer technique is used to solve problems involving sorted arrays or lists, where one pointer moves from the start and the other from the end.
   - This technique helps solve problems like searching pairs or finding the maximum/minimum in certain conditions.

3. **Prefix Sum:**
   - A prefix sum array helps you calculate the sum of elements from index 0 to any index in constant time, which is useful in problems where you need subarrays’ sums.

---
1. **Longest Substring Without Repeating Characters (LeetCode #3) → Sliding Window**
   
   - **Problem**: Find the length of the longest substring without repeating characters.
   - **Approach**: Use a sliding window to keep track of the substring that contains no repeating characters. Use a hash map to store the last occurrence of each character.

   **C# Example:**
   ```csharp
   using System;
   using System.Collections.Generic;

   class Program
   {
    static int LengthOfLongestSubstring(string s)
    {
        var map = new Dictionary<char, int>();
        int start = 0, maxLength = 0;
        for (int end = 0; end < s.Length; end++)
        {
            if (map.ContainsKey(s[end]))
            {
                start = Math.Max(start, map[s[end]] + 1);
            }
            map[s[end]] = end;
            maxLength = Math.Max(maxLength, end - start + 1);
        }
        return maxLength;
    }
    static void Main()
    {
        Console.WriteLine("Enter a string to find the length of the longest substring without repeating characters:");
        string input = Console.ReadLine();
        int result = LengthOfLongestSubstring(input);
        Console.WriteLine($"Length of the longest substring without repeating characters: {result}");
    }
   }
   ```

2. **3Sum (LeetCode #15) → Two Pointers**
   
   - **Problem**: Find all unique triplets in an array that sum to zero.
   - **Approach**: Sort the array and then use two pointers to find pairs that sum up to the negative of the current element.

   **C# Example:**
   ```csharp
   public IList<IList<int>> ThreeSum(int[] nums) {
       var result = new List<IList<int>>();
       Array.Sort(nums);
       for (int i = 0; i < nums.Length - 2; i++) {
           if (i > 0 && nums[i] == nums[i - 1]) continue; // Skip duplicates
           int left = i + 1, right = nums.Length - 1;
           while (left < right) {
               int sum = nums[i] + nums[left] + nums[right];
               if (sum == 0) {
                   result.Add(new List<int> { nums[i], nums[left], nums[right] });
                   while (left < right && nums[left] == nums[left + 1]) left++;
                   while (left < right && nums[right] == nums[right - 1]) right--;
                   left++;
                   right--;
               } else if (sum < 0) {
                   left++;
               } else {
                   right--;
               }
           }
       }
       return result;
   }
   ```

3. **Subarray Sum Equals K (LeetCode #560) → Prefix Sum**
   
   - **Problem**: Find the total number of continuous subarrays whose sum equals to a given value `k`.
   - **Approach**: Use a prefix sum and a hash map to store the frequency of each prefix sum. This allows you to count the number of subarrays that sum to `k` efficiently.

   **C# Example:**
   ```csharp
   public int SubarraySum(int[] nums, int k) {
       var map = new Dictionary<int, int> { { 0, 1 } }; // Prefix sum to count
       int sum = 0, count = 0;
       foreach (var num in nums) {
           sum += num;
           if (map.ContainsKey(sum - k)) {
               count += map[sum - k];
           }
           if (!map.ContainsKey(sum)) {
               map[sum] = 0;
           }
           map[sum]++;
       }
       return count;
   }
   ```

4. **Container With Most Water (LeetCode #11) → Two Pointers**
   
   - **Problem**: Find the container with the most water by determining the area formed between two vertical lines.
   - **Approach**: Use two pointers: one at the beginning and one at the end of the array, and calculate the area. Move the pointer pointing to the shorter line inward, hoping to find a taller line that may form a larger area.

   **C# Example:**
   ```csharp
   public int MaxArea(int[] height) {
       int left = 0, right = height.Length - 1;
       int maxArea = 0;
       while (left < right) {
           int width = right - left;
           int currentArea = Math.Min(height[left], height[right]) * width;
           maxArea = Math.Max(maxArea, currentArea);
           if (height[left] < height[right]) {
               left++;
           } else {
               right--;
           }
       }
       return maxArea;
   }
   ```

---

### **Tricks to Learn:**

1. **Use Hash Maps for Quick Lookups**:
   - Hash maps provide constant-time complexity for lookups, making them ideal for problems that require frequent access to data, like checking if an element exists in a window or tracking prefix sums.

2. **Optimize Brute Force Solutions by Reducing Nested Loops**:
   - Instead of using multiple nested loops, try to reduce complexity by leveraging sliding windows, two pointers, or prefix sums. These techniques allow you to reduce the time complexity from `O(n^2)` to `O(n)` or `O(n log n)` in many cases.
