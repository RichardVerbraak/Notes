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
