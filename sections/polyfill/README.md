# Polyfill

## .filter() polyfill

```js
Array.prototype.myFilter = function (cb) {
  const temp = [];

  for (let index = 0; index < this.length; index++) {
    if (cb(this[index], index)) temp.push(this[index]);
  }

  return temp;
};

const arr = [1, 2, 3];
const res = arr.myFilter((item) => item < 2);

console.log(res); // [1]
```

## .reduce() polyfill

```js
Array.prototype.myReduce = function (cb, initialValue) {
  let accumulator = initialValue;

  for (let index = 0; index < this.length; index++) {
    accumulator = cb(accumulator, this[index]);
  }

  return accumulator;
};

const arr = [1, 2, 3];

const res = arr.myReduce((accumulator, current) => accumulator + current, 0);
console.log(res); // 6
```

## promise.all() polyfill

```js
function task1() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("Task one resolved");
    }, 1000);
  });
}

function task2() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("Task two resolved");
    }, 2000);
  });
}

myAllPromise([task1, task2])
  .then((response) => console.log(response))
  .catch((err) => console.log(err));

function myAllPromise(tasks) {
  const results = [];
  let countResolved = 0;

  return new Promise((resolve, reject) => {
    tasks.forEach((task, index) => {
      task()
        .then((resp) => {
          results.push(resp);
          countResolved++;

          if (countResolved === tasks.length) {
            resolve(results);
          }
        })
        .catch((err) => {
          reject(err);
        });
    });
  });
}
```

## promise.allSettled() polyfill

```js
function task1() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("Task one resolved");
    }, 1000);
  });
}

function task2() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      reject("Task two rejected");
    }, 1000);
  });
}

myAllSettledPromise([task1, task2])
  .then((response) => console.log(response))
  .catch((err) => console.log(err));

function myAllSettledPromise(tasks) {
  const results = [];
  let count = 0;

  return new Promise((resolve, reject) => {
    tasks.forEach((task, index) => {
      task()
        .then((resp) => {
          results.push(resp);
          count++;
          if (count === tasks.length) {
            resolve(results);
          }
        })
        .catch((err) => {
          results.push(err);
          count++;
          if (count === tasks.length) {
            resolve(results);
          }
        });
    });
  });
}
```
