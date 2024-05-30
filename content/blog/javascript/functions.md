---
title: Function.
description: A JavaScript function is a block of code designed to perform a particular task. A JavaScript function is executed when "something" invokes it (calls it).
date: 2024-05-29
tags:
  - javascript
  - basic
  - concept
---

## Functions

#### Function Declaration

```js
function fun() {
	//
}
```

#### Function Expression

```js
const fun = function () {
	//
};
```

#### First-Class function

- In JavaScript, functions are first-class citizens. This means functions can be treated like any other variable. Specifically, functions can be:

  1. Assigned to a variable:

  ```js
  const greet = function () {
  	console.log("Hello, World!");
  };
  greet(); // Output: Hello, World!
  ```

  2. Passed as arguments to other functions:

  ```js
  function callFunction(fn) {
  	fn();
  }

  function sayHello() {
  	console.log("Hello!");
  }

  callFunction(sayHello); // Output: Hello!
  ```

  3. Returned from other functions:

  ```js
  function createGreeter(greeting) {
  	return function (name) {
  		console.log(greeting + ", " + name);
  	};
  }

  const greeter = createGreeter("Hello");
  greeter("Alice"); // Output: Hello, Alice
  ```

#### IIFE

- Immediately Invoked Function Expression
- An IIFE is a function that is defined and executed simultaneously. This technique is often used to create a private scope and avoid polluting the global namespace.

```js
(function () {
	///
})();
```

- Major use of IIFE is initializing code that needs to run immediately and only once, **_setup routines, configuration settings, and initial connections, such as those to a database_**.
- Variable and functions inside a iife aren't accessible from outside , so it prevents potential errors or conflicts.

#### Callback Function

- A callback function is a function that is passed as an argument to another function and is executed inside that function.

  - passed as an argument
  - called inside another function

  ```js
  function fun1(str, cb) {
  	return cb(str);
  }
  function fun2(str) {
  	console.log(str);
  }

  fun1("sima", fun2);
  ```

Use cases : Asynchronous Operations, Array Methods, Timers, etc

##### Callback Hell

- Callback hell refers to the situation where multiple nested callback functions are called, which often happens during the handling of asynchronous operations. This nesting can make the code difficult to read, debug, and maintain. It creates problems such as:
  - Readability
  - Error handling
  - Scalability

```js
doSomething(function (result1) {
	doSomethingElse(result1, function (result2) {
		doAnotherThing(result2, function (result3) {
			doYetAnotherThing(result3, function (result4) {
				// Final callback
				console.log("Final result: ", result4);
			});
		});
	});
});
```

##### Solutions to Callback Hell

- Using Promises:

```js
doSomething()
	.then((result1) => doSomethingElse(result1))
	.then((result2) => doAnotherThing(result2))
	.then((result3) => doYetAnotherThing(result3))
	.then((result4) => {
		console.log("Final result: ", result4);
	})
	.catch((error) => {
		console.error("Error: ", error);
	});
```

- use async/await

```js
async function executeTasks() {
	try {
		const result1 = await doSomething();
		const result2 = await doSomethingElse(result1);
		const result3 = await doAnotherThing(result2);
		const result4 = await doYetAnotherThing(result3);
		console.log("Final result: ", result4);
	} catch (error) {
		console.error("Error: ", error);
	}
}

executeTasks();
```

> Both approaches significantly improve the readability and maintainability of asynchronous code compared to traditional callback patterns.

#### Arrow function

```js
const greet = () => {
	console.log("Greetings!");
};
```

- Arrow functions have lexical scope, meaning they are bound to the scope in which they are defined. This implies that they inherit the this value from their surrounding code, unlike regular functions that have their own this binding.
- It's essential to define arrow functions before using them to avoid reference errors.
- Arrow functions have an implicit binding with this. This means that they do not have their own this context, they inherit this from parents.
  > The scope defines which part of the code can access a variable, and lexical scope means that this is determined by the variable's location in the source code.
