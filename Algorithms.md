# Algorithms

For now just some scrambled notes, will reformat later.

### Big O

Big O notation is a generalized way of understanding how your algorithm will react to your input
Another way of saying Big O is: As your input grows, how fast does computation (performance) or memory grow
Growth is with respect to the input

If someone says your algorithm is O of N, denoted as, O(n) - that would mean your algorithm scales linearly based on its input

We use Big O to help decide which data structure and algorithm to use since we can calculate their performance

O(n) example
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
