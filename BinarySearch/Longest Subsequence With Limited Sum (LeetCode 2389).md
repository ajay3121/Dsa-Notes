### Goal

For a given array of numbers (`nums`) and a list of maximum sums (`queries`), find the **maximum length** of a subsequence from `nums` whose sum is less than or equal to each query limit.

### 🧠 Core Idea: Transform to Prefix Sum & Binary Search

The key insight to solving this problem efficiently is realizing two things:

1. **Longest Subsequence:** To maximize length for a given sum, you must choose the **smallest possible numbers** first. This means we must **sort `nums`** in non-decreasing order.
    
2. **Efficient Querying:** Once sorted, the length of the longest subsequence is equivalent to finding the largest index `i` such that the **prefix sum** up to that index (i.e., `P[i]`) is less than or equal to the query limit. This search can be performed quickly using **Binary Search**.
    

---

### 🛠️ Step-by-Step Flow

1. **Sort `nums`:** Sort the input array `nums` to ensure we are always picking the smallest elements first.
    
2. **Calculate Prefix Sums:** Create a prefix sum array, $P$, where $P[i]$ is the sum of the first $i+1$ elements of the sorted `nums`. This allows $O(1)$ calculation of any contiguous sum starting from index 0.
    
3. **Process Queries:** For each query $Q$, use Binary Search on the **Prefix Sum array ($P$)** to find the last index `i` such that $P[i] \le Q$.
    
4. **Result:** The answer for query $Q$ is the length $i+1$.
    

---

### 📝 Implementation Details

We use a modified Binary Search (similar to finding the "Floor" or insertion point) to find the correct index in the prefix sum array.

#### Example: Find Insertion Point

If `Prefix Sums` = `[2, 3, 7, 10, 15]` and `Query` = `8`:

- Standard binary search might stop at 7 (index 2).
    
- The length is $2+1 = 3$.
    

The simplest way is to use a language's built-in **upper bound** or **`Arrays.binarySearch`** equivalent, or the **Ceiling logic** from our previous note (modified).

#### Code Snippet (Java)

Java

```
import java.util.Arrays;

class Solution {
    public int[] answerQueries(int[] nums, int[] queries) {
        // Step 1: Sort nums to ensure we take the smallest elements first.
        Arrays.sort(nums); 

        int n = nums.length;
        // Step 2: Calculate the Prefix Sums
        long[] prefixSum = new long[n];
        prefixSum[0] = nums[0];
        for (int i = 1; i < n; i++) {
            prefixSum[i] = prefixSum[i - 1] + nums[i];
        }

        int m = queries.length;
        int[] results = new int[m];

        // Step 3: Process Queries using Binary Search
        for (int i = 0; i < m; i++) {
            int target = queries[i];
            
            // Find the index of the largest element <= target in the prefixSum array.
            // Using a helper function (or built-in Arrays.binarySearch)
            int index = findMaxIndexLessThanOrEqualToTarget(prefixSum, target);

            // Step 4: The length is index + 1. If index is -1, length is 0.
            results[i] = (index == -1) ? 0 : index + 1;
        }

        return results;
    }

    // Helper function using Binary Search to find the rightmost insertion point (Floor)
    private int findMaxIndexLessThanOrEqualToTarget(long[] prefixSum, int target) {
        int left = 0;
        int right = prefixSum.length - 1;
        int maxIndex = -1; // Stores the index of the longest valid subsequence

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (prefixSum[mid] <= target) {
                // Potential answer found. Record it and try to find a longer subsequence (on the right)
                maxIndex = mid;
                left = mid + 1; // Expand right
            } else {
                // Current prefix sum is too large, discard the right side.
                right = mid - 1; // Contract left
            }
        }
        return maxIndex;
    }
}
```

---

### ⏱️ Complexity

- **Time Complexity:**
    
    - Sorting: $O(N \log N)$
        
    - Prefix Sums: $O(N)$
        
    - Queries (Binary Search): $O(M \log N)$
        
    - **Total:** $O(N \log N + M \log N)$
        
- **Space Complexity:** $O(N)$ for the prefix sum array and $O(M)$ for the results array.
    

---

### 🔗 Pattern Links
[[Binary Search]]