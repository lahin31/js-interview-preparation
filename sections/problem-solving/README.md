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
const longestConsecutiveChar = str => {
  let track = { char: "", count: 0 };

  for (let i = 0; i < str.length; i++) {
    if (track.char !== str[i]) {
      track.char = str[i];
      track.count = 1;
    } else if (track.char === str[i]) {
      track.count++;
    }
  }

  return track.char;
};

console.log(longestConsecutiveChar("aaaabbcccc")); // a
```
