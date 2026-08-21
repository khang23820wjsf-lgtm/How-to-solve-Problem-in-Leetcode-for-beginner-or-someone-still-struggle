# Lesson 3 – Loop

## Loop – Why do we need it?

Imagine you want to print all numbers from 1 → 1,000,000.

If you don't use a loop, you would have to write the same instruction 1,000,000 times. Obviously, that's impractical.

A loop allows a program to **repeatedly execute** a block of code while following a certain rule.

In another sense: instead of telling the computer *what to do* 1,000,000 times, you tell it *how to repeat* the same task.

---

## 1. What is a loop?

In programming, a **loop** is a code structure used to repeatedly execute a specific block of code until a particular condition is met. Instead of writing the same line of code multiple times, you can simply use a loop to save time and minimize errors.

**Example:** Print numbers from 1 → 1,000,000

```javascript
for (let i = 1; i <= 1000000; i++) {
    console.log(i);
}
```

```cpp
for (int i = 1; i <= 1000000; i++) {
    cout << i << endl;
}
```

We use a loop with a condition that starts at 1 and ends at 1,000,000.

---

## 2. How does a loop work?

The essence of how a loop works is to repeat a cycle of **checking and executing** based on a logical condition. Computers process loops in a strict sequence of four consecutive steps.

### Step 1: Initialization
1. The computer allocates a memory area for the counter variable (often named `i`, `j`, or `count`).
2. This variable is assigned an initial value (e.g., `i = 1`).
3. Note: this step runs only **once**, at the start of the loop.

### Step 2: Condition
1. The computer checks the logical condition (`True` or `False`).
2. If **True**: the computer proceeds into the loop (Step 3).
3. If **False**: the computer immediately exits the loop and executes the subsequent lines of code. The loop terminates.

### Step 3: Execution
1. The computer executes all the commands contained within the body of the loop (the code block).
2. These are the tasks you want to automate (e.g., printing text, performing calculations, sending emails...).

### Step 4: Update
1. After executing the last line of code in the loop body, the computer updates the value of the counter variable (e.g., increments or decrements it by 1).
2. Immediately after the update, the computer returns to Step 2 to re-evaluate the condition using the new value of the counter variable.

---

## 3. How many types of loop are there?

There are two main types of loops: **for** and **while**.

### What is a `for` loop and how does it work?

The `for` loop is the most commonly used type of loop when you know exactly how many times you want to iterate (e.g., iterate exactly 5 times, iterate over 10 elements, iterate from 1 to 100).

Instead of requiring you to manually initialize and update the counter variable across multiple lines of code, the `for` loop condenses all these steps into a single, compact statement.

**Syntax & Structure:**
```
for (initialization; condition; update) {
    // execution code block (loop body)
}
```

**Example (JavaScript):**
```javascript
for (let i = 1; i <= 5; i++) {
    console.log("Iteration:", i);
}
```

**Example (Python):**
```python
for i in range(1, 6):
    print("Iteration:", i)
```

**Example (C++):**
```cpp
for (int i = 1; i <= 5; i++) {
    cout << "Iteration: " << i << endl;
}
```

### What is a `while` loop and how does it work?

The `while` loop is used when you do **not** know the exact number of iterations in advance. Instead, it relies strictly on a logical condition to decide whether to keep running. The loop will continue executing as long as the condition remains `True`.

**Syntax & Structure:**
```
[Initialization]
while (Condition) {
    // Execution code block (loop body)

    [Update]
}
```

**Example (JavaScript):**
```javascript
let i = 1;
while (i <= 5) {
    console.log("Iteration:", i);
    i++;
}
```

**Example (Python):**
```python
i = 1
while i <= 5:
    print("Iteration:", i)
    i += 1
```

**Example (C++):**
```cpp
int i = 1;
while (i <= 5) {
    cout << "Iteration: " << i << endl;
    i++;
}
```

### ⚠️ Warning: Infinite Loop

Unlike the `for` loop, the `while` loop separates the **Initialization** and **Update** steps.

If you forget to write the **Update** step inside the loop body, the condition will always be `True`. This causes an **"Infinite Loop"**, which can freeze your program or crash the computer.

```javascript
// ❌ Infinite loop example — missing the update step
let i = 1;
while (i <= 5) {
    console.log(i);
    // forgot i++ here → i is always 1 → loop never ends
}
```

```cpp
// ❌ Infinite loop example — missing the update step
int i = 1;
while (i <= 5) {
    cout << i << endl;
    // forgot i++ here → i is always 1 → loop never ends
}
```

> **Note:** Besides `for` and `while`, some languages also have a third variant called `do-while`, which executes the loop body **at least once** before checking the condition. This lesson focuses on `for` and `while` since they cover the vast majority of use cases; `do-while` can be covered separately later.

---

## 4. Summary: When to use `for` vs `while`?

- **Use `for` loop:** when the number of iterations is known before entering the loop (e.g., print numbers 1 to 100, read all 10 items in a cart).
- **Use `while` loop:** when the number of iterations depends on an event or external factor, and you cannot predict when it will stop (e.g., keep asking for a password until it's correct, keep running a game until the user clicks "Exit").

---

## 5. Time Complexity and Space Complexity

Understanding how loops affect your computer's resources (CPU and Memory) is critical for writing efficient code. We measure this efficiency using **Big O Notation**.

### Time Complexity (how long the loop takes to run)

1. It represents the relationship between the number of input elements (**N**) and the number of operations the computer must perform.
2. **Single Loop:** if a loop runs exactly N times (e.g., from 1 to N), its time complexity is **O(N)** (Linear Time).
   - *Example:* printing numbers from 1 to 1,000,000 takes 1,000,000 steps. If N doubles, the execution time doubles.
3. **Nested Loops** (loop inside another loop): if you put a loop that runs N times inside another loop that runs N times, the computer performs N × N operations.
   - Its time complexity is **O(N²)** (Quadratic Time).
   - ⚠️ Warning: O(N²) loops can slow down your program drastically when N is large. (A third nested loop would make it O(N³), and so on.)

### Space Complexity (how much extra memory the loop uses)

1. It measures the extra memory space allocated during the execution of the loop.
2. **Standard Loops:** in most cases, a loop only reuses a single counter variable (like `i`) to control the cycle.
   - Its space complexity is **O(1)** (Constant Space).
   - This means no matter if the loop runs 10 times or 1,000,000 times, it consumes the same tiny amount of memory.
3. **Memory-Consuming Loops:** if inside the loop body you continuously create and store new data into a list/array at every iteration, the memory will grow with N.
   - Its space complexity becomes **O(N)** (Linear Space).

### Summary Table

| Structure               | Time Complexity | Space Complexity |
|--------------------------|:---------------:|:-----------------:|
| Loop from 1 to N          | O(N)             | O(1)               |
| Nested Loops (N × N)      | O(N²)            | O(1)               |
| Loop creating N items     | O(N)             | O(N)               |
