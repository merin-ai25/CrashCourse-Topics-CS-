### **Day 2: Binary Search and Sorting**

**Patterns to Focus On:**

**1.Binary Search (Iterative/Recursive)**
   - **Binary search** works efficiently on **sorted** arrays by repeatedly halving the search space.
   - **Iterative**: Uses `while (low <= high)`, ensuring all cases are checked.
   - **Recursive**: Reduces the problem size through function calls.

**1.Search in Rotated Sorted Array (LeetCode #33) → Modified Binary Search**
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

**2.Modified Binary Search (Rotated Arrays, Peaks)**
   - Used when the array is **not fully sorted**, but has a special property (e.g., rotated, mountain array).
   - Adjusts **binary search logic** to handle these modifications.

**2.Find First and Last Position of Element in Sorted Array (LeetCode #34) → Binary Search**
   - **Problem**: Find the **first** and **last** occurrence of a target in a **sorted array**.
   - **Approach**:
     - Use **binary search twice**:
       1. To find the **leftmost position**.
       2. To find the **rightmost position**.

```csharp
public int[] SearchRange(int[] nums, int target) {
    return new int[] { FindBound(nums, target, true), FindBound(nums, target, false) };
}

private int FindBound(int[] nums, int target, bool isFirst) {
    int left = 0, right = nums.Length - 1, res = -1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) {
            res = mid;
            if (isFirst) right = mid - 1; // Search left side
            else left = mid + 1;  // Search right side
        } else if (nums[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return res;
}
```

---

**3.Sorting + Greedy**
   - **Sorting** simplifies decision-making in **greedy algorithms**.
   - Helps in problems like **merging intervals**, **minimizing/maximizing results**, or **partitioning elements** efficiently.
     
**3.Merge Intervals (LeetCode #56) → Sorting + Greedy**
   - **Problem**: Given a list of intervals, merge all overlapping ones.
   - **Approach**:
     - **Sort** intervals based on **start time**.
     - **Iterate and merge** overlapping intervals.

**C# Implementation:**
```csharp
public int[][] Merge(int[][] intervals) {
    if (intervals.Length == 0) return intervals;

    // Sort by start time
    Array.Sort(intervals, (a, b) => a[0] - b[0]);
    var result = new List<int[]>();

    foreach (var interval in intervals) {
        if (result.Count == 0 || result[^1][1] < interval[0]) {
            result.Add(interval);
        } else {
            result[^1][1] = Math.Max(result[^1][1], interval[1]); // Merge
        }
    }
    return result.ToArray();
}
```

---

**4.Kth Largest Element in an Array (LeetCode #215) → Quickselect or Heap**
   - **Problem**: Find the **kth largest** element in an **unsorted** array.
   - **Approach**:
     - **Quickselect Algorithm**: Similar to quicksort, but only partitions the array where needed.
     - **Heap Approach**: Uses a **Min-Heap** to maintain the `k` largest elements.

**Quickselect Approach (O(n) on average):**
```csharp
public int FindKthLargest(int[] nums, int k) {
    return QuickSelect(nums, 0, nums.Length - 1, nums.Length - k);
}

private int QuickSelect(int[] nums, int left, int right, int k) {
    if (left == right) return nums[left];

    int pivotIndex = Partition(nums, left, right);
    if (pivotIndex == k) return nums[pivotIndex];
    else if (pivotIndex < k) return QuickSelect(nums, pivotIndex + 1, right, k);
    else return QuickSelect(nums, left, pivotIndex - 1, k);
}

private int Partition(int[] nums, int left, int right) {
    int pivot = nums[right], i = left;
    for (int j = left; j < right; j++) {
        if (nums[j] <= pivot) {
            (nums[i], nums[j]) = (nums[j], nums[i]);
            i++;
        }
    }
    (nums[i], nums[right]) = (nums[right], nums[i]);
    return i;
}
```

---
**Tricks to Learn:**
**Edge Cases Matter!**  
   - **Empty arrays**  
   - **Arrays with one element**  
   - **Duplicates**  
   - **All elements are the same**  

**Binary Search Rule: `while (low <= high)`**  
   - **Avoid infinite loops** by always checking `low <= high`.
   - **For first occurrence**, move `right = mid - 1`.
   - **For last occurrence**, move `left = mid + 1`.

**Sorting Before Greedy**  
   - Sorting simplifies greedy approaches like **merging intervals**.
   - Helps with problems involving **overlapping** or **partitioning**.
