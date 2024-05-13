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
  let sol = 0
  for(let i of nums){
    sol ^= i
  }
  return sol
}
```

---

#### _q2_. Given an integer array, all the elements will occur twice except two. Find those two elements.

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
