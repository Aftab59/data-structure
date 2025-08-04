### 1. What Is the Two-Pointer Technique?
Defination: A problem-solving approach where we maintain two indices (Pointers) to traverse an array, list, or string, either:
   1. From opposite ends toward each other -> converging ponters
   2. From the same string point moving forward -> sliding pointers

   Instead of checking all combinations (O(n^2)), we exploit sorted order or specific constraints to achieve O(n) or better. 

---
### 2.When to use two pointers? 
Look for these mental triggers: 
* Sorted array or string (most common trigger)
* Finding pairs, triplets, subarrays that meet a sum/product condition
* Merging sorted arrays or lists
* Removing or skipping elements without extra space
* Detecting cycle in linked lists (fast/slow pointers)

If one of these appears, this two pointers before brute force

---

### 3. Core Two-Pointer Variants

| Variant | Movement | Common Use-Case |
| ------- |---------|-------------------|
| Opposite Ends | Left at start, right at end; move toward each other | Pair sum in sorted array, palindrome check, container with most water |
| Same Direction (Sliding Window) | Both start at 0; right expands, left shrinks | Subarray problems, removing duplicates in-place |
| Fast & Slow | Fast moves faster than slow | Detect cycles, find middle of linked list | 
| Merge Pointers| Each pointer on a different array; advance smaller one | Merge sorted arrays/lists|

---
### 4. Mental Checklist Before Solving
1. Sorted? -> Start with opposite ends. 
2. Looking for sum/target condition? -> Move pointer that helps meet target. 
3. Removing duplicates or in-place modificatio? Use write-pointer (slow) & read-pointer (fast)
4. Merging? -> compare both and advance one pointer.

----
### 5. Example 1- Pair sum in Sorted Array
Problem: Given arr = [1, 2, 3, 4, 6], target = 6. Find a pair that sums to target.

Thought Process:
1. Sorted? 
2. Looking for sum condition? → Use opposite ends.

Step-by-Step
```dtd
L = 0 (1), R = 4 (6) → sum = 7 > target → move R--
L = 0 (1), R = 3 (4) → sum = 5 < target → move L++
L = 1 (2), R = 3 (4) → sum = 6 ✅ found

```
Code (Flowless Template)
```dtd
public int[] pairSum(int[] arr, int target) {
    int left = 0, right = arr.length - 1;
    while (left < right) {
        int sum = arr[left] + arr[right];
        if (sum == target) {
            return new int[]{arr[left], arr[right]};
        } else if (sum < target) {
            left++;
        } else {
            right--;
        }
    }
    return new int[]{}; // not found
}

```
----
### 6. Example 2- Remove Duplicates from sorted Array
Problem: Modify array in-place to remove duplicates. Return length.
Thought Process:

1. Sorted?
2. Removing duplicates? → Use slow pointer for write index.

Step-by-step:
```dtd
slow = 0
fast = 1
if arr[slow] != arr[fast]:
    slow += 1
    arr[slow] = arr[fast]

```
Code: 
```dtd
public int removeDuplicates(int[] nums) {
    if (nums.length == 0) return 0;
    int slow = 0;
    for (int fast = 1; fast < nums.length; fast++) {
        if (nums[fast] != nums[slow]) {
            slow++;
            nums[slow] = nums[fast];
        }
    }
    return slow + 1;
}

```
### 7.Example 3 - Container with most water
Problem: Find two lines that hold the most water. 

Thought Process: 
1. Sorted? No, but opposite ends works because moving inward can maximize area. 
2. Formula: width * min(height[left], height [right])
3. Move pointer at smaller height (Since taller one may hold more with another pairing)

----

### 8. How you will identify this instantly
* See "sorted array" -> think opposite ends. 
* See "remove duplicates" -? think fast/slow. 
* See "merge sorted arrays" -> think merge pointers. 
* See "cycle detection" -> think fast/slow. 
