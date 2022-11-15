# Datastructures

## Arrays

---

### Technical level of Arrays

!Note: This is technical stuff is all about traditional arrays

Arrays are a _contiguous memory_ space that contains a certain amount of bytes (contiguous = unbreaking)
You cannot "grow" arrays since you have to specify the size when you initialize an array
You _can reallocate_ it by taking your old array and writing that into a new one and thus having a bigger array
There are no methods on arrays

Inserting data in an array is going to the memory address, add in the width of the type -
usually done in bytes (32 integer would be 4 bytes) and then multiply by the offset

---

Example:

const a = []
a[0] = 45

the operation would look like: a + width \* 0

This is also a _O(1) process_ since you'd always do the exact same operation for every array
It's a constant amount of things that happen no matter how the input grows

---

### Why a JavaScript Array isn't an actual Array

Arrays in JavaScript have methods like .push which means you grow the array
We previously determined this is not how arrays work, they have a set size
Not to mention there are methods attached to the array itself like .shift and .pop

So a JS array maybe an actual array under the hood somewhere -
but there's something else happening that allows us to add, insert and delete from an array

Bad things about regular arrays

- Can't delete (deleting means just setting an indices to null)
- Can't insert (you can only overwrite, not insert)
- Can't grow (set size)

---

## Linked List

---

Sometimes called a node-based datastructure, nodes being the types of containers that wrap our data

Series of values

Organized in a way that you're able to visit a node but that node will point to the next node

You can't just "get" the ith element in a list
You'll have to start at the _head_ of the linked list and then walk to the element you wanted to return

(A) -> (B) -> (C) -> (D)
This is called a singly linked list because A points to B and B points to C -- you can't walk backwards
The moment you go forward, if you don't have a ref to what's behind you, it's gone
If the head would point to (B) here, no one could access (A)

If you would define this as a type in TypeScript it would look like:

Singly linked list

---

```
Node<T>
  val: T
  nextNode?: Node<T>
```

Doubly Linked List

---

```
Node<T>
  val: T
  nextNode?: Node<T>
  prevNode?: Node<T>
```

A cool property of linked lists is that insertion / deletion can be very fast

###### Insertion

---

Inserting F into:

(A) <-> (B) <-> (C) <-> (D)

If you would insert (F) between (A) and (B)
All you'd need to do is to point A to F and B to F while pointing (F) to both
(A) <-> (F) <-> (B)

None of these operations are based on how many nodes are in a linked list
So basically, setting "Next" could be assumed that it is constant time --- O(1)

###### Deletion

---

Deleting (C) from:

(A) <-> (B) <-> (C) <-> (D)

From (C), take previous node (B)
(B).next = (C).next
And now to point (D) to (B)
(D).prev = (C).prev
(C).prev = (C).next = null

Deletion is also a O(1) operation
It does not matter how big or small the list is
The computer will go into memory to said node and will only need (B) + (C) + (D) to delete
