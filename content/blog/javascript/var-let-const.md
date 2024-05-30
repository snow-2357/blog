---
title: Var-let-const.
description: In JavaScript, var, let, and const are used to declare variables, but they differ significantly in scope, hoisting, and mutability.
date: 2024-05-29
tags:
  - javascript
  - basic
  - concept
---

### var

- **_var_** was the original method for declaring variables in JavaScript before ES6 introduced _let_ and _const_.
- Variables declared with **_var_** have function scope or global scope, but not block scope. This means they are **visible throughout the entire function** or **globally if declared outside of any function**.
- Variables declared with **_var_** are hoisted to the top of their function or global scope during the **initialization phase**. This means that even if the declaration occurs later in the code, the variable is still accessible (though its value will be undefined until it's actually assigned).
- Variables declared with **_var_** are added as properties of the global object (e.g., **_window_** in browsers, **_global_** in Node.js). This can lead to potential naming conflicts or unintended behavior if not used carefully.

### let

- Variables declared with **_let_** have block scope, meaning they are only accessible within the block where they are defined.
  > This enhances predictability and reduces potential bugs by limiting the scope of variables to where they are needed.
  ```js
  {
  	let x = 1;
  }
  console.log(x); //ReferenceError: x is not defined
  ```
- Variables declared with **_let_** can only be initialized once.
- Variables declared with **_let_** are **hoisted** to the top of their **block scope** (kind similar to var). However, there's a concept called the **_Temporal Dead Zone_** (TDZ) for variables declared with **_let_** and **_const_**. Accessing the variable during this time results in a ReferenceError.
- During the **_initialization phase_** of JavaScript, variables declared with **_let/const_** are allocated memory, but they are placed in the **_Temporal Dead Zone_** until their declaration is reached in the code.

### const

- Everything from **_let_**

  ```js
  const x = 1;
  x = 2; // TypeError: Assignment to constant variable.
  ```

- Declaring a **_const_** variable without providing an initial value results in a **_SyntaxError_**, indicating that const variables must be initialized during declaration.
  ```js
  const y; // SyntaxError: Missing initializer in const declaration
  ```

### TDZ

- Variables declared with **_let_** and **_const_** are hoisted to the top of their scope during the initialization phase, but they **are not initialized until the actual declaration is reached in the code**. Until that point, they exist in a _temporal dead zone_ where they are considered to be uninitialized, and any attempt to access them will throw a ReferenceError.
- This concept is important because it helps prevent issues such as accessing variables before they are declared, promoting cleaner and more predictable code.
