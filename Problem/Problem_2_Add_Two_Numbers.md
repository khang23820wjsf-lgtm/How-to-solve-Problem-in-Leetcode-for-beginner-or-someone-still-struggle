# Problem 2 — Add Two Numbers

You are given two non-empty linked lists representing two non-negative integers.

The digits are stored in **reverse order**, and each of their nodes contains a single digit.

Add the two numbers and return the sum as a linked list.

> If you don't yet know what a linked list is, you can find my article on linked lists in the **Terminology** section. I have explained it clearly there.

---

## Beginner-Friendly Edition

### Explanation

For this problem, I decided to solve it in the simplest way I could understand first.

Instead of adding the two linked lists directly, I will:

```text
Linked List 1
      ↓
   Integer

Linked List 2
      ↓
   Integer

Integer + Integer
      ↓
    Integer
      ↓
Linked List
```

This is not the most optimized approach, but it makes the idea easier to understand.

---

# Part 1 — Convert `list1` into an Integer

### 1. Create `num1`

Create a variable named `num1` — or anything else you like, as long as you'll understand what it represents when you look at it later.

```python
num1 = 0
```

Why does it start at `0`?

Because we need a starting point from which we can combine every digit in the linked list into one complete integer.

---

### 2. Create `place`

Create another variable called `place`.

```python
place = 1
```

`place` tells us what position each digit belongs to.

For example, suppose we have:

```text
2 → 4 → 3 → NULL
```

Because the digits are stored in reverse order, this actually represents:

```text
342
```

We can use:

```text
num1 = num1 + current.val × place
```

Let's walk through it.

### First node

```text
num1 = 0
current.val = 2
place = 1
```

So:

```text
num1 = 0 + 2 × 1
num1 = 2
```

Then we move to the next decimal position:

```text
place = place × 10
place = 10
```

---

### Second node

Now:

```text
current.val = 4
place = 10
```

So:

```text
num1 = 2 + 4 × 10
num1 = 42
```

Then:

```text
place = 10 × 10
place = 100
```

---

### Third node

Now:

```text
current.val = 3
place = 100
```

So:

```text
num1 = 42 + 3 × 100
num1 = 342
```

Tada! 🎉

We converted:

```text
2 → 4 → 3
```

into:

```text
342
```

---

## Python

```python
num1 = 0
place = 1
current = l1

while current:
    num1 += current.val * place
    place *= 10
    current = current.next
```

The important idea is:

```text
current.val × place
```

Each digit gets multiplied by the correct power of 10.

---

# Part 2 — Convert `list2` into an Integer

Now we do exactly the same thing for the second linked list.

We just use different variable names:

```python
num2
place2
current2
```

```python
num2 = 0
place2 = 1
current2 = l2

while current2:
    num2 += current2.val * place2
    place2 *= 10
    current2 = current2.next
```

After this, we have:

```text
num1 = first number
num2 = second number
```

So now we can simply add them:

```python
c = num1 + num2
```

---

# Part 3 — Convert the Integer Back into a Linked List

THIS IS THE START OF THE MOST IMPORTANT PART.

We now have:

```text
c = num1 + num2
```

But the problem does **not** ask us to return an integer.

It asks us to return the answer as a linked list.

So we need to convert our integer back into a linked list.

---

## Special Case: `c == 0`

If the answer is `0`:

```python
return ListNode(0)
```

This means:

```text
0 → NULL
```

It is a linked list containing one node whose value is `0`.

It is **not** an empty list.

---

# Part 4 — The Dummy Node

Otherwise, create a placeholder node called `dummy` with a value of `0`.

```python
dummy = ListNode(0)
current = dummy
```

You may ask:

## Why do we need a dummy node?

`dummy` is a placeholder node used as the starting point of the result linked list.

It does **not** store an actual answer.

Its purpose is to make building the result list easier because we always have a node before the first real result node.

For example:

```text
dummy → 7 → 0 → 8
```

The `dummy` node is just there to give us a convenient starting point.

---

## What is `current` doing?

`current` points to the **last node of the result list**.

Whenever we calculate a new digit, we attach a new node to:

```python
current.next
```

Then we move `current` forward.

For example:

```text
dummy → 7
         ↑
       current
```

We calculate another digit, `0`:

```text
dummy → 7 → 0
             ↑
           current
```

Then another digit, `8`:

```text
dummy → 7 → 0 → 8
                 ↑
               current
```

At the end, `dummy` itself is not part of the actual answer.

So we return:

```python
dummy.next
```

which gives us:

```text
7 → 0 → 8
```

---

# Part 5 — Getting Each Digit

Now we need to extract the digits from our integer.

We use:

```python
c % 10
```

to get the **last digit** of an integer.

For example:

```text
342 % 10 = 2
```

Then we use:

```python
c //= 10
```

to remove the last digit.

```text
342 // 10 = 34
```

So the process becomes:

```text
c = 342

342 % 10 → 2
342 // 10 → 34

34 % 10 → 4
34 // 10 → 3

3 % 10 → 3
3 // 10 → 0
```

Because the problem stores digits in reverse order, this gives us exactly the order needed for the result linked list.

---

# Python Code

```python
class Solution:
    def addTwoNumbers(
        self,
        l1: Optional[ListNode],
        l2: Optional[ListNode]
    ) -> Optional[ListNode]:

        # Convert l1 into an integer
        num1 = 0
        place = 1
        current = l1

        while current:
            num1 += current.val * place
            place *= 10
            current = current.next

        # Convert l2 into an integer
        num2 = 0
        place2 = 1
        current2 = l2

        while current2:
            num2 += current2.val * place2
            place2 *= 10
            current2 = current2.next

        # Add the two numbers
        c = num1 + num2

        # Special case: the answer is 0
        if c == 0:
            return ListNode(0)

        # Create the result linked list
        dummy = ListNode(0)
        current = dummy

        while c > 0:
            current.next = ListNode(c % 10)
            current = current.next
            c //= 10

        return dummy.next
```

---

# C++ Code

```cpp
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {

        // Convert l1 into an integer
        long long num1 = 0;
        long long place = 1;
        ListNode* current = l1;

        while (current != nullptr) {
            num1 += current->val * place;
            place *= 10;
            current = current->next;
        }

        // Convert l2 into an integer
        long long num2 = 0;
        long long place2 = 1;
        current = l2;

        while (current != nullptr) {
            num2 += current->val * place2;
            place2 *= 10;
            current = current->next;
        }

        // Add the two numbers
        long long c = num1 + num2;

        // Special case: the answer is 0
        if (c == 0) {
            return new ListNode(0);
        }

        // Create the result linked list
        ListNode* dummy = new ListNode(0);
        current = dummy;

        while (c > 0) {
            current->next = new ListNode(c % 10);
            current = current->next;
            c /= 10;
        }

        return dummy->next;
    }
};
```

---

# JavaScript Code

```javascript
var addTwoNumbers = function(l1, l2) {

    // Convert l1 into an integer
    let num1 = 0;
    let place = 1;
    let current = l1;

    while (current !== null) {
        num1 += current.val * place;
        place *= 10;
        current = current.next;
    }

    // Convert l2 into an integer
    let num2 = 0;
    let place2 = 1;
    current = l2;

    while (current !== null) {
        num2 += current.val * place2;
        place2 *= 10;
        current = current.next;
    }

    // Add the two numbers
    let c = num1 + num2;

    // Special case: the answer is 0
    if (c === 0) {
        return new ListNode(0);
    }

    // Create the result linked list
    const dummy = new ListNode(0);
    current = dummy;

    while (c > 0) {
        current.next = new ListNode(c % 10);
        current = current.next;
        c = Math.floor(c / 10);
    }

    return dummy.next;
};
```

---

# Example

Suppose:

```text
l1 = 2 → 4 → 3
l2 = 5 → 6 → 4
```

Because the digits are reversed:

```text
l1 = 342
l2 = 465
```

Add them:

```text
342 + 465 = 807
```

Now convert `807` back into the required reversed linked list:

```text
807 % 10 = 7
807 // 10 = 80

80 % 10 = 0
80 // 10 = 8

8 % 10 = 8
8 // 10 = 0
```

Result:

```text
7 → 0 → 8
```

---

# Complexity

Let:

- `n` = length of `l1`
- `m` = length of `l2`

Converting the two linked lists takes:

```text
O(n + m)
```

Creating the result linked list takes approximately:

```text
O(k)
```

where `k` is the number of digits in the sum.

So overall:

```text
Time:  O(n + m + k)
Space: O(k)
```

However, this solution has an important limitation:

> We convert the linked lists into integers first.

For very large numbers, this is not ideal and can even cause integer overflow in languages such as C++.

---

# After Solving It: Can We Do Better?

Yes.

The linked lists already store the digits for us.

So why convert them into integers at all?

We can instead add the numbers **directly node by node**, just like how we learned addition in elementary school:

```text
  342
+ 465
-----
  807
```

Starting from the rightmost digit:

```text
2 + 5 = 7
4 + 6 = 10 → write 0, carry 1
3 + 4 + 1 = 8
```

The linked lists are already reversed:

```text
2 → 4 → 3
5 → 6 → 4
```

So we can process them from left to right while maintaining a `carry`.

That approach avoids converting the entire linked list into an integer and is the more standard solution.

---

# Final Note

This solution might not be the most optimized one.

I intentionally solved it this way because I wanted to understand the problem in the simplest way possible first.

The important thing is not just getting an accepted solution.

The goal is:

```text
I don't understand
       ↓
Break the problem into smaller pieces
       ↓
Find a simple solution
       ↓
Understand why it works
       ↓
Ask: "Can I make it better?"
       ↓
Learn the optimized approach
```

The next step is to solve **Add Two Numbers directly with linked lists**, using `carry`, `dummy`, and `current`.
