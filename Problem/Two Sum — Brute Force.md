# Two Sum — Brute Force

## Problem

We have a list variable named `nums` and a variable named `target`.

Our mission is to find **two different numbers** in the list whose sum is equal to `target`, and return their indices.

We **cannot use the same element twice**.

### Example 1

```text
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
```

**Explanation:**
Because `nums[0] + nums[1] == 9`, we return `[0,1]`.

### Example 2

```text
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

---

## For Beginners

We can use **brute force** to solve this problem.

The basic idea is simple:

> Try every possible pair of numbers and check whether their sum is equal to `target`.

We will use **two nested loops** to check every possible pair.

### Complexity

* **Time Complexity:** `O(n²)`
* **Space Complexity:** `O(1)`

Brute force is simple and works well when the list is small.

However, as the number of elements increases, we have to check more and more pairs, making this approach inefficient.

I think this is a good way for beginners to start learning because it helps us understand the problem before trying to optimize the solution.

---

## The Main Condition

Our condition is:

```python
if nums[i] + nums[j] == target:
    i1, j1 = i, j
    break
```

If the sum of `nums[i]` and `nums[j]` equals `target`, we have found our answer.

---

## Python

```python
nums = list(map(int, input().split()))
target = int(input())

i1, j1 = -1, -1

for i in range(len(nums)):
    for j in range(i + 1, len(nums)):
        if nums[i] + nums[j] == target:
            i1, j1 = i, j
            break

if i1 != -1:
    print(i1, j1)
else:
    print(-1)
```

---

## C++

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> nums;
    int x;

    while (cin >> x) {
        nums.push_back(x);
    }

    int target;
    cin.clear();
    cin >> target;

    int i1 = -1, j1 = -1;

    for (int i = 0; i < nums.size(); i++) {
        for (int j = i + 1; j < nums.size(); j++) {
            if (nums[i] + nums[j] == target) {
                i1 = i;
                j1 = j;
                break;
            }
        }
    }

    if (i1 != -1) {
        cout << i1 << " " << j1 << endl;
    } else {
        cout << -1 << endl;
    }

    return 0;
}
```

---

## JavaScript

```javascript
const fs = require("fs");

const input = fs.readFileSync(0, "utf8").trim().split("\n");

const nums = input[0].split(" ").map(Number);
const target = Number(input[1]);

let i1 = -1;
let j1 = -1;

for (let i = 0; i < nums.length; i++) {
    for (let j = i + 1; j < nums.length; j++) {
        if (nums[i] + nums[j] === target) {
            i1 = i;
            j1 = j;
            break;
        }
    }
}

if (i1 !== -1) {
    console.log(i1, j1);
} else {
    console.log(-1);
}
```

---

## Why `j = i + 1`?

You may notice that the second loop starts with:

```python
for j in range(i + 1, len(nums)):
```

Why `i + 1`?

There are **two reasons**.

### 1. We cannot use the same element twice

Suppose:

```text
nums = [2, 7, 11, 15]
```

If `i = 0`, then `nums[i]` is `2`.

We don't want:

```text
nums[0] + nums[0]
```

because that would use the same element twice.

Starting `j` from `i + 1` guarantees that:

```text
j > i
```

So `i` and `j` are always different.

### 2. We don't need to check the same pair twice

Without `i + 1`, we might check:

```text
nums[0] + nums[1]
```

and later:

```text
nums[1] + nums[0]
```

These are the same pair.

By starting from `i + 1`, we only check each pair once.

---

## Understanding the Loops

For:

```text
nums = [2, 7, 11, 15]
```

The loops check pairs like this:

```text
i = 0:
    (0,1)
    (0,2)
    (0,3)

i = 1:
    (1,2)
    (1,3)

i = 2:
    (2,3)
```

We don't check:

```text
(0,0)
(1,1)
(2,2)
(3,3)
```

because we cannot use the same element twice.

We also don't check:

```text
(1,0)
(2,0)
(2,1)
...
```

because those pairs have already been checked in the opposite order.

---

## Time Complexity

The time complexity is:

```text
O(n²)
```

because, in the worst case, we may need to check almost every possible pair.

For example, if the list becomes much larger, the number of pairs increases very quickly.

That's the main weakness of the brute-force approach.

---

## Space Complexity

The space complexity is:

```text
O(1)
```

because we only use a few extra variables such as:

```python
i
j
i1
j1
```

We don't create any additional data structure to store information about the elements.

---

## Conclusion

Although brute force is **not the most efficient solution**, it is a great approach for beginners because it is simple and easy to understand.

More importantly, it helps us understand the problem before moving on to more optimized solutions.

Once we understand the brute-force solution, we can start asking:

> **Can we find the answer without checking every possible pair?**

That's where the **Hash Map** solution comes in.

> **In the future, I will do the Hash Map edition UwU.** 🗿
