```markdown
# JavaScript Interview Questions

## 1. What is the difference between `this` in JavaScript when used in strict mode versus non-strict mode?

### Answer:
```javascript
// Non-strict mode
function myFunction() {
  console.log(this); // Output: Window object (or global object)
}

myFunction();

// Strict mode
"use strict";

function myFunction() {
  console.log(this); // Output: undefined
}

myFunction();
```

### Explanation:
- **Non-strict mode:** When `this` is used in a standalone function, it usually refers to the global object (e.g., `window` in a browser).
- **Strict mode:** In strict mode, `this` defaults to `undefined` in a standalone function, helping avoid reliance on the global object.

### Key Points:
- `this` is determined by how a function is called, not where it's declared.
- Arrow functions inherit `this` from the surrounding scope.
- Strict mode introduces stricter rules, making code more robust.

---

## 2. Explain the concept of hoisting in JavaScript.

### Answer:
```javascript
console.log(x); // Output: undefined
var x = 10;
```

### Explanation:
- **Variable Declarations:** In JavaScript, variable declarations (`var`) are hoisted to the top of their scope.
- **Initialization:** The initialization happens later, so accessing the variable before it’s assigned results in `undefined`.

### Key Points:
- Function declarations are hoisted.
- `let` and `const` are hoisted but remain in a "temporal dead zone" before declaration, causing a `ReferenceError`.

---

## 3. What is the difference between `var`, `let`, and `const` in JavaScript?

### Answer:
```javascript
// var: Function scope, can be re-declared and reassigned
var x = 10;
var x = 20; // Re-declared and reassigned

// let: Block scope, cannot be re-declared but can be reassigned
let y = 10;
// let y = 20; // SyntaxError: Identifier 'y' has already been declared
y = 20; // Reassigned

// const: Block scope, cannot be re-declared or reassigned
const z = 10;
// const z = 20; // SyntaxError: Identifier 'z' has already been declared
// z = 20; // TypeError: Assignment to constant variable.
```

### Key Differences:
- **Scope:**
  - `var`: Function-scoped.
  - `let` and `const`: Block-scoped.
- **Redeclaration:**
  - `var`: Can be redeclared.
  - `let` and `const`: Cannot be redeclared within the same scope.
- **Reassignment:**
  - `var` and `let`: Can be reassigned.
  - `const`: Cannot be reassigned.

### Best Practices:
- Use `let` and `const` for better scoping and immutability control.

---

## 4. Explain the difference between synchronous and asynchronous code execution in JavaScript.

### Answer:

**Synchronous Code Execution:**
- Executes line by line, blocking until the current task finishes.
- Example:
  ```javascript
  console.log('Step 1');
  console.log('Step 2');
  console.log('Step 3');
  ```
  Output:
  ```
  Step 1
  Step 2
  Step 3
  ```

**Asynchronous Code Execution:**
- Allows code to execute without waiting for long-running operations.
- Example:
  ```javascript
  console.log('Step 1');

  setTimeout(() => {
    console.log('Step 2 - After 2 seconds');
  }, 2000);

  console.log('Step 3');
  ```
  Output:
  ```
  Step 1
  Step 3
  Step 2 - After 2 seconds
  ```

### Key Points:
- Asynchronous programming allows handling I/O operations (e.g., AJAX requests) without blocking the main thread.

---

## 5. What are unit tests, and why are they important in JavaScript development?

### Answer:

**Unit Tests:**
- Tests small, isolated pieces of code (usually functions or methods).
- Purpose: To verify correctness and ensure that each part of the code functions as expected.

### Key Benefits:
- **Early Bug Detection:** Identifies bugs early, reducing the cost of fixing them.
- **Improved Code Quality:** Encourages writing modular, testable code.
- **Increased Confidence:** Assures that changes do not break existing functionality.

### Example:
```javascript
function add(a, b) {
  return a + b;
}

test('adds 1 + 2 to equal 3', () => {
  expect(add(1, 2)).toBe(3);
});
```

---

## 6. What is the purpose of the Module Pattern in JavaScript?

### Answer:

**Module Pattern:**
- Creates self-contained, modular code with public and private variables/methods.
- Helps with **encapsulation**, **namespace management**, and **code organization**.

### Example:
```javascript
const myModule = (() => {
  let privateVar = 'Hello';

  function privateFunction() {
    console.log(privateVar);
  }

  return {
    publicVar: 'World',
    publicFunction: () => {
      console.log(publicVar + ' ' + privateVar);
    }
  };
})();
```

### Benefits:
- Improved code organization and reduced naming conflicts.
- Public API exposed while keeping implementation details hidden.

---

## 7. Explain the concept of Promises in JavaScript.

### Answer:

**Promises:**
- A promise represents a value that may be available in the future, or an error if something went wrong.
- **States:**
  - **Pending:** Initial state.
  - **Fulfilled:** Operation completed successfully.
  - **Rejected:** Operation failed.

### Example:
```javascript
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('Data fetched');
    }, 1000);
  });
}

fetchData()
  .then(data => console.log(data))
  .catch(error => console.error(error));
```

### Key Points:
- Promises allow for cleaner, more readable asynchronous code compared to callbacks.

---

## 8. What is the Observer Pattern, and how can it be implemented in JavaScript?

### Answer:

**Observer Pattern:**
- Defines a one-to-many dependency where one object (the subject) notifies multiple objects (observers) about changes.

### Example:
```javascript
class Subject {
  constructor() {
    this.observers = [];
  }

  subscribe(observer) {
    this.observers.push(observer);
  }

  unsubscribe(observer) {
    this.observers = this.observers.filter(obs => obs !== observer);
  }

  notify(data) {
    this.observers.forEach(observer => observer.update(data));
  }
}

class Observer {
  update(data) {
    console.log('Observer received:', data);
  }
}

const subject = new Subject();
const observer1 = new Observer();
subject.subscribe(observer1);
subject.notify('Data changed');
```

### Benefits:
- Loose coupling between subject and observers, allowing for easier updates and maintenance.

---

## 9. Can you explain how JavaScript can be used to manipulate the Document Object Model (DOM)?

### Answer:
```javascript
// Access an element by ID
const myElement = document.getElementById('myElementId');

// Change text content
myElement.textContent = 'New text content';

// Modify style
myElement.style.color = 'blue';
myElement.style.fontSize = '20px';

// Add/Remove classes
myElement.classList.add('myClass');
myElement.classList.remove('myClass');

// Create new elements and append them
const newElement = document.createElement('p');
newElement.textContent = 'This is a new paragraph.';
myElement.appendChild(newElement);
```

### Key Points:
- **Accessing Elements:** Methods like `getElementById()`, `querySelector()`.
- **Modifying DOM:** Change content, styles, attributes, or even create new elements.
- **Event Handling:** Attach event listeners to DOM elements for interactivity.

---

This concludes the list of JavaScript interview questions with their answers. These concepts cover essential JavaScript topics that are commonly asked in interviews and help understand how JavaScript works in different scenarios.
```
