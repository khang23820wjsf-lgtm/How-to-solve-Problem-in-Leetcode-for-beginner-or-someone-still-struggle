# Linked List — Feynman Notes

> **Goal:** Understand linked lists from the ground up, instead of memorizing how to use them.

---

# Part 1: Terminology

## 1. So, what the hell is a Linked List?

Unlike a normal array/list, where we can access an element directly using its index:

```text
s[0]
s[1]
s[2]
...
```

a **linked list** is a linear data structure in Computer Science that is made up of **nodes**.

For example:

```text
1 -> 2 -> 3 -> 4 -> None
```

Each node stores two important things:

1. A **value**
2. A **reference to the next node**

So we can imagine the list like this:

```text
1 (val: 1 | next: 2) -> 2 (val: 2 | next: 3)
    -> 3 (val: 3 | next: 4) -> 4 (val: 4 | next: None)
```

The important thing is that the nodes **do not have to be stored next to each other in memory**.

Instead, each node tells us where the next node is.

### Moving through a Linked List

Imagine we are currently at the first node:

```text
current
   |
   v
1 -> 2 -> 3 -> 4 -> NULL
```

If we want to move to the next node, we can use:

```python
current = current.next
```

After that:

```text
      current
         |
         v
1 -> 2 -> 3 -> 4 -> NULL
```

And we can keep doing this until `current` becomes `None`.

---

## How do we access a Linked List? — The `head` pointer

A linked list needs a starting point called **`head`**.

- `head` is a reference pointing to the **very first node**.
- From `head`, we can follow the `next` references to traverse the entire list.
- If we lose the reference to `head` and have no other reference to any node, we can no longer traverse or access the list.

For example:

```text
head
 |
 v
1 -> 2 -> 3 -> 4 -> None
```

You can think of `head` as the **entrance** to the linked list.

If you lose the entrance, good luck getting back inside. 💀

---

# 2. What is a Node?

A **node** is simply an object that stores some data and a reference to another node.

In Python, a simple linked list node can look like this:

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
```

For example:

```python
c = ListNode(5)
```

This means:

```text
c.val  = 5
c.next = None
```

So the node looks like:

```text
c
|
v
+----------------+
| val  | next    |
|  5   | None    |
+----------------+
```

### What do `val` and `next` mean?

`val` stores the actual data.

`next` stores a **reference to the next node**, not simply the next node's value.

For example:

```python
a = ListNode(1)
b = ListNode(2)

a.next = b
```

Now:

```text
a
|
v
+------+------+
| val  | next | ------+
|  1   |  *   |       |
+------+------+       |
                      v
                  +------+------+
                  | val  | next |
                  |  2   | None |
                  +------+------+
```

So `a.next` is referring to node `b`.

It is **not** just storing the number `2`.

---

## The key difference from an Array

An array/list lets me **jump** to an element using an index.

For example:

```python
arr[3]
```

I can directly ask for the element at index `3`.

A linked list makes me **walk** to the element.

If I want to reach the fourth node:

```text
1 -> 2 -> 3 -> 4
```

I have to start from `head` and follow:

```text
head
 |
 v
1 -> 2 -> 3 -> 4
     ^    ^    ^
     |    |    |
   step step step
```

In other words:

> **Array lets me jump to an element; linked list makes me walk to it.**

This is one of the most important ideas to understand before learning linked list algorithms.

---

# 3. What does Traversal mean?

**Traversal** simply means visiting the nodes in a data structure one by one.

For a linked list:

```text
1 -> 2 -> 3 -> 4 -> None
```

we can traverse it by starting from `head` and repeatedly following `next`.

In Python:

```python
current = head

while current:
    # Do something with the current node
    print(current.val)

    current = current.next
```

The important line is:

```python
current = current.next
```

It moves `current` from the current node to the next node.

So the process looks like:

```text
current = head

1 -> 2 -> 3 -> 4 -> None
^
|
current
```

Then:

```text
1 -> 2 -> 3 -> 4 -> None
     ^
     |
   current
```

Then:

```text
1 -> 2 -> 3 -> 4 -> None
          ^
          |
        current
```

Then:

```text
1 -> 2 -> 3 -> 4 -> None
               ^
               |
             current
```

Finally:

```text
1 -> 2 -> 3 -> 4 -> None
                      ^
                      |
                    current
```

`current` becomes `None`, so the loop stops.

---

# Quick Summary

A linked list is made of **nodes**.

Each node contains:

```text
[value | reference to next node]
```

The list starts from:

```text
head
 |
 v
1 -> 2 -> 3 -> 4 -> None
```

To move through it:

```python
current = current.next
```

The three things I need to remember:

- **Node** = stores a value + reference to the next node.
- **Head** = reference to the first node.
- **Traversal** = walking through the nodes one by one.

And the mental model:

> **Array: jump.**  
> **Linked List: walk.**

---

## One thing I should not forget

At first, linked lists can look unnecessarily complicated.

With an array, I can just do:

```python
arr[3]
```

With a linked list, I have to start from `head` and follow the chain until I reach what I want.

But that extra indirection is exactly what makes linked lists useful in situations where we care about how elements are connected and how nodes are inserted or removed.

The important thing is not to memorize:

```python
current = current.next
```

as some magical line of code.

I should understand **why** it works:

> `current` holds a reference to a node, and `current.next` gives me the reference to the next node.

Once that clicks, linked lists become much less scary.
