# Algorithms

For now just some scrambled notes, will reformat later.

## Big O

---

#### Important

- Growth is with respect to the input
- Drop constants
- Worst case is how you _usually_ start to measure

Big O notation is a generalized way of understanding how your algorithm will react to your input.

Another way of saying Big O is:
As your input grows, how fast does computation (performance) or memory grow.

If someone says your algorithm is O of N, denoted as, O(n) - that would mean your algorithm scales linearly based on its input.
The N in O(n) refers to the input size.

We use Big O to help decide which data structure and algorithm to use since we can calculate their performance.

Question yourself if your data set is ordered, if it is you have new advantages you can take (use other algorithms)

---

#### Growth is with respect to input

The below code scales linearly because the for loop has to loop through the length of the string.
So if the string grows by 50% that would mean our function slows by 50%.
For every char in the string, the loop would have to run again.

```
function sum_char_codes(n: string) : number {
    let sum = 0;

    for(let i = 0; i < n.length; i++) {
        sum += n.charCodeAt(i)
    }

    return sum
}

```

The easiest way to tell the Big O complexity is to look for loops.

Ask yourself "where do you loop over the input?"

---

#### Dropping constants

```

function sum_char_codes(n: string) : number {
    let sum = 0;

    for(let i = 0; i < n.length; i++) {
        sum += n.charCodeAt(i)
    }

    for(let i = 0; i < n.length; i++) {
        sum += n.charCodeAt(i)
    }

    return sum
}

```

In this example you might say this is O(2N) since it loops the input twice and that is true but -
the reason we drop constants is that we only need a general approximation relating to the _growth_ of the algorithm.

While the constant maybe practical, eventually that constant becomes irrelevant to measure the time complexity.

An example of this would be:

N = 1 | O(10N) -> 10 | O(N^2) -> 1
N = 10.000 | O(10N) -> 100.000 | O(N^2) -> 100.000.000 // 100 times bigger

So in the first example, having the constant is more accurate and could be seen as more practical.
But the second example shows that the constant infront of N isn't relevant because N^2 grows disproportionally faster.

In summary, we use Big O to not get the _exact_ time, only the growth of an algorithm and not concern ourselves with what unit of measurement we're using like CPUs.

---

#### Worst case measurement

In this following example the function terminates when it encounters a capital E.
This would still be O(N) because we often consider the _worst case_.
It could be that you'd have to go through the entire string.
Or if E were to be in the second last place it could be considered O(N - 2) but we _drop all constants_.

```
function sum_char_code (n: string) : number {
    let sum = 0

    for(let i = 0; i < n.length; i++) {
        const charCode = n.charCodeAt(i)

        // 69 === E
        if(charCode === 69) {
            return sum
        }


        sum+= charCode
    }
}
```

---

#### Examples

##### O(N^2)

---

```
function sum_char_code (n: string) : number {
    let sum = 0

    for(let i = 0; i < n.length; i++) {
      for(let j = 0; j < n.length; j++) {
        sum+= n.charCode(j)
      }
    }

    return sum
}
```

##### O(N^3)

---

```
function sum_char_code (n: string) : number {
    let sum = 0

    for(let i = 0; i < n.length; i++) {
      for(let j = 0; j < n.length; j++) {
        for(let k = 0; k < n.length; k++) {
            sum+= n.charCode(j)
        }
      }
    }

    return sum
}
```

##### O(n log n)

- Quicksort

##### O(log n)

- Binary search tree

---

#### Search Algorithms

---

##### Linear Search

Linear search is what the indexOf method does under the hood
It's walking through each array item and seeing if X item is the index we are looking for

This is a O(n) operation because it grows equally with the array growth as in -
If the array grows by 10, you'd have to loop 10 more times (worst case scenario)

---

##### Binary Search

Can be used in an ordered data set

You can half the array an X amount of times to eventually reach the value you're looking for

This is a _O(log(n)) operation_

---

###### Theoretical Example

Array of 4096 -> 2048 -> 1024 -> 512 -> 256 -> 128 -> 64 -> 32 -> 16 -> 8 -> 4 -> 2 -> 1

This would be log(4096) = 12 // O(log(n))

So 12 halvings before reaching the value in this example, a log(n) amount of halving

And again this example is the _worst case scenario_

---

###### Code Example

If the number is the same as the value on the midpoint

- return true

Else if the number is higher than midpoint value

- start checking from midpoint + 1 index (we know midpoint isnt the value from the first check) to end

Else if the number is lower than midpoint value

- set our midpoint as our high to then check in between low and high again

Repeat this while we can still halve the array (low < high)

```
function bs_list(haystack: number[], needle: number): boolean {
    // Start of array
    let low = 0;

    // End of array
    let high = haystack.length;

    // Do the following while our low < high
    do {
        const midpoint = Math.floor(low + (high - low) / 2);

        // Value of midpoint
        const value = haystack[midpoint];

        if (needle === value) {
            return true;
        } else if (needle > value) {
            low = midpoint + 1;
        } else if (needle < value) {
            high = midpoint;
        }
    } while (low < high);

    return false;
}
```

---

##### Two Crystal Balls Problem

When given two crystal balls that will break if dropped from a high enough distance, determine the exact spot in which it will break.

You can look at this problem as an array full of falses until it starts being true.
If you drop the ball from a 100-story building you could imagine it like:
const stories = [false, false, false, false, true, true, true, etc.]

This array is also ordered which means you can use Binary Search but...

Imagine jumping the middle of the array and it's true, one of the balls just broke!

So now all that's left is linearly walking from the last good point until we hit the bad point
Which is walking from the start to the midpoint (again, worst case)
So linearly from point [0] to the midpoint of N -> O(1/2 of N) -> dropping constant -> O(N)

What's left is to jump in a way that isn't a portion of N to again walk that portion of N - i.e what we did before this

The solution is to jump the Square Root of N an amount of times until the ball breaks
If it breaks, you have to jump backwards to the last known good point
And then walk forward, which at most is... the Sqrt(N)

The running time of this would be, worst case, which is if you have to jump back and walk forward -- O(Sqrt(n) + Sqrt(n))
Which could be written as 2Sqrt(N) but you can drop the 2 so it'll be just O(Sqrt(n))

Summary: To solve this problem _non linearly_, linear as in, jumping by just some portion of N, we can use Sqrt(n)

Why Sqrt and not cubed?

- This would become increasingly smaller jumps the higher N is to the point of becoming almost linear

---

###### Code Example

Jump by the square root of N

Loop over the input until ball breaks

Jump back to previous jump and walk forward until value is found

```
function two_crystal_balls(breaks: boolean[]): number {
    const jumpAmount = Math.floor(Math.sqrt(breaks.length));

    let breakPoint;
    let previousJump;

    // Start at jumping point
    // Keep jumping until ball breaks
    for (let i = jumpAmount; i < breaks.length; i += jumpAmount) {
        if (breaks[i] === true) {
            breakPoint = i;
            previousJump = breakPoint - jumpAmount;
            break;
        }
    }

    // If statement is so TypeScript doesn't yell about vars being undefined

    // Start at previous jumping point
    // Walk forward until our determined breaking point
    // Return the index when found
    if (breakPoint && previousJump) {
        for (let j = previousJump; j < breakPoint; j++) {
            if (breaks[j] === true) {
                return j;
            }
        }
    }

    // False if not found
    return -1;
}
```

---

#### Search Algorithms

---

##### Bubble Sort

The mathy way of saying an array is sorted if every Xi <= Xi + 1
Xi meaning every "ith" position in X array, so X[i] (index)

Bubble sort starts at the 0th position and goes to the end of the array
It looks at the index next to it and says "if _I'm larger_ than you, we _swap position_"

[1, 3, 7, 4, 2] after _one_ iteration will become [1, 3 , 4, 2, 7]
Meaning the largest item will _always_ be at the last spot after an iteration
And in the next iteration we don't have to go to the last spot because that is already sorted

---

##### Tips

If the input halves at each step, it's likely O(LogN) or O(NLogN)
