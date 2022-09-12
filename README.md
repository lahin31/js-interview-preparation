# js-interview-preparation

This is a preparation guide for your next JavaScript Interview. You will learn some essential concepts that will help you to pass interview.

### Table of Contents

<details>

<summary><b>Expand Table of Contents</b></summary>

- [Section 1: this keyword](#section-1-this-keyword)
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
// window { 0: global, window: Window }
```

## this inside regular function

```js
function doSomething() {
    this.name = "Meherun";
    console.log(this);
}

doSomething();
// window { 0: global, window: Window, name: Meherun, ... }
```

The parent scope of `doSomething` function is the window object.

## this inside Arrow Function

```js
const doSomething = () => {
    this.name = "Meherun";
    console.log(this); // { name: Meherun }
}

doSomething();
```

If we don't provide any this environment inside `doSomething` function this will go up to its parent context and grab its this.

```js
this.name = "Meherun";
const doSomething = () => {
    console.log(this); // { name: 'Meherun' }
}

console.log(this); // { name: 'Meherun' }

doSomething();
```

## this inside object

example 1: 

```js
const user = {
    name: "Lahin",
    age: 30,
    getInfo() {
        return `Name is ${this.name} and Age is ${this.age}`
    }
}

console.log(user.getInfo()); // Name is Lahin and Age is 30
```

example 2:

```js
const user = {
    name: "Lahin",
    age: 30,
    education: {
        university: "Metropolitan University",
        getInfo() {
            return `${this.name} and your university is ${this.university}`
        }
    }
}

console.log(user.education.getInfo()); // undefined and your university is Metropolitan University
```

`getInfo()` has a parent "this" context inside `education` object not in `user` object thats why this.name is undefined.

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