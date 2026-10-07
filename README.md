# JavaScript Interview Questions

Simple, beginner-friendly solutions to 12 common JavaScript coding interview questions.
Every solution uses basic loops and objects — easy to read, easy to remember, and easy to explain in an interview.

## Table of Contents

1. [Reverse a String](#1-reverse-a-string)
2. [Palindrome Check](#2-palindrome-check)
3. [Largest and Smallest in an Array](#3-largest-and-smallest-in-an-array)
4. [Find Duplicates in an Array](#4-find-duplicates-in-an-array)
5. [Second-Largest Element](#5-second-largest-element)
6. [Prime Number Check](#6-prime-number-check)
7. [Fibonacci Series](#7-fibonacci-series)
8. [Factorial Using Recursion](#8-factorial-using-recursion)
9. [Anagram Check](#9-anagram-check)
10. [Character Frequency](#10-character-frequency)
11. [Missing Number from 1 to N](#11-missing-number-from-1-to-n)
12. [Two Sum](#12-two-sum)

- [Complexity Cheat Sheet](#complexity-cheat-sheet)

---

## 1. Reverse a String

**Question:** Reverse a string without using the built-in `reverse()` function.

**Approach:** Start from the last character and add each one to a new string.

```javascript
function reverseString(str) {
  let reversed = '';
  for (let i = str.length - 1; i >= 0; i--) {
    reversed = reversed + str[i];
  }
  return reversed;
}

console.log(reverseString('hello')); // "olleh"
```

**Complexity:** O(n) time, O(n) space

---

## 2. Palindrome Check

**Question:** Check whether a given string or number is a palindrome.

**Approach:** Reverse it and compare with the original. `String(value)` makes it work for numbers too.

```javascript
function isPalindrome(value) {
  const str = String(value);
  let reversed = '';
  for (let i = str.length - 1; i >= 0; i--) {
    reversed = reversed + str[i];
  }
  return str === reversed;
}

console.log(isPalindrome('madam')); // true
console.log(isPalindrome(12321)); // true
console.log(isPalindrome('hello')); // false
```

**Complexity:** O(n) time, O(n) space

---

## 3. Largest and Smallest in an Array

**Question:** Find the largest and smallest elements in an array.

**Approach:** Start with the first element as both min and max, then loop once and update them.

```javascript
function findMinMax(arr) {
  let min = arr[0];
  let max = arr[0];
  for (let i = 1; i < arr.length; i++) {
    if (arr[i] > max) max = arr[i];
    if (arr[i] < min) min = arr[i];
  }
  return { min, max };
}

console.log(findMinMax([12, 4, 89, -3, 45, 7])); // { min: -3, max: 89 }
```

**Complexity:** O(n) time, O(1) space

**Tip:** Start with `arr[0]`, not `0` — otherwise an all-negative array gives the wrong max.

---

## 4. Find Duplicates in an Array

**Question:** Find the duplicate elements in an array.

**Approach:** Count each number in an object. When a count reaches 2, it is a duplicate.

```javascript
function findDuplicates(arr) {
  const count = {};
  const duplicates = [];
  for (const num of arr) {
    count[num] = (count[num] || 0) + 1;
    if (count[num] === 2) {
      duplicates.push(num);
    }
  }
  return duplicates;
}

console.log(findDuplicates([1, 2, 3, 2, 4, 5, 1, 1])); // [2, 1]
```

**Complexity:** O(n) time, O(n) space

---

## 5. Second-Largest Element

**Question:** Find the second-largest element in an array without sorting.

**Approach:** Track the largest and second-largest in one loop. When a new largest appears, the old largest becomes second.

```javascript
function secondLargest(arr) {
  let largest = -Infinity;
  let second = -Infinity;
  for (const num of arr) {
    if (num > largest) {
      second = largest;
      largest = num;
    } else if (num > second && num < largest) {
      second = num;
    }
  }
  return second;
}

console.log(secondLargest([12, 35, 1, 10, 34, 1])); // 34
```

**Complexity:** O(n) time, O(1) space

---

## 6. Prime Number Check

**Question:** Check whether a given number is prime.

**Approach:** A prime has no divisors other than 1 and itself. Checking divisors up to √n is enough.

```javascript
function isPrime(n) {
  if (n < 2) return false;
  for (let i = 2; i * i <= n; i++) {
    if (n % i === 0) return false;
  }
  return true;
}

console.log(isPrime(29)); // true
console.log(isPrime(10)); // false
```

**Complexity:** O(√n) time, O(1) space

---

## 7. Fibonacci Series

**Question:** Print the first N numbers of the Fibonacci series.

**Approach:** Keep two variables. Each new number is the sum of the previous two.

```javascript
function fibonacci(n) {
  let a = 0;
  let b = 1;
  const result = [];
  for (let i = 0; i < n; i++) {
    result.push(a);
    const next = a + b;
    a = b;
    b = next;
  }
  return result;
}

console.log(fibonacci(10)); // [0, 1, 1, 2, 3, 5, 8, 13, 21, 34]
```

**Complexity:** O(n) time, O(n) space

---

## 8. Factorial Using Recursion

**Question:** Find the factorial of a number using recursion.

**Approach:** Base case: 0! = 1! = 1. Otherwise, n! = n × (n − 1)!.

```javascript
function factorial(n) {
  if (n <= 1) return 1;
  return n * factorial(n - 1);
}

console.log(factorial(5)); // 120
```

**Complexity:** O(n) time, O(n) space (call stack)

---

## 9. Anagram Check

**Question:** Check whether two strings are anagrams of each other.

**Approach:** Sort the letters of both strings. If the sorted strings match, they are anagrams.

```javascript
function isAnagram(str1, str2) {
  const sorted1 = str1.toLowerCase().split('').sort().join('');
  const sorted2 = str2.toLowerCase().split('').sort().join('');
  return sorted1 === sorted2;
}

console.log(isAnagram('listen', 'silent')); // true
console.log(isAnagram('hello', 'world')); // false
```

**Complexity:** O(n log n) time, O(n) space

**Tip:** If asked for something faster, count letters with an object instead of sorting — that is O(n).

---

## 10. Character Frequency

**Question:** Count the frequency of each character in a string.

**Approach:** Loop through the string and keep a count for each character in an object.

```javascript
function charFrequency(str) {
  const freq = {};
  for (const ch of str) {
    if (freq[ch]) {
      freq[ch]++;
    } else {
      freq[ch] = 1;
    }
  }
  return freq;
}

console.log(charFrequency('banana')); // { b: 1, a: 3, n: 2 }
```

**Complexity:** O(n) time, O(k) space (k = number of unique characters)

---

## 11. Missing Number from 1 to N

**Question:** Find the missing number in an array containing numbers from 1 to N.

**Approach:** The total of 1 to N is N × (N + 1) / 2. Subtract the array's sum; what is left is the missing number.

```javascript
function findMissing(arr, n) {
  const expected = (n * (n + 1)) / 2;
  let actual = 0;
  for (const num of arr) {
    actual = actual + num;
  }
  return expected - actual;
}

console.log(findMissing([1, 2, 4, 5, 6], 6)); // 3
```

**Complexity:** O(n) time, O(1) space

---

## 12. Two Sum

**Question:** Given an array and a target, find two numbers whose sum equals the target.

**Approach:** Check every pair with two loops and return the pair whose sum equals the target.

```javascript
function twoSum(nums, target) {
  for (let i = 0; i < nums.length; i++) {
    for (let j = i + 1; j < nums.length; j++) {
      if (nums[i] + nums[j] === target) {
        return [nums[i], nums[j]];
      }
    }
  }
  return null;
}

console.log(twoSum([2, 7, 11, 15], 9)); // [2, 7]
```

**Complexity:** O(n²) time, O(1) space

**Tip:** Interviewers often ask for a faster version: store each number in an object and check whether `target - num` was already seen. That is O(n).

---

## Complexity Cheat Sheet

| #   | Problem        | Technique           | Time       | Space |
| --- | -------------- | ------------------- | ---------- | ----- |
| 1   | Reverse string | Reverse loop        | O(n)       | O(n)  |
| 2   | Palindrome     | Reverse and compare | O(n)       | O(n)  |
| 3   | Min and max    | Single loop         | O(n)       | O(1)  |
| 4   | Duplicates     | Count object        | O(n)       | O(n)  |
| 5   | Second largest | Two variables       | O(n)       | O(1)  |
| 6   | Prime check    | Divisors up to √n   | O(√n)      | O(1)  |
| 7   | Fibonacci      | Loop                | O(n)       | O(n)  |
| 8   | Factorial      | Recursion           | O(n)       | O(n)  |
| 9   | Anagram        | Sort and compare    | O(n log n) | O(n)  |
| 10  | Char frequency | Count object        | O(n)       | O(k)  |
| 11  | Missing number | Sum formula         | O(n)       | O(1)  |
| 12  | Two Sum        | Two loops           | O(n²)      | O(1)  |

---
