# JavaScript

A random collection of notes on how JavaScript operates and it's quirks

## General Info

JavaScript is

    - Single-Threaded
    -

### Event Loop

Stack and all that

### Event Listeners

Event propagation (bubbling & capture)
If you were to add a click event listener to the child and run it, the event will bubble up from child > parent > grandparent.
If you add a capture option to the event listener it will run from the outside, so the opposite of bubbling.

#### Code Example

```
<div class="grandparent">
    <div class="parent">
        <div class="child">
        </div>
    </div>
</div>
```

### Closures

A closure is a function that captures or "closes over" variables defined in it's lexical scope.
Lexical scope being the scope that the function has access to.

#### Code Example

```

// Inner function has access to the outer variable of tax and closes over it
const shippingTax = (tax) => {
    const taxRate = (amount) => {
        return amount - tax
    }

    return taxRate
}

// Run the shippingTax function which sets the tax variable inside taxRate to 30
// Taxrate closes over the tax variable from the outer scope and is returned and thus assigned to tax30
const tax30 = shippingTax(30)

// tax30 is now the taxRate function
// Calls taxRate with the amount which will return the amount - the fixed tax rate of 30
tax30(500)

```
