### 🎯Goal

Find the first (leftmost) and last (rightmost) index of a `target` in a sorted array.

---

### 🧠 Core Idea: Modified Binary Search for Boundaries

The standard binary search finds _any_ index of the target. To find the **boundary (first or last)**, we use a modified approach:

1. When a match is found (`nums[mid] == target`), **record** the current index as a potential answer.
    
2. Instead of immediately returning, **force the search** to continue towards the desired boundary by intelligently adjusting the `left` or `right` pointer.
    

---

### 🛠️ Key Flow & Logic

|**Step**|**Find Left Boundary (First Index)**|**Find Right Boundary (Last Index)**|
|---|---|---|
|**Search Range**|`while (left <= right)`|`while (left <= right)`|
|**Match Found**|`boundaryIndex = mid;`|`boundaryIndex = mid;`|
|**Pointer Update**|**Contract Left:** `right = mid - 1;` (Try to find an _even smaller_ index)|**Expand Right:** `left = mid + 1;` (Try to find an _even larger_ index)|
|**No Match**|If `nums[mid] < target`, move **Right:** `left = mid + 1;`|If `nums[mid] > target`, move **Left:** `right = mid - 1;`|

---

### ⏱️ Complexity

- **Time Complexity:** $O(\log N)$ (Two independent binary searches run on the array).
    
- **Space Complexity:** $O(1)$ (Only a few pointer variables are used).
    

---

### 📝 Code Snippet (Helper Function)

```
private int findBoundary(int[] nums, int target, boolean findLeftBoundary) {
    int left = 0;
    int right = nums.length - 1;
    int boundaryIndex = -1; // Stores the potential answer

    while (left <= right) {
        int mid = left + (right - left) / 2; // Safe midpoint

        if (nums[mid] == target) {
            boundaryIndex = mid; // 1. Record the potential answer
            
            // 2. Force the search direction
            if (findLeftBoundary) {
                right = mid - 1; // Contract left
            } else {
                left = mid + 1; // Expand right
            }
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return boundaryIndex;
}
```