# Day 1: Arrays, Strings, and Two Pointers
Objective: Master array manipulation and two-pointer techniques.

---

### **1️⃣ Sliding Window: Longest Substring Without Repeating Characters (LeetCode #3)**  
**Concept**: Maintain a window of non-repeating characters and slide it dynamically.  
🔹 **Key Idea**: Use a HashMap to store characters and their last seen positions.  

💡 **Approach**:
- Use a left and right pointer.
- Expand `right` while adding characters to a HashMap.
- If a character repeats, shrink from `left` until it's unique again.
- Keep track of the max length.

**Code (Python)**
```python
def lengthOfLongestSubstring(s):
    char_map = {}
    left = max_length = 0

    for right in range(len(s)):
        if s[right] in char_map:
            left = max(left, char_map[s[right]] + 1)
        char_map[s[right]] = right
        max_length = max(max_length, right - left + 1)
    
    return max_length
```

---

### **2️⃣ Two Pointers: 3Sum (LeetCode #15)**  
**Concept**: Sort the array and use two pointers to find triplets summing to zero.  
🔹 **Key Idea**: Convert `O(n³)` brute-force to `O(n²)` by using sorting and two-pointer strategy.  

💡 **Approach**:
- Sort the array.
- Fix one element, then use two pointers to find the other two numbers.
- Move pointers based on the sum.

**Code (Python)**
```python
def threeSum(nums):
    nums.sort()
    res = []

    for i in range(len(nums) - 2):
        if i > 0 and nums[i] == nums[i - 1]:  # Skip duplicates
            continue
        left, right = i + 1, len(nums) - 1
        while left < right:
            total = nums[i] + nums[left] + nums[right]
            if total == 0:
                res.append([nums[i], nums[left], nums[right]])
                left += 1
                right -= 1
                while left < right and nums[left] == nums[left - 1]:  # Skip duplicates
                    left += 1
                while left < right and nums[right] == nums[right + 1]:  # Skip duplicates
                    right -= 1
            elif total < 0:
                left += 1
            else:
                right -= 1
                
    return res
```

---

### **3️⃣ Prefix Sum: Subarray Sum Equals K (LeetCode #560)**  
**Concept**: Use a HashMap to store prefix sums and find subarrays that sum to `k`.  
🔹 **Key Idea**: Instead of brute-force `O(n²)`, use prefix sum to get `O(n)` efficiency.  

💡 **Approach**:
- Maintain a running sum.
- Check how many times `running_sum - k` has appeared before in a HashMap.
- Store occurrences of running sums.

**Code (Python)**
```python
def subarraySum(nums, k):
    prefix_sum = {0: 1}  # Store sum frequencies
    running_sum = count = 0

    for num in nums:
        running_sum += num
        count += prefix_sum.get(running_sum - k, 0)
        prefix_sum[running_sum] = prefix_sum.get(running_sum, 0) + 1
    
    return count
```

---

### **4️⃣ Two Pointers: Container With Most Water (LeetCode #11)**  
**Concept**: Use two pointers to maximize area.  
🔹 **Key Idea**: Instead of brute-force `O(n²)`, shrink the side with the smaller height in `O(n)`.  

💡 **Approach**:
- Use two pointers at both ends.
- Calculate the area at each step.
- Move the pointer with the smaller height.

**Code (Python)**
```python
def maxArea(height):
    left, right = 0, len(height) - 1
    max_water = 0

    while left < right:
        max_water = max(max_water, (right - left) * min(height[left], height[right]))
        if height[left] < height[right]:
            left += 1
        else:
            right -= 1
            
    return max_water
```

---

### **💡 Tricks Recap**
✅ **Sliding Window** → Use HashMaps to track seen characters.  
✅ **Two Pointers** → Efficient in sorted arrays for `O(n²)` optimizations.  
✅ **Prefix Sum** → HashMap helps store and retrieve sums efficiently.  

---

🔥 **Next Steps**:  
- Implement these in C# or any other language you're practicing.  
- Try similar problems like "Minimum Window Substring" (Sliding Window) or "Two Sum II" (Two Pointers).  
- Time yourself solving them to build speed.  

Let me know if you want variations or explanations for edge cases! 🚀
