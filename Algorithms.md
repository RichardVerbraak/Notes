# Algorithms

For now just some scrambled notes, will reformat later.

### Big O

#### Important

- Growth is with respect to the input
- Drop constants

Big O notation is a generalized way of understanding how your algorithm will react to your input
Another way of saying Big O is: As your input grows, how fast does computation (performance) or memory grow

If someone says your algorithm is O of N, denoted as, O(n) - that would mean your algorithm scales linearly based on its input
The N in O(n) refers to the input size

We use Big O to help decide which data structure and algorithm to use since we can calculate their performance

---

#### O(n) example

The below code scales linearly because the for loop has to loop through the length of the string
So if the string grows by 50% that would mean our function slows by 50%
For every char in the string, the loop would have to run again

```
function sum_char_codes(n: string) : number {
    let sum = 0;

    for(let i = 0; i < n.length; i++) {
        sum += n.charCodeAt(i)
    }

    return sum
}

```

The easiest way to tell the Big O complexity is to look for loops
Ask yourself "where do you loop over the input?"

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
the reason we drop constants is we care about the _growth_ of the algorithm.

While the constant maybe practical, eventually that constant becomes irrelevant to measure the time complexity

An example of this would be

N = 1 | O(10N) -> 10 | O(N^2) -> 1
N = 10.000 | O(10N) -> 100.000 | O(N^2) -> 100.000.000 // 100 times bigger

So the first example having the constant is more accurate and could be seen as more practical
But the second example shows that the constant infront of N isn't relevant because N^2 grows disproportionally faster

In summary, we use Big O to not get the _exact_ time, only the growth of an algorithm and not concern ourselves with what unit of measurement we're using like CPUs

---