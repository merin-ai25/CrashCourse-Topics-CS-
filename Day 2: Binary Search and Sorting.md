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
using System;

class Program
{
    static void Main()
    {
        Console.Write("Enter the number of elements in the array: ");
        string input = Console.ReadLine(); // Store input in a variable

        if (int.TryParse(input, out int n) && n > 0)
        {
            int[] nums = new int[n];

            Console.WriteLine($"Enter {n} elements:");
            for (int i = 0; i < n; i++)
            {
                string elementInput = Console.ReadLine(); // Store input before checking
                while (!int.TryParse(elementInput, out nums[i]))
                {
                    Console.WriteLine("Invalid input. Please enter an integer:");
                    elementInput = Console.ReadLine(); // Get new input
                }
            }

            Console.Write("Enter the number you want to search for: ");
            string targetInput = Console.ReadLine(); // Store input before checking

            if (int.TryParse(targetInput, out int target))
            {
                int index = Search(nums, target);

                if (index != -1)
                    Console.WriteLine($"Number found at index {index}.");
                else
                    Console.WriteLine("Number not found.");
            }
            else
            {
                Console.WriteLine("Invalid input. Please enter a valid number.");
            }
        }
        else
        {
            Console.WriteLine("Invalid input. Please enter a positive integer for the array size.");
        }
    }

    static int Search(int[] nums, int target)
    {
        int left = 0, right = nums.Length - 1;

        while (left <= right)
        {
            int mid = left + (right - left) / 2;

            if (nums[mid] == target) return mid;

            if (nums[left] <= nums[mid])
            {
                if (target >= nums[left] && target < nums[mid])
                    right = mid - 1; // Search the left half
                else
                    left = mid + 1;  // Search the right half
            }
            else
            {
                if (target > nums[mid] && target <= nums[right])
                    left = mid + 1; // Search the right half
                else
                    right = mid - 1; // Search the left half
            }
        }

        return -1;
    }
}

```

---
