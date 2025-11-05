### Goal

Efficiently find the index of a `target` in a **sorted array**.

---

### 🧠 Core Idea: Invariant & Search Space

Use the **`[left, right]` inclusive** loop invariant (`while (left <= right)`). This guarantees the search space always includes the potential answer, even if the space is reduced to a single element.

---

### 🛠️ Key Flow & Logic

|**Condition**|**Action**|**Pointer Update (New Search Space)**|**Rationale**|
|---|---|---|---|
|`nums[mid] == target`|**Match!**|`return mid;`|Target found.|
|`nums[mid] < target`|Target is larger.|**Move Right:** `left = mid + 1;`|Discard `mid` and everything to its left.|
|`nums[mid] > target`|Target is smaller.|**Move Left:** `right = mid - 1;`|Discard `mid` and everything to its right.|

---

### ⏱️ Complexity

- **Time Complexity:** $O(\log N)$ (The search space is halved in each iteration).
    
- **Space Complexity:** $O(1)$ (Iterative approach uses only a constant number of pointers).
    

---

### 📝 Code Snippet (Iterative Implementation)

Java

public static int search(int[] nums, int target) {
    if (nums == null || nums.length == 0) {
        return -1;
    }
    
    int left = 0;
    int right = nums.length - 1;

    // Standard inclusive invariant: [left, right]
    while (left <= right) {
        
        // SDE 2 Standard: Safe midpoint to prevent integer overflow
        int mid = left + (right - left) / 2;

        if (nums[mid] == target) {
            return mid;
        } else if (nums[mid] < target) {
            // Target is on the right side
            left = mid + 1;
        } else {
            // Target is on the left side
            right = mid - 1;
        }
    }

    return -1; // Target not found
}

---

### 🔗 Pattern Links (Obsidian Integration)

This note is the core of the Binary Search pattern. You can link other problems here:

- [[Binary Search for Range (First_Last Position)]]
    
- [[Binary Search - Rotated Sorted Array]]
    
- [[Binary Search - Square Root]]
    
- [[Binary Search Pattern Hub]]