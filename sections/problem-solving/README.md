# Problem Solving

## Check two strings anagram or not

```js
const value1 = "Hussain";
const value2 = "rumhnee";

const checkAnagram = (str1, str2) => {
  let sort1 = str1.split("").sort().join("");
  let sort2 = str2.split("").sort().join("");

  if (sort1 !== sort2) {
    return false;
  }

  return true;
};

console.log(checkAnagram(value1, value2)); // true
```

## Create a Debounce Function

```js
function debounce(fn, delay) {
  let timer;
  return function () {
    if (timer) {
      clearTimeout(timer);
    }
    timer = setTimeout(() => {
      fn();
    }, delay);
  };
}
```

## Find the Longest Consecutive Charecter in a given string

```js
const longestConsecutiveChar = (str) => {
  let track = { char: "", count: 0 };
  let result = { chat: "", count: 0 };

  for (let i = 0; i < str.length; i++) {
    if (track.char !== str[i]) {
      track.char = str[i];
      track.count = 1;
    } else if (track.char === str[i]) {
      track.count++;
    }

    if (track.count > result.count) {
      result = { ...track };
    }
  }

  return result.char;
};

console.log(longestConsecutiveChar("aabbb")); // b
console.log(longestConsecutiveChar("aaabb")); // a
```

## Find if a string contains duplicate or not

```js
const isDuplicate = (str) => {
  const map = new Map();

  for (let item of str) {
    if (map.has(item)) { // the time complexity for .has is O(1)
      return true;
    }
    map.set(item, true);
  }

  return false;
};

console.log(isDuplicate("11223")); // true
console.log(isDuplicate("12345")); // false
```

## Two Sum 

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

Input: nums = [2,7,11,15], target = 9

Output: [0,1]

```js
function twoSum(arr, target) {
  let track = {};
  let res = null;

  for (let i = 0; i < arr.length; i++) {
    let sub = target - arr[i];

    if (track.hasOwnProperty(arr[i])) {
      res = [track[arr[i]], i];
      break;
    }

    track[sub] = i;
  }

  return res;
}

console.log(twoSum([2,7,11,15], 9)); // [0, 1]
```

## Retry API after a specific type

```js
const makeRandom = (min, max) =>
  Math.floor(Math.random() * (max - min + 1)) + min;

const retryAPI = (fetcher, maxRetryCount) => {
  return new Promise((resolve, reject) => {
    let retries = 0;
    const caller = () => {
      fetcher("lahin31")
        .then((data) => {
          resolve(data);
        })
        .catch((err) => {
          if (retries < maxRetryCount) {
            retries++;
            
            const retryAfter = makeRandom(1000, 5000);

            setTimeout(() => {
              console.log("Retrying in " + retryAfter + " seconds");

              caller();
            }, retryAfter);
          } else {
            reject(err);
          }
        });
    };
    retries = 1;
    caller();
  });
};

const fetchGithub = async (username) => {
  const response = await fetch(`https://api.github.com/users/${username}`);
  const data = await response.json();
  return data;
};

retryAPI(fetchGithub, 5);
```
