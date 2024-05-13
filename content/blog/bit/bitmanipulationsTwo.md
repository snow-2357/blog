---
title: Bit Manipulations II.
description: A bitmask allows focusing on specific bits within a number. By setting a single bit in a mask and performing bitwise operations with it and another number,only the corresponding bit positions are affected. For instance, to isolate the 2nd bit of a number x, a mask is shifted left twice. Checking if the 2nd bit is set involves using the AND operation between the mask and x; if the result is non-zero, the bit is flipped. To flip the 2nd bit of x, a bitwise XOR operation between the mask and x is executed, leaving other bits unchanged. XORing with 0 preserves x, while XORing with 1 flips it
date: 2024-05-11
tags:
  - dsa
  - basic
  - bit
  - bitmask
---

## BitMask

A **_bitmask_** allows focusing on specific bits within a number. By setting a single bit in a mask and performing bitwise operations with it and another number, _only the corresponding bit positions are affected_. For instance, to isolate the 2nd bit of a number x, a mask is shifted left twice. Checking if the 2nd bit is set involves using the AND operation between the mask and x; if the result is non-zero, the bit is flipped. To flip the 2nd bit of x, a bitwise XOR operation between the mask and x is executed, leaving other bits unchanged. XORing with 0 preserves x, while XORing with 1 flips it. [for more](/blog/bitmanipulationsOne)

---

#### _q1_. Given a non-empty array of integers nums, every element appears twice except for one. Find that single one.

<a href="https://leetcode.com/problems/single-number/description/" target="_blank">Leet code</a>

Input: [2, 3, 4, 3, 2]

Output: 4

- Approach : **_Using bitwise XOR operator_**
  - To understand this approach lets see with a example:

```js
  A = [2,3,4,3,2]

  2 - 0   1   0
  3 - 0   1   1
  4 - 1   0   0
  3 - 0   1   1
  2 - 0   1   0
  ^  -----------
      1   0   0  -> 4

```

- Explain :

  - From the above example, we can see that those elements occurring twice don't contribute to the bits in the solution. Therefore, we can use XOR to remove those elements occurring twice.

> Note: We can also count the number of set bits and then take the mod of the count by 2. This approach will be valuable for future questions.

- Algorithm :
  - Traverse the array and take the Bitwise XOR of each element.
  - Return the value.
- Code:

```js
const singleNumber(nums){
  let sol = 0;
  for(let i of nums){
    sol ^= i;
  }
  return sol;
}
```

- Time and Space Complexity
  - TC - O(N)
  - SC - O(1)

---

#### _q2_. Given an integer array, all the elements will occur twice except two. Find those two elements.

<a href="https://leetcode.com/problems/single-number-iii/description/" target="_blank">Leet code</a>

Input: [4, 5, 4, 1, 6, 6, 5, 2]

Output: 1, 2

- Approach :
  - Suppose if two unique numbers are a and b. Their XOR is c.
  - We will find the position of any set bit in XOR c, it will denote that this bit is different in a and b. (1 xor 0 = 1)
  - Now, we divide the entire array in two groups, based upon whether that particular bit is set or not.
  - This way a and b will fall into different groups.
  - Now since every number repeats twice, they will cancel out when we take XOR of the two groups individually leaving a and b.
- Explain:
  - For the array [4, 5, 4, 1, 6, 6, 5, 2], the xor of all the number is **3**.
  - We can choose any bit position since 3 has 2 set bits. Let's pick position **1**.
  - Position 1 is set for the numbers [6, 6, 2].
  - Position 1 is unset for the numbers [4, 5, 4, 1, 5].
  - Now, we can find both of the unique numbers by following the **_q1_**.
- Algorithm :
  - Traverse the array and take the Bitwise XOR of each element.
  - Identify one set bit position in the resulting XOR value.
  - Divide the array into two parts based on whether the elements have the set bit at the identified position or not.
  - Compute the XOR of each part separately; each XOR result will provide one of the solutions.
- Code:

```js
var singleNumber = function (nums) {
	if (nums.length == 2) return nums;

	let xor = 0;

	for (let num of nums) {
		xor ^= num;
	}

	let pos = 0;
	while ((xor & (1 << pos)) === 0) {
		pos++;
	}

	let sol = [0, 0];

	for (let num of nums) {
		if ((num & (1 << pos)) !== 0) {
			sol[0] ^= num;
		} else {
			sol[1] ^= num;
		}
	}

	return sol;
};
```

- Time and Space Complexity
  - TC - O(N)
  - SC - O(1)

#### _q3_. Given N array elements, choose two indices(i, j) such that (i != j) and (arr[i] & arr[j]) is maximum.

Input: [5, 4, 6, 8, 5]

Output: [0, 4]

> If we take the & of 5 with 5, we get 5 which is the maximum possible value here. The required answer would be their respective indices i.e. 0,4

- Observation :
  - When bit is set in both the numbers, that bit in their & will be 1
  - For the maximum answer, we want more set bits in the most significant bits (MSB) on the left side.
- Algorithm :
  - Iterate from the MSB to the LSB for all numbers, keeping a count if we find a set bit in the number at the current bit position.
  - If the count is greater than 1, we can form a pair and ignore the rest of the elements.
  - If the count is either 0 or 1, we do not care at the moment and just iterate to the next bit position.
- Code:

```js
var maxPair = function (nums) {
	let sol = 0;
	for (let i = 31; i >= 0; i++) {
		let count = 0;
		for (let j = 0; j < nums.length; i++) {
			if (arr[j] & (1 << i)) count++;
		}
		if (count > 1) {
			sol = sol | (1 << i); // setting the bit in sol
		}
		for (let j = 0; j < nums.length; i++) {
			if (!(arr[j] & (1 << i))) arr[j] = 0; // ignoring them bc they cant make a large number
		}
	}
};
```

- Time and Space Complexity
  - TC - O(N)
  - SC - O(1)
- Dry Run

```js
A = [15, 14, 6, 8, 5, 7, 13]

 15 - 1  1  1  1
 14 - 1  1  1  0
  8 - 1  0  0  0
  5 - 0  1  0  1
  7 - 0  1  1  1
 13 - 1  1  0  1
 i=3
 ----------------
 count = 4


 15 - 1  1  1  1
 14 - 1  1  1  0
  8 - 1  0  0  0
 13 - 1  1  0  1
 i=2
 ----------------
 count = 3


 15 - 1  1  1  1
 14 - 1  1  1  0
 13 - 1  1  0  1
 i=2
 ----------------
 count = 2

 15 - 1  1  1  1
 14 - 1  1  1  0

```

> Following this algo we can also solve for max AND of Triplets, quadruples, etc

- **Extra Leetcode Problems**

  - [Add Binary](https://leetcode.com/problems/add-binary/description/)
  - [Reverse Bits](https://leetcode.com/problems/reverse-bits/description/)
  - [Counting Bits](https://leetcode.com/problems/counting-bits/description/)
  - [No of 1bits](https://leetcode.com/problems/number-of-1-bits/description/)
  - [Single Number II](https://leetcode.com/problems/single-number-ii/description/)
  - [Bitwise AND of Numbers Range](https://leetcode.com/problems/bitwise-and-of-numbers-range/description/)
  - [Minimum Flips to Make a OR b Equal to c](https://leetcode.com/problems/minimum-flips-to-make-a-or-b-equal-to-c/description/)
