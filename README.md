# DSA

-----

# Data Structures & Algorithms: Binary Search

Binary search is an efficient algorithm for finding an item from a sorted list of items. It works by repeatedly dividing in half the portion of the list that could contain the item, until you've narrowed down the possible locations to just one.

-----

### Kth Smallest Product of Two Sorted Arrays

**Tag:** Binary Search

**Question:** Given two sorted 0-indexed integer arrays `nums1` and `nums2` and an integer `k`, return the `k`-th (1-based) smallest product of `nums1[i] * nums2[j]` where $0 \\le i \< \\text{nums1.length}$ and $0 \\le j \< \\text{nums2.length}$.

-----

### 1\. Check If a Number Exists in a Sorted Array

**❓ Problem:** Given a sorted array `arr` and a `target` value, return `True` if `target` exists in the array, otherwise `False`.

```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1

    while left <= right:
        mid = (left + right) // 2

        if arr[mid] == target:
            return True
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return False
```

-----

### 2\. Find First Occurrence of a Number in a Sorted Array

**❓ Problem:** Given a sorted array `arr` (with possible duplicates) and a `target` value, return the index of the **first occurrence** of `target`. If not found, return `-1`.

```python
def first_occurrence(arr, target):
    left, right = 0, len(arr) - 1
    result = -1

    while left <= right:
        mid = (left + right) // 2

        if arr[mid] == target:
            result = mid
            right = mid - 1  # Search in the left half for an earlier occurrence
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return result
```

-----

### 3\. Find Last Occurrence of a Number in a Sorted Array

**❓ Problem:** Given a sorted array `arr` (with possible duplicates) and a `target` value, return the index of the **last occurrence** of `target`. If not found, return `-1`.

```python
def last_occurrence(arr, target):
    left, right = 0, len(arr) - 1
    result = -1

    while left <= right:
        mid = (left + right) // 2

        if arr[mid] == target:
            result = mid
            left = mid + 1  # Search in the right half for a later occurrence
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return result
```

-----

### 4\. Find Index of First Element Greater Than a Given Number

**❓ Problem:** Given a sorted array `arr` and a number `num`, return the index of the **first element strictly greater** than `num`. If no such element exists, return `-1`.

```python
def index_of_first_greater(arr, num):
    left, right = 0, len(arr) - 1
    result = -1

    while left <= right:
        mid = (left + right) // 2

        if arr[mid] > num:
            result = mid
            right = mid - 1  # Try to find an earlier index
        else:
            left = mid + 1
    return result
```

-----

### 5\. Find Index of Last Element Less Than a Given Number

**❓ Problem:** Given a sorted array `arr` and a number `num`, return the index of the **last element strictly less** than `num`. If no such element exists, return `-1`.

```python
def index_of_last_less(arr, num):
    left, right = 0, len(arr) - 1
    result = -1

    while left <= right:
        mid = (left + right) // 2

        if arr[mid] < num:
            result = mid
            left = mid + 1  # Try to find a later index
        else:
            right = mid - 1
    return result
```

-----

### 6\. Count Elements Less Than a Given Number

**❓ Problem:** Given a sorted array `arr` and a number `num`, return the **number of elements strictly less than** `num`.

```python
def count_elements_less_than(arr, num):
    left, right = 0, len(arr) - 1
    count = 0 # Initialize count of elements less than num

    while left <= right:
        mid = (left + right) // 2

        if arr[mid] < num:
            count = mid + 1 # All elements up to mid are less than num
            left = mid + 1  # Look for more on the right
        else:
            right = mid - 1 # Search in the left half
    return count
```

-----

### 7\. Count Elements Greater Than a Given Number

**❓ Problem:** Given a sorted array `arr` and a number `num`, return the **number of elements strictly greater than** `num`.

```python
def count_elements_greater_than(arr, num):
    left, right = 0, len(arr) - 1
    first_greater_idx = len(arr) # Default to array length if no element is greater

    while left <= right:
        mid = (left + right) // 2

        if arr[mid] > num:
            first_greater_idx = mid # Potential start of elements greater than num
            right = mid - 1         # Try to find an earlier greater element
        else:
            left = mid + 1
    return len(arr) - first_greater_idx
```

-----

### 8\. Count Elements Less Than or Equal to a Given Number

**❓ Problem:** Given a sorted array `arr` and a number `num`, return the **number of elements less than or equal to** `num`.

```python
def count_elements_less_equal(arr, num):
    left, right = 0, len(arr) - 1
    count = 0 # Initialize count of elements less than or equal to num

    while left <= right:
        mid = (left + right) // 2

        if arr[mid] <= num:
            count = mid + 1 # All elements up to mid are less than or equal to num
            left = mid + 1  # Look for more on the right
        else:
            right = mid - 1 # Search in the left half
    return count
```

-----

### 9\. Count Elements Greater Than or Equal to a Given Number

**❓ Problem:** Given a sorted array `arr` and a number `num`, return the **number of elements greater than or equal to** `num`.

```python
def count_elements_greater_equal(arr, num):
    left, right = 0, len(arr) - 1
    first_ge_idx = len(arr) # Default to array length if all elements are less than num

    while left <= right:
        mid = (left + right) // 2

        if arr[mid] >= num:
            first_ge_idx = mid  # Potential start of elements greater than or equal to num
            right = mid - 1     # Search for an earlier index
        else:
            left = mid + 1
    return len(arr) - first_ge_idx
```

-----

### 10\. Count of Products $\\le v$ When Multiplied by $x$ (for any $x$)

**❓ Problem:** Given a sorted array `nums2`, an integer `x`, and an integer `v`, count how many elements in `nums2` satisfy the condition: $x \\times \\text{nums2}[j] \\le v$. This function handles positive, negative, and zero values for `x`.

```python
def count_products_leq_v(nums2, x, v):
    n = len(nums2)
    
    if x == 0:
        return n if v >= 0 else 0

    left, right = 0, n - 1

    if x > 0:
        # For positive x, we are looking for the count of numbers nums2[j] <= v/x
        # This is equivalent to finding the last element less than or equal to v/x
        ans_idx = -1
        while left <= right:
            mid = (left + right) // 2
            if x * nums2[mid] <= v:
                ans_idx = mid
                left = mid + 1
            else:
                right = mid - 1
        return ans_idx + 1

    else:  # x < 0
        # For negative x, multiplying by a smaller number in nums2 results in a larger product.
        # We need to find nums2[j] such that nums2[j] >= v/x (since inequality flips)
        # This is equivalent to finding the first element greater than or equal to v/x
        ans_idx = n
        while left <= right:
            mid = (left + right) // 2
            if x * nums2[mid] <= v: # The condition still applies, but its effect on index changes
                ans_idx = mid
                right = mid - 1 # Try to find an earlier element that satisfies the condition
            else:
                left = mid + 1
        return n - ans_idx
```

-----

### 11\. Count of Products $\< v$ When Multiplied by $x$ (for any $x$)

**❓ Problem:** Given a sorted array `nums2`, an integer `x`, and an integer `v`, count how many elements in `nums2` satisfy the condition: $x \\times \\text{nums2}[j] \< v$. This function handles positive, negative, and zero values for `x`.

```python
def count_products_lt_v(nums2, x, v):
    n = len(nums2)

    if x == 0:
        return n if v > 0 else 0

    left, right = 0, n - 1

    if x > 0:
        # For positive x, we are looking for the count of numbers nums2[j] < v/x
        # This is equivalent to finding the last element strictly less than v/x
        ans_idx = -1
        while left <= right:
            mid = (left + right) // 2
            if x * nums2[mid] < v:
                ans_idx = mid
                left = mid + 1
            else:
                right = mid - 1
        return ans_idx + 1

    else:  # x < 0
        # For negative x, multiplying by a smaller number in nums2 results in a larger product.
        # We need to find nums2[j] such that nums2[j] > v/x (since inequality flips)
        # This is equivalent to finding the first element strictly greater than v/x
        ans_idx = n
        while left <= right:
            mid = (left + right) // 2
            if x * nums2[mid] < v: # The condition still applies, but its effect on index changes
                ans_idx = mid
                right = mid - 1 # Try to find an earlier element that satisfies the condition
            else:
                left = mid + 1
        return n - ans_idx
```

-----

### 12\. Count of Products $\> v$ When Multiplied by $x$ (for any $x$)

**❓ Problem:** Given a sorted array `nums2`, an integer `x`, and an integer `v`, count how many elements in `nums2` satisfy the condition: $x \\times \\text{nums2}[j] \> v$. This function handles positive, negative, and zero values for `x`.

```python
def count_products_gt_v(nums2, x, v):
    n = len(nums2)

    if x == 0:
        return n if v < 0 else 0

    left, right = 0, n - 1

    if x > 0:
        # For positive x, we are looking for the count of numbers nums2[j] > v/x
        # This is equivalent to finding the first element strictly greater than v/x
        ans_idx = n
        while left <= right:
            mid = (left + right) // 2
            if x * nums2[mid] > v:
                ans_idx = mid
                right = mid - 1
            else:
                left = mid + 1
        return n - ans_idx

    else:  # x < 0
        # For negative x, multiplying by a smaller number in nums2 results in a larger product.
        # We need to find nums2[j] such that nums2[j] < v/x (since inequality flips)
        # This is equivalent to finding the last element strictly less than v/x
        ans_idx = -1
        while left <= right:
            mid = (left + right) // 2
            if x * nums2[mid] > v: # The condition still applies, but its effect on index changes
                ans_idx = mid
                left = mid + 1 # Try to find a later element that satisfies the condition
            else:
                right = mid - 1
        return ans_idx + 1
```

-----

### 13\. Count of Products $\\ge v$ When Multiplied by $x$ (for any $x$)

**❓ Problem:** Given a sorted array `nums2`, an integer `x`, and an integer `v`, count how many elements in `nums2` satisfy the condition: $x \\times \\text{nums2}[j] \\ge v$. This function handles positive, negative, and zero values for `x`.

```python
def count_products_ge_v(nums2, x, v):
    n = len(nums2)

    if x == 0:
        return n if v <= 0 else 0

    left, right = 0, n - 1

    if x > 0:
        # For positive x, we are looking for the count of numbers nums2[j] >= v/x
        # This is equivalent to finding the first element greater than or equal to v/x
        ans_idx = n
        while left <= right:
            mid = (left + right) // 2
            if x * nums2[mid] >= v:
                ans_idx = mid
                right = mid - 1
            else:
                left = mid + 1
        return n - ans_idx

    else:  # x < 0
        # For negative x, multiplying by a smaller number in nums2 results in a larger product.
        # We need to find nums2[j] such that nums2[j] <= v/x (since inequality flips)
        # This is equivalent to finding the last element less than or equal to v/x
        ans_idx = -1
        while left <= right:
            mid = (left + right) // 2
            if x * nums2[mid] >= v: # The condition still applies, but its effect on index changes
                ans_idx = mid
                left = mid + 1 # Try to find a later element that satisfies the condition
            else:
                right = mid - 1
        return ans_idx + 1
```
