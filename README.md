# js-interview-preparation

This is a preparation guide for your next JavaScript Interview. You will learn some essential concepts that will help you to pass interview.

### Table of Contents

<details>

<summary><b>Expand Table of Contents</b></summary>

- [Section 1: this keyword](section-1-this-keyword)
- [Section 2: Bind, Call and Apply]
- [Section 3: Function](#section-3-function)
- [Section 4: Hoisting]
- [Section 5: Closure]

</details>

# Section 1: this keyword

In JavaScript this keyword means reference of its context.

## this inside global or window object

```js
console.log(this);
// window {0: global, window: Window}
```

## this inside regular function

```js
function doSomething() {
    this.name = "Meherun";
    console.log(this);
}

doSomething();
// window {0: global, window: Window, name: Meherun, ...}
```

The parent scope of `doSomething` function is the window object. Same goes for Arrow Function also,

```js
const doSomething = function() {
    this.name = "Meherun";
    console.log(this);
}

doSomething();
// window {0: global, window: Window, name: Meherun, ...}
```
# Section 3: Function

## Function Statement

If function starts with function keyword then this is Function Statement.

```js
function add(a, b) {}
```

## Function Expression

You can assign function into variable and this is Function Expression.

```js
const add = function(a, b) {}
```

## Difference between Function Statement & Function Expression

The difference between them is Hoisting.