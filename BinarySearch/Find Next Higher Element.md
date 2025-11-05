## 📌 Obsidian Snippet: Find Next Higher Element (Ceiling)

### 🎯 Goal

Find the index of the **smallest element** in the sorted array that is **greater than** the `target`. If no such element exists (i.e., the target is greater than or equal to the largest element), return an indicator (e.g., `-1` or `nums.length`).

---

### 🧠 Core Idea: "Record and Contract Right"

This search uses the standard $O(\log N)$ binary search, but modifies the pointer logic:

1. We maintain a variable (`ceilingIndex`) to **record the best potential answer** found so far (an element $\ge$ target).
    
2. When `nums[mid]` is **greater than or equal** to the target, we record `mid` as a potential answer and then **contract the search space to the left** (`right = mid - 1`) to try and find an even smaller (and thus better) ceiling element.
    

---

### 🛠️ Key Flow & Logic

|**Condition**|**Action**|**Pointer Update (New Search Space)**|**Rationale**|
|---|---|---|---|
|`nums[mid] >= target`|**Potential Ceiling!**|**Record:** `ceilingIndex = mid;`<br><br>  <br><br>**Contract Left:** `right = mid - 1;`|Discard the right half to force the search for a _smaller_ element that still meets the ceiling condition.|
|`nums[mid] < target`|Too small.|**Move Right:** `left = mid + 1;`|Target must be in the right half.|
|**Termination**|When `left > right`|`return ceilingIndex;`|The search loop terminates, and `ceilingIndex` holds the index of the smallest element $\ge$ target.|

---

### ⏱️ Complexity

- **Time Complexity:** $O(\log N)$
    
- **Space Complexity:** $O(1)$
    

---

### 📝 Code Snippet (Ceiling Implementation)

Java

```
/**
 * Finds the index of the smallest element >= target.
 * Returns -1 if no such element exists (or nums.length if you prefer).
 */
public static int findCeiling(int[] nums, int target) {
    if (nums == null || nums.length == 0) {
        return -1;
    }
    
    int left = 0;
    int right = nums.length - 1;
    int ceilingIndex = -1; // Stores the index of the best potential answer

    while (left <= right) {
        // SDE 2 Standard: Safe midpoint
        int mid = left + (right - left) / 2;

        if (nums[mid] >= target) {
            // Potential Ceiling: Record the answer and try to find a smaller one on the left
            ceilingIndex = mid;
            right = mid - 1; // Contract left
        } else {
            // Element is too small, search the right half
            left = mid + 1; // Move right
        }
    }

    return ceilingIndex;
}
```

---

### 🔗 Pattern Links (Obsidian Integration)

This is a **variation** of the standard search:
    
- [[Binary Search]]