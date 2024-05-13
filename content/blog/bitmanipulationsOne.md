---
title: Bit Manipulations I.
description: .
date: 2024-05-10
tags:
  - dsa
  - basic
  - bit
  - bitmask
---

## Bit Manipulation Basics

Bit manipulation is a powerful tool that can significantly improve the complexity of algorithms in clever ways. It involves looking at data in binary form and manipulating the individual "bits" in this binary representation. Here are some of the most important operations you need to know:

- **OR (|):**

  - If any bit is 1, then the result will be 1. Otherwise, the result is 0.

- **AND (&):**

  - If all bits are 1, then the result will be 1. Otherwise, the result is 0.

- **XOR (^):**

  - If the number of 1 bits is odd, then the result will be 1. Otherwise, the result is 0.

- **Left Shifts (<<):**

  - The left shift operator (<<) shifts the bits of a number to the left by a specified number of positions.
  - The left shift operator can be used to multiply a number by \(2^n\), where \(n\) is the specified number of positions.

```js
  a << n = a * 2^n
  1 << n = 2^n
```

> Note: Left shift can overflow when exceeding the upper limit.

- **Right Shifts (>>):**
  - The left shift operator (<<) shifts the bits of a number to the left by a specified number of positions.
  - The left shift operator can be used to multiply a number by \(2^n\), where \(n\) is the specified number of positions.

```js
 a >> n = a / 2^n
```

---

### Basic AND OR XOR Properties

- **Even / Odd Number :**

  - in binary, for a even number the least significant bit (LSB) will always be a 0 (unset)
  - Conversely, if a number is odd, then its LSB is 1(set)

```js
x = N & 1;
```

- **Check if nth bit is set or not :**

  - We can easily check whether a number's ith bit is set or not by performing a bitwise AND operation with **_1 << i_**, where **_i_** is the position of the bit. This operation means **_000...1...000_** where 1 is at the ith position. If our number's ith bit is not set, it will return **_0_**.

```js
N = N & (1 << i);
```

Example :

```js
    1 0 1 1 0 1
  & 0 0 0 1 0 0  ->  1<<2
    -----------
    0 0 0 1 0 0   >  0

    1 0 1 1 0 1
  & 0 1 0 0 0 0  ->  1<<4
    -----------
    0 0 0 0 0 0  ==  0
```

- **Set ith Bit :**

  - We can **set** a number's ith bit by performing a bitwise OR operation with **_1 << i_**, where **_i_** is the position of the bit.

```js
N = N | (1 << i);
```

Example :

```js
    1 0 1 1 0 1
  | 0 0 0 1 0 0  ->  1<<2
    -----------
    1 0 1 1 0 1

    1 0 1 1 0 1
  | 0 1 0 0 0 0  ->  1<<4
    -----------
    1 1 1 1 0 1
```

- **Toggle ith Bit :**

  - We can **toggle** a number's ith bit by performing a bitwise XOR operation with **_1 << i_**, where **_i_** is the position of the bit.
  - This operation flips the ith bit of the number. If the bit was originally 0, it becomes 1, and if it was originally 1, it becomes 0. This is because XORing a bit with 1 toggles its value: 0 XOR 1 results in 1, and 1 XOR 1 results in 0.

```js
N = N ^ (1 << i);
```

Example :

```js
    1 0 1 1 0 1
  ^ 0 0 0 1 0 0  ->  1<<2
    -----------
    1 0 1 0 0 1

    1 0 1 1 0 1
  ^ 0 1 0 0 0 0  ->  1<<4
    -----------
    1 1 1 1 0 1
```

### Useful Utils :

- **Unset the ith bit of a Number**

```js
function checkBit(N, i) {
	return !(N & (1 << i)) == 0;
}

function unsetBit(N, i) {
	if (checkBit(N, i)) {
		N = N ^ (1 << i);
	}
}
```

- **Count the no of set bits in a Int**

```js
function countBit(N) {
	let count = 0;
	for (let i = 0; i < 32; i++) {
		if ((N & (1 << i)) > 0) {
			count++;
		}
	}
	return count;
}
```
