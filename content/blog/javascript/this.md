---
title: this
description: The this keyword in JavaScript is a special identifier that behaves differently depending on the context in which it's used. Understanding this can be tricky, but it's crucial for writing effective JavaScript.
date: 2024-05-31
tags:
  - javascript
  - basic
  - concept
---

The this keyword in JavaScript is a special identifier that behaves differently depending on the context in which it's used. Understanding this can be tricky, but it's crucial for writing effective JavaScript

- In a normal function, this keeps the context of its parent object when the function is called as a method of that object.

```js
const user = {
	name: "Alice",
	greet() {
		console.log(this.name); // this refers to the user obj
	},
};
user.greet(); // Alice
```

- Arrow functions inherit this from their enclosing scope at the time they are defined, not when they are called.
- This means if an arrow function is defined inside another function, it will use the this value from that enclosing function.

```js
const user = {
	name: "Alice",
	greet()=> {
		console.log(this.name); // this refers to the parent "function"
	},
};
user.greet(); //  undefined

```

```js
const user = {
	name: "Alice",
	wrapper() {
		const greet = () => {
			console.log(this.name);
		};
		greet();
	},
};
user.wrapper(); //  Alice
```

> If you have a nested arrow function inside a regular function which is itself inside an object, the arrow function will inherit the context from its immediate parent function, which, in this case, is the function inside the object. This means that the arrow function's this will refer to the object.
>
> Global context: this refers to the global object.
> Function context: this refers to the global object (non-strict mode) or undefined (strict mode).
> Method context: this refers to the object that the method is called on.
> Constructor context: this refers to the newly created object.
> Arrow functions: this is inherited from the parent scope.
