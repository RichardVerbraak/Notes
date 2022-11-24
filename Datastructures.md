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

#### Insertion

---

Inserting F into:

(A) <-> (B) <-> (C) <-> (D)

If you would insert (F) between (A) and (B)
All you'd need to do is to point A to F and B to F while pointing (F) to both
(A) <-> (F) <-> (B)

None of these operations are based on how many nodes are in a linked list
So basically, setting "Next" could be assumed that it is constant time --- O(1)

#### Deletion

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

#### Time / Space complexity

- Prepending / Appending
  Getting the head and tail of a linked list is constant since we have a defined pointer to that, so inserting at the start or end is fast

- Insertion / Deletion from the middle
  The operation itself is fast but depending on how big the list is, traversing it can be slow

Summary: Linked Lists are fast for doing operations at both ends but _could_ be very slow if you were to traverse to the middle to do said operation

The API for a LinkedList in TypeScript:

```
interface LinkedList<T> {
  get length(): number;
  insertAt(item: T, index: number): void;
  remove(item: T): T | undefined;
  removeAt(index: number); T | undefined;
  append(item: T): void;
  prepend(item: T): void;
  get(index: number): T | undefined;
}
```

---

## Queue

---

A queue is a Datastructure build on top of a Linked List

You can think of it like a First in / First out operation (FIFO)
So like getting back into the end of a line at for example, a carnival ride

If you were to append (E) at the end of the following _singly linked list_:

(A) -> (B) -> (C) -> (D) (E)

You can point the tail.next to (E) and then set tail to (E)

Now if you want to set (B) to be the head, you'd do the reverse

First you temporarily store the current head (A)
Set head to head.next which is (B)
Then set the original head.next to null in order to "break the link"

These are all O(1) operations

---

###### Code Example of Queue as Class

```
type Node<T> = {
    value: T;
    nextNode?: Node<T>;
};

export default class Queue<T> {
    public length: number;
    private head?: Node<T>;
    private tail?: Node<T>;

    constructor() {
        this.head = undefined;
        this.tail = undefined;
        this.length = 0;
    }

    // Add
    enqueue(item: T): void {
        const node = { value: item } as Node<T>;

        this.length++;

        // If there is no tail, meaning there aren't any items and thus also no head
        // Set our tail and head to point to the new node
        // Basically creating an array (list rather) with 1 item
        if (!this.tail) {
            this.tail = this.head = node;
            return;
        }

        // Set the nextNode of the current tail to our new node
        this.tail.nextNode = node;

        // Set current tail to be said new node
        this.tail = node;
    }

    // Pop
    deque(): T | undefined {
        if (!this.head) {
            return undefined;
        }

        this.length--;

        const head = this.head;
        this.head = this.head.nextNode;

        // Don't have to do this since JS uses a "garbage collector" to free up the space itself
        head.nextNode = undefined;

        return this.head?.value;
    }

    // Get
    peek(): T | undefined {
        return this.head?.value;
    }
}
```

---

## Stack

---

A stack is a queue but in reverse
It looks and acts like a queue
Is a singly linked list which you can only add or remove from the head

(D) being the head

(A) <- (B) <- (C) <- (D)

If you wanted to add (E) you would do:

(E).next = head
head = E

Removing and returning (E) would be:
currentHead = head (E)
head = currentHead.next
return currentHead

A stack only allows pushing and popping from one side which makes it a really fast operation
And again the running time for this is still O(1) since we're just pointing to other values

---

###### Code Example of Stack as Class

```
type Node<T> = {
    value: T;
    next?: Node<T>;
};

export default class Stack<T> {
    public length: number;
    private head?: Node<T>;

    constructor() {
        this.length = 0;
        this.head = undefined;
    }

    push(item: T): void {
        const node = { value: item } as Node<T>;

        this.length++;

        if (!this.head) {
            this.head = node;
            return;
        }

        node.next = this.head;
        this.head = node;
    }

    pop(): T | undefined {
        if (!this.head) {
            return undefined;
        }

        // A <- B <- C

        this.length--;

        const head = this.head;

        // Point head to the next one (C points to B)
        this.head = head.next;

        // In another langue you'd usually free up the space the previous head was using

        return head.value;
    }

    peek(): T | undefined {
        return this.head?.value;
    }
}
```

---

## Arrays vs Linked List

---

Usability

- Arrays

  - Good
    Can access random indices
    Easy to just allocate memory and set the values

  - Bad
    No literal insert, you can only overwrite
    Manually have to write a for loop to set an indices to null for deletion

- Linked List

  - Good

    - Can push and pop really easily from the head and tail

  - Bad
    - Not as easy to access nodes
    - Cumbersome to create a linked list and connect all of the nodes

Time

- Arrays

  - O(1) for every operation (overwriting, accessing, deleting)

- Linked List

  - Always has linear search since you have to walk through all the nodes, can't just jump in the middle
  - Fast with push/pop

Space

- Arrays

  - Set amount of memory

- Linked List

  - Memory usage more optimized since it's not a pre-defined amount

Contrived use case for a Linked List:

If you didn't want to have more than 5 async/await requests happening at the same time -
you'd have to pull of the front and push in the new as the older requests complete.

This is basically a queue problem and using an array here wouldn't be optimal because you'd
have to shift/unshift all the indices around vs just using the head/tail in a Linked List.

---

## ArrayList

---

An ArrayList has _array access_ and the _ability to grow_ like a list

Example:

An array with the length of 1 but the capacity of 3

[2, null, null]

Get(index)
If it's out of bounds
if(index >= arr.length) throw Error

Push operation
If the length is within the capacity, push the item
if(length =< arr.capacity) push(item)

Pushing when length = capacity
Create a new array with for example, double the capacity (6)

An ArrayList technically starts off with an array structure since you start off by giving it a hint -
"Hey how much space do you want to use and not allocate too much memory"
It comes down to a game of reserving the least amount of memory while also doing the least amount of growing operations

What about Queue like operations (Enqueue and Queue)

Enqueue (insert at front) example:

Length: 3
Capacity: 6

[2, 3, 5, null, null, null]

The problem here would be that you can't just "write" at index[0] because you will overwrite the value 2 here
So what you'll have to start at 5 and shift everything by 1 to the right side so [0] will be empty to insert our value into

This is a O(n) operation and not performant which is why people would use a node based list instead of an array for these operations

So to summarize, an ArrayList is bad with queue and dequeue but good with push / pop, the latter being O(1)

Same with removing at an index, if you were to jump into the middle and remove an item,
you'd have to shift all the items that came after that index in order to fill the "gap" you created
Doing a get(index) and it returning null instead of an item because you didn't shift things would be problematic
