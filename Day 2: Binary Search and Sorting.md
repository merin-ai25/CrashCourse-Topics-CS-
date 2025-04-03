### **Day 2: Binary Search and Sorting**

**1.Binary Search (Iterative/Recursive)**
   - **Binary search** works efficiently on **sorted** arrays by repeatedly halving the search space.
   - **Iterative**: Uses `while (low <= high)`, ensuring all cases are checked.
   - **Recursive**: Reduces the problem size through function calls.

**.Search in Rotated Sorted Array (LeetCode #33) → Modified Binary Search**
   - **Problem**: Given a rotated sorted array, find a target element in **O(log n)** time.
   - **Approach**:
     - Identify which half is **sorted**.
     - Use **binary search** accordingly.

```csharp
public int Search(int[] nums, int target) {
    int left = 0, right = nums.Length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) return mid;

        // Identify the sorted half
        if (nums[left] <= nums[mid]) {
            if (target >= nums[left] && target < nums[mid])
                right = mid - 1;
            else
                left = mid + 1;
        } else {
            if (target > nums[mid] && target <= nums[right])
                left = mid + 1;
            else
                right = mid - 1;
        }
    }
    return -1;
}
```

---
