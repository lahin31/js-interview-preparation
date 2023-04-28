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

console.log(twoSum([7, 3, 6, 4], 11)); // [0, 3]
```
