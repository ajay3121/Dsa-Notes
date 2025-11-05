### Goal

Find the index of `target` in a sorted array that has been arbitrarily rotated. Time Complexity must be $O(\log N)$.

### 🧠 Core Idea: Identify the Sorted Half

The key is that in any iteration of binary search, at least one half of the array (either `[left, mid]` or `[mid, right]`) **must be sorted**. By checking the sorted state, we can determine two things:

1. Is the **target** within the range of the sorted half?
    
2. If not, the target must be in the **unsorted half**, which is the new, smaller subproblem.
    

---

### 🛠️ Key Flow & Logic

We use the standard $\mathbf{while (left \le right)}$ inclusive search invariant.

|**Step**|**Condition & Analysis**|**Action**|
|---|---|---|
|**Check Match**|If $\mathbf{nums[mid] == target}$|`return mid;`|
|**Identify Sorted Half**|$\mathbf{nums[left] \le nums[mid]}$ (Left Half is Sorted)|**Check Target in Left:** If $nums[left] \le target < nums[mid]$|
|||**Else (Target not in Left):**|
|**Identify Sorted Half**|$\mathbf{nums[left] > nums[mid]}$ (Right Half is Sorted)|**Check Target in Right:** If $nums[mid] < target \le nums[right]$|
|||**Else (Target not in Right):**|

---

### ⏱️ Complexity

- **Time Complexity:** $O(\log N)$ (Search space is halved in every iteration).
    
- **Space Complexity:** $O(1)$.
    

---

### 📝 Code Snippet (SDE 2 Standard)

Java

```
public int search(int[] nums, int target) {
    int left = 0;
    int right = nums.length - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2; // Safe midpoint

        if (nums[mid] == target) {
            return mid;
        }

        // 1. Check if the LEFT side is sorted: nums[left] <= nums[mid]
        if (nums[left] <= nums[mid]) {
            
            // Case A: Target is in the left (sorted) half
            if (nums[left] <= target && target < nums[mid]) {
                right = mid - 1;
            } 
            // Case B: Target is in the right (unsorted) half
            else {
                left = mid + 1;
            }
        } 
        
        // 2. Otherwise, the RIGHT side MUST be sorted: nums[left] > nums[mid]
        else {
            
            // Case C: Target is in the right (sorted) half
            if (nums[mid] < target && target <= nums[right]) {
                left = mid + 1;
            } 
            // Case D: Target is in the left (unsorted) half
            else {
                right = mid - 1;
            }
        }
    }

    return -1; // Target not found
}
```

---

### 🔗 Pattern Links (Obsidian Integration)
[[Binary Search]]