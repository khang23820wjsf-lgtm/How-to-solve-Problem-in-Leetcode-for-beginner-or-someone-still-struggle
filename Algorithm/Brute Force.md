# Algorithm - Lesson 1: Brute Force

## 1. What is Brute Force?

Brute Force is a straightforward problem-solving approach that tries every possible candidate until it finds a valid solution.

The main idea is simple:

> **Try everything, check everything, and don't miss a valid answer.**

---

## 2. The Core Idea

The core idea of the brute-force algorithm is:

> **"Better to kill the innocent than let the guilty go free."**

In other words, instead of trying to find a clever shortcut immediately, we systematically check all possible cases.

There are two main steps:

### 1. List all possible cases

The computer generates all possible cases, answers, combinations, or other candidates that could be relevant to the problem.

### 2. Check each case

We test each candidate directly to see whether it satisfies the required conditions.

The algorithm does not need to be particularly clever. It simply makes sure that every possibility is checked.

### Example

Suppose we have:

```text
Array = [1, 2, 3, 4, 5]
Target = 7
```

We need to find two numbers whose sum equals the target.

### How does it work?

Start with number `1`:

```text
Try pair (1, 2) -> sum = 3  -> Wrong
Try pair (1, 3) -> sum = 4  -> Wrong
Try pair (1, 4) -> sum = 5  -> Wrong
Try pair (1, 5) -> sum = 6  -> Wrong
```

Then move to number `2`:

```text
Try pair (2, 1) -> sum = 3  -> Wrong
Try pair (2, 3) -> sum = 5  -> Wrong
Try pair (2, 4) -> sum = 6  -> Wrong
Try pair (2, 5) -> sum = 7  -> Accepted
```

And the algorithm continues checking possible pairs until it finds a valid answer or finishes checking all possibilities.

> **The important part is not the specific pair. The important part is that every possible candidate is considered.**

---

## 3. Time and Space Complexity

### Time Complexity

Brute Force often has a high time complexity because it may need to examine a large number of possible outcomes.

The actual complexity depends on the problem.

Some common examples are:

### `O(n²)` or `O(n³)`

These commonly appear when the algorithm uses nested loops to examine pairs, triples, or other combinations.

For example:

```text
for each i
    for each j
        check(i, j)
```

This can result in `O(n²)` time.

### `O(2^n)`

This commonly appears when considering all subsets.

For each element, there can be two choices:

```text
Select it
OR
Do not select it
```

Therefore, with `n` elements, there can be `2^n` possible subsets.

### `O(n!)`

This commonly appears when trying every possible permutation.

For example, if we need to test every possible ordering of `n` cities, the number of possible permutations is:

```text
n!
```

The number of possibilities grows extremely quickly, so brute-force permutation problems become impractical even for relatively small values of `n`.

---

### Space Complexity

Brute Force does **not** have one fixed Space Complexity.

However, many simple brute-force algorithms can use very little extra memory because they process one candidate at a time instead of storing every possible result.

For example:

```text
O(1)
```

may be possible when we only need a few variables or counters.

However, some brute-force approaches may require more memory, especially when they generate and store many candidates or use recursion/backtracking.

For example:

```text
O(n)
```

may occur because of recursion depth.

The important point is:

> **Brute Force can have low Space Complexity, but it is not automatically O(1).**

---

## 4. When Should We Use Brute Force?

Brute Force is useful when:

- The search space is small enough to explore within the given constraints.
- We need a simple and reliable solution.
- We want to create a baseline solution before developing an optimized one.
- We want to verify the correctness of a more complicated algorithm.
- We cannot yet see a better approach.

A brute-force solution is often a good **starting point**.

First, solve the problem correctly.

Then ask:

> **"What work am I doing unnecessarily?"**

That question can lead us toward a more optimized algorithm.

---

## 5. Limitations

### 5.1 Time Limit Exceeded (TLE)

One of the biggest problems with Brute Force is that the number of operations can become too large.

For example, suppose:

```text
n = 10^5
```

and our solution has:

```text
O(n²)
```

The number of operations can be roughly:

```text
(10^5)² = 10^10
```

That is far too many operations for most competitive programming time limits.

The result is usually:

```text
Time Limit Exceeded (TLE)
```

So even if the algorithm is logically correct, it may still receive no points because it cannot finish within the required time.

---

### 5.2 Inefficient for Large Graph and Tree Problems

Brute Force can also be used on Graph and Tree problems.

The problem is that the number of possible paths, configurations, or states can grow extremely quickly.

For example, a brute-force graph algorithm might try many different paths between vertices.

If cycles exist, we also need to keep track of visited states to avoid repeatedly exploring the same states.

Therefore, the problem is not that Brute Force is "powerless" against Graphs or Trees.

The real problem is:

> **The search space can become too large.**

---

### 5.3 Redundant Computation

Brute Force often performs the same work repeatedly because it does not take advantage of information it has already computed.

A classic example is the recursive Fibonacci sequence.

To calculate:

```text
F(5)
```

we calculate:

```text
F(5)
├── F(4)
│   ├── F(3)
│   └── F(2)
└── F(3)
    ├── F(2)
    └── F(1)
```

Notice that `F(3)` and `F(2)` are calculated multiple times.

The larger `n` becomes, the more repeated work occurs.

This is one of the ideas that eventually leads to:

> **Dynamic Programming: remember results that have already been calculated.**

---

### 5.4 Brute Force May Only Pass Small Subtasks

In competitive programming, a problem may have multiple subtasks with different constraints.

For example:

```text
Subtask 1: N <= 1,000
Subtask 2: N <= 100,000
```

A brute-force solution might pass the smaller subtask but fail the larger one because its complexity is too high.

This means:

> **A correct solution is not necessarily an efficient solution.**

Brute Force can sometimes earn partial points, but we need a better algorithm to handle larger constraints.

---

## 6. Can We Do Better?

Brute Force checks every possible pair, which takes `O(n²)` time for the Two Sum example.

But do we really need to check every pair?

For each number `x`, we only need to know whether:

```text
target - x
```

has already appeared.

For example:

```text
Array:  [1, 2, 3, 4, 5]
Target: 7
```

Take `2`:

```text
7 - 2 = 5
```

Have we seen `5` before?

```text
No.
```

Take `3`:

```text
7 - 3 = 4
```

Have we seen `4` before?

```text
No.
```

Take `4`:

```text
7 - 4 = 3
```

Have we seen `3` before?

```text
Yes -> Found the answer.
```

Instead of checking every possible pair, we can use a **Hash Map / Hash Set** to remember the values we have already seen.

This reduces the time complexity from:

```text
Brute Force: O(n²)
Hash Map:    O(n)
```

The main idea is:

> **Don't repeatedly search for something that you can remember.**

This is an important pattern in algorithmic thinking:

```text
Brute Force
    ↓
Find repeated or unnecessary work
    ↓
Find a way to avoid it
    ↓
More efficient algorithm
```

---

## 7. Practice Problems

1. [Two Sum - LeetCode #1](https://leetcode.com/problems/two-sum/)
2. [Maximum Subarray - LeetCode #53](https://leetcode.com/problems/maximum-subarray/)
3. [3Sum - LeetCode #15](https://leetcode.com/problems/3sum/)

---

## 8. My Takeaway

- Brute Force might not be the most efficient algorithm, but it can be a **springboard for developing algorithmic thinking**.
- It is simple and reliable, but the number of possible cases can grow very quickly, making it inefficient for large inputs.
- Brute Force is often a good starting point: first make sure I can solve the problem correctly, then think about how to reduce unnecessary work.
- The most important question is not only **"Can I solve this problem?"**, but also:

  > **"What work am I doing unnecessarily?"**

That question is often the beginning of optimization.
