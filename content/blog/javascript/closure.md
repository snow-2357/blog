---
title: Closure.
description: Closures are created every time an inner function is defined within an outer function, capturing the lexical scope of the outer function
date: 2024-05-29
tags:
  - javascript
  - basic
  - concept
---

### Closures

- Closures are created every time an inner function is defined within an outer function, capturing the lexical scope of the outer function.
- This captured scope includes any variables that were in scope at the time the closure was created, allowing the inner function to access those variables even after the outer function has finished executing.

```js
function fun() {
	let x = 1;
	function fun1() {
		console.log(x);
	}
	return fun1;
}

let fun2 = fun();
fun2(); //1
```

- Private variable
  - Closures can be used to create private variable/ functions

```js
function counter() {
	let count = 0;
	return function () {
		count++;
		return count;
	};
}
```

- Caching
  - We can also cache variable with the help of closure.

```js
function memory(func) {
	let counter = 0;
	return function (...args) {
		counter++;
		console.log("called  " + counter + "  times");
		return func(...args);
	};
}

const add = (a, b) => {
	return a + b;
};

const counterAdd = memory(add);

counterAdd(1, 2);
counterAdd(1, 2);
counterAdd(1, 2);
```
