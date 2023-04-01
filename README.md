# js-interview-preparation

This is a preparation guide for your next JavaScript Interview. You will learn some essential concepts that will help you to understand JS as well as pass interviews.

### Table of Contents

<details>

<summary><b>Expand Table of Contents</b></summary>

- [Section 1: this keyword](#section-1-this-keyword)
- [Section 2: Bind, Call and Apply](#section-2-bind-call-and-apply)
- [Section 3: ProtoType](#section-3-prototype)
- [Section 4: Function](#section-4-function)
- [Section 5: Hoisting]
- [Section 6: Closure]
- [Section 7: Problem Solving](#section-7-problem-solving)
- [Section 8: Polyfill](#section-8-polyfill)

</details>

# Section 1: this keyword

In JavaScript this keyword means reference of its context.

## this inside global or window object

```js
console.log(this);
// window { 0: global, window: Window }
```

🔗 [**Learn More**](./sections/this/README.md)

# Section 2: Bind, Call and Apply

```js
const person = {
  firstName: "John",
  lastName: "Doe",
  fullName: function () {
    return this.firstName + " " + this.lastName;
  },
};

const member = {
  firstName: "Muhammad",
  lastName: "Lahin",
};

let fullName = person.fullName.bind(member);
fullName(); // Muhammad Lahin
```

.bind() method creates a new function called fullName(), and change the person object's this context to newly created member object's this context.

```js
const person = {
  firstName: "John",
  lastName: "Doe",
  fullName: function (age) {
    return `${this.firstName} ${this.lastName} age is ${age}`;
  },
};

const member = {
  firstName: "Muhammad",
  lastName: "Lahin",
};

person.fullName.call(member, 24); // Muhammad Lahin age is 24
```

.call() method calls a function with a given this context value and arguments provided individually.

```js
const person = {
  firstName: "John",
  lastName: "Doe",
  fullName: function (age, birthYear) {
    return `${this.firstName} ${this.lastName} age is ${age} birth year is ${birthYear}`;
  },
};

const member = {
  firstName: "Muhammad",
  lastName: "Lahin",
};

person.fullName.apply(member, [24, 1994]); // Muhammad Lahin age is 24 birth year is 1994
```

.apply() method invokes the function on given context and allows to pass arguments as an array.

In general Call and Apply both are similar only difference is the way they get arguments.

# Section 3: ProtoType

## What is ProtoType?

Each Object and Array contains a property or object called [[Prototype]]. Which indicated to the prototype of that object, this can be null or points to another object.

## What is `__proto__`?

[[Prototype]] is an internal property that cannot be accessed directly, so we have `__proto__` in order to access that prototype.

# Section 4: Function

## Function Statement

If function starts with function keyword then this is Function Statement.

```js
function add(a, b) {}
```

## Function Expression

You can assign function into variable and this is Function Expression.

```js
const add = function (a, b) {};
```

## Difference between Function Statement & Function Expression

The difference between them is Hoisting.

# Section 7: Problem Solving

## Check if a string is Pangram or not

Means if string consist 26 english alphabets or not.

```js
const str = "The quick brown fox jumps over the lazy dog";

function isPangram(text) {
  const tracks = new Array(26).fill(false);
  let index;

  for (let i = 0; i < text.length; i++) {
    if (text[i] >= "A" && text[i] <= "Z") {
      index = text.charCodeAt(i) - "A".charCodeAt(0);
    } else if (text[i] >= "a" && text[i] <= "z") {
      index = text.charCodeAt(i) - "a".charCodeAt(0);
    }

    tracks[index] = true;
  }

  return tracks.every((track) => track === true);
}

console.log(isPangram(str)); // true
```

🔗 [**Learn More**](./sections/problem-solving/README.md)

# Section 8: Polyfill

## .map() polyfill

```js
Array.prototype.myMap = function (cb) {

    let temp = [];

    for(let index = 0; index < this.length; index++) { // this - is the actual object that is currently attached with myMap parent
        temp.push(cb(this[index], index);
    }

    return temp;

}

const arr = [1, 2, 3];
const res = arr.myMap(item => item * 2);

console.log(res); // [2, 4, 6]
```

🔗 [**Learn More**](./sections/polyfill/README.md)
