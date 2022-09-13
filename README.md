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
- [Section 6: Problem Solving](#section-6-problem-solving)

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

# Section 6: Problem Solving

## Check if a string is Pangram or not

Means if string consist 26 english alphabets or not.

```js
const str = "The quick brown fox jumps over the lazy dog";

function isPangram(text) {
    const tracks = new Array(26).fill(false);
    let index;

    for(let i = 0; i < text.length; i++) {
        if(text[i] >= 'A' && text[i] <= 'Z') {
            index = text.charCodeAt(i) - 'A'.charCodeAt(0);
        } else if(text[i] >= 'a' && text[i] <= 'z') {
            index = text.charCodeAt(i) - 'a'.charCodeAt(0);
        }

        tracks[index] = true;
    }

    return tracks.every(track => track === true)
}

console.log(isPangram(str)); // true
```

## Check two strings anagram or not

```js
const value1 = "meherun";
const value2 = "rumhnee";

const checkAnagram = (str1, str2) => {
    let sort1 = str1.split('').sort().join('');
    let sort2 = str2.split('').sort().join('');

    if(sort1 !== sort2) {
        return false;
    }

    return true;
}

console.log(checkAnagram(value1, value2)); // true
```