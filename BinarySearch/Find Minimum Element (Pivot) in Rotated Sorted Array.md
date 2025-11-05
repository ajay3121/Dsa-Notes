### Goal

Find the **index of the minimum element (the pivot)** in a Rotated Sorted Array in $O(\log N)$ time.

### 🧠 Core Idea: Preserve the Disruption (Your Logic)

The strategy is to use the comparison between $\mathbf{nums[mid]}$ and $\mathbf{nums[right]}$ to determine which segment is **sorted**. We then **discard the sorted segment** because the minimum (the point of disruption) must be in the unsorted segment, which becomes the new, smaller subproblem.

---

### 🛠️ Key Flow & Logic

We use the search space invariant $\mathbf{while (left < right)}$ to ensure convergence on the single pivot index.

|**Case**|**Condition**|**Your Reasoning**|**Action**|**Pointer Update (New Subproblem)**|
|---|---|---|---|---|
|**Pivot Right**|$\mathbf{nums[mid] > nums[right]}$|The left side $\mathbf{[left, mid]}$ is sorted. The right side $\mathbf{[mid+1, right]}$ is the unsorted subproblem where the minimum **must** be.|Discard the left sorted segment.|$\mathbf{left = mid + 1;}$|
|**Pivot Left**|$\mathbf{nums[mid] \le nums[right]}$|The right side $\mathbf{[mid, right]}$ is sorted. The minimum is either at `mid` or in the left unsorted subproblem $\mathbf{[left, mid)}$.|Keep `mid` as the best candidate and discard the right sorted segment.|$\mathbf{right = mid;}$|

---

### ⏱️ Complexity

- **Time Complexity:** $O(\log N)$ (The subproblem size is halved in every iteration).
    
- **Space Complexity:** $O(1)$.
    

---

### 📝 Code Snippet (SDE 2 Standard)

Java

```
/**
 * Finds the index of the minimum element (the pivot).
 */
static int findPivot(int[] nums) {
    int left = 0;
    int right = nums.length - 1;

    // Loop terminates when left == right, pointing to the minimum.
    while (left < right) {
        int mid = left + (right - left) / 2; // Safe midpoint

        if (nums[mid] > nums[right]) {
            // Right is the unsorted subproblem: move to mid + 1
            left = mid + 1;
        } else { 
            // Left (or mid) is the subproblem: contract to mid
            right = mid; 
        }
    }
    // left == right at termination
    return left;
}
```

---

### 🔗 Pattern Links (Obsidian Integration)
[[Binary Search - Rotated Sorted Array]]