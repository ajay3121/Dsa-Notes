### Goal

Given a sorted array (`nums`) and a `target` value, return the index if the target is found. If not, return the index where it would be inserted in order.

### 🧠 Core Idea: The "Left" Pointer as the Answer

This problem is solved by using the **Standard Binary Search** structure and observing the final state of the pointers:

1. If the target is **found**, we return `mid`.
    
2. If the target is **not found**, the loop terminates when `left > right`. At this point, the **`left` pointer** always points to the correct insertion index (the **Ceiling**), as it stopped at the first position where `nums[left]` is greater than the `target`.
    

---

### 🛠️ Key Flow & Logic (Focus on Standard BS)

We use the standard `while (left <= right)` inclusive search. The logic is identical to a normal search, but we rely on the final state of the `left` pointer.

|**Condition**|**Action**|**Pointer Update (New Search Space)**|**Rationale**|
|---|---|---|---|
|`nums[mid] == target`|**Match!**|`return mid;`|Target found.|
|`nums[mid] < target`|Too small.|**Move Right:** `left = mid + 1;`|Discard `mid` and everything to its left. `left` moves past the largest element smaller than `target`.|
|`nums[mid] > target`|Too large.|**Move Left:** `right = mid - 1;`|Discard `mid` and everything to its right. `right` moves before the smallest element larger than `target`.|
|**Termination**|`left > right`|`return left;`|The search space collapsed. `left` is the index of the **first element $\ge$ target** (the insertion point/Ceiling).|

---

### ⏱️ Complexity

- **Time Complexity:** $O(\log N)$ (Standard binary search efficiency).
    
- **Space Complexity:** $O(1)$.
    

---

### 📝 Code Snippet (Standard Implementation)

Java

```
public int searchInsert(int[] nums, int target) {
    int left = 0;
    int right = nums.length - 1;

    // Use the standard inclusive search invariant: [left, right]
    while (left <= right) {
        // Safe midpoint calculation
        int mid = left + (right - left) / 2;

        if (nums[mid] == target) {
            return mid; // Target found
        } else if (nums[mid] < target) {
            // Target is larger, so we discard the left side
            left = mid + 1;
        } else {
            // Target is smaller, so we discard the right side
            right = mid - 1;
        }
    }

    // When the loop terminates (left > right), 
    // 'left' is the index where the target should be inserted.
    return left; 
}
```

---

### 🔗 Pattern Links (Obsidian Integration)

This problem is a specific case of the **Ceiling** pattern and uses the **Standard Binary Search** structure:
[[Binary Search]]