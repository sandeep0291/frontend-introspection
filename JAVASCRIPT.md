# JavaScript Interview Question Bank

Listing all the possible JavaScript questions, divided into following types

A. [Fundamentals Theory](#fundamentals-theory)

B. [Fundamentals Practical]()

C. [Advanced Concepts]()

D. [Coding / Array / Objects]()

## Fundamentals Theory

1. ### What are the different data types in JavaScript

    JavaScript has seven built-in data types, which are divided into two categories: primitive types and object types.

    **Primitive Types**

    Primitive types are the most basic types of data in JavaScript. They are immutable (i.e., they cannot be changed) and are copied by value when they are assigned to a variable.

    1. **Number:**

        The Number type represents numeric values. It can be an integer or a floating-point number. For example:

        ```javascript
        let x = 10; // integer
        let y = 3.14; // floating-point number
        ```

    2.  **String:**

        The String type represents a sequence of characters. It is enclosed in single or double quotes. For example:

        ```javascript
        let name = "John"; // single quotes
        let message = "Hello, world!"; // double quote
        ```

    3.  **Boolean:**

        The Boolean type represents a logical value, which can be either true or false. For example

    4.  **Null:**

        The Null type represents a deliberate non-value. It is often used to initialize a variable that will later be assigned a value.

    5.  **Undefined:**

        The Undefined type represents an undefined value. It is used when a variable has been declared but has not been assigned a value. For example:

        ```javascript
        let y;
        console.log(y); // Output: undefined
        ```

    6.  **Symbol:**

        The Symbol type represents a unique identifier. It is often used as a key in object properties.

        ```javascript
        let id1 = Symbol("id");
        let id2 = Symbol("id");
        console.log(id1 === id2); // Output: false  
        ```

2.  ### What is hoisting in JavaScript

    Hoisting is a JavaScript mechanism that moves variable and function declarations to the top of their respective scopes during the compilation phase, allowing variables and functions to be used before they are declared. This can sometimes result in unexpected behavior, especially when combined with closures.

    ```javacript
    console.log(x); // Output: undefined
    var x = 10;
    ```

    ```javacript
    foo(); // Output: "Hello, world!"

    function foo() {
    console.log("Hello, world!");
    ```

    ```javacript
    foo(); // Output: TypeError: foo is not a function

    var foo = function() {
    console.log("Hello, world!");
    };
    ```

    In this example, a function expression is used to create the foo() function. However, when we try to call the function before it has been declared, we get a TypeError instead of a reference error. This is because the variable declaration is hoisted, but the function expression is not.

    ```javacript
    function outer() {
        console.log(x); // Output: undefined

        var x = "Hello, world!";

        function inner() {
            console.log(x); // Output: "Hello, world!"
        }

        inner();
    }

    outer();
    ```

    In this example, the x variable is declared and initialized in the outer function, but when we try to log its value before it has been initialized, we get undefined. However, when we call the inner function, which also has access to the x variable, it logs the correct value of "Hello, world!". This is because the variable declaration is hoisted to the top of its scope, but the assignment is not.

3.  ### What is the difference between `let`, `const`, and `var` in JavaScript

    `let`, `var`, and `const` are all used to declare variables in JavaScript, but they have different scoping rules and behaviors.

    - `var` declarations are function scoped, meaning they are accessible within the function they are declared in or any nested functions. They can also be accessed outside the function if they are declared in the global scope.
    - `let` and `const` are block scoped, meaning they are only accessible within the block they are declared in, such as a loop or conditional statement. The difference between `let` and `const` is that `let` allows the variable to be reassigned, while `const` does not.

    For example:

    ```javacript
    function example() {
    var x = 1;
    let y = 2;
    const z = 3;

    if (true) {
        var x = 4; // same variable as the one declared above
        let y = 5; // different variable than the one declared above
        const z = 6; // different variable than the one declared above
        console.log(x, y, z); // outputs 4, 5, 6
    }

    console.log(x, y, z); // outputs 4, 2, 3
    }

    example();
    ```

    In the above example, `var x` is accessible throughout the entire function, while `let y` and `const z` are only accessible within their respective blocks. When the if statement is entered, a new `let y` and `const z` are declared within the block, creating new variables that are distinct from the ones declared outside of the block. When the if statement is exited, the original `var x` retains its value of 4.

    Another Example

    ```javsacript
    function example() {
    if (true) {
        var x = 1;
        let y = 2;
        console.log(x); // Output: 1
        console.log(y); // Output: 2
    }
    console.log(x); // Output: 1
    console.log(y); // Output: Uncaught ReferenceError: y is not defined
    }
    example();

    ```

    In this example, the variable x is declared with var and the variable y is declared with let. Inside the if block, both variables are accessible and their values are printed to the console. Outside of the if block, x is still accessible (because it is declared with var and is hoisted to the top of the function scope), but y is not accessible (because it is declared with let and has block scope).

4.  **What are closures in JavaScript?**

    Closures are an important concept in JavaScript that allow inner functions to access the variables and parameters of outer functions, even after the outer functions have returned. In other words, a closure is a function that has access to variables in its outer scope, even after the outer function has finished executing.

    **Basic Closure**

    ```javascript
    function outer() {
      var x = 10;

      function inner() {
        console.log(x);
      }

      return inner;
    }

    var closure = outer();
    closure(); // Output: 10
    ```

    In this example, the inner() function is defined inside the outer() function and has access to the x variable in the outer scope, even after the outer() function has returned. When we call the closure() function, it logs the value of x, which is 10.

    **Closure with Arguments**

    ```javascript
    function outer(x) {
      return function (y) {
        console.log(x + y);
      };
    }

    var closure = outer(10);
    closure(5); // Output: 1
    ```

    In this example, the outer() function returns an inner function that has access to the x parameter in the outer scope. When we call the closure() function with an argument of 5, it logs the sum of x and y, which is 15.

    **Closure with Private Variables**

    ```javascript
    var counter = (function () {
      var count = 0;

      return {
        increment: function () {
          count++;
          console.log(count);
        },
        reset: function () {
          count = 0;
          console.log(count);
        },
      };
    })();

    counter.increment(); // Output: 1
    counter.increment(); // Output: 2
    counter.reset(); // Output: 0
    ```

    In this example, an immediately invoked function expression (IIFE) is used to create a closure with private variables count, increment() and reset() methods. The increment() method increments the count variable and logs its value, while the reset() method sets count to 0 and logs its value. The counter variable is assigned the returned object, which has access to the private count variable and the public increment() and reset() methods.

5. **What is event loop in Javascript**
    The event loop is a fundamental concept in JavaScript, and it's essential to understanding how asynchronous programming works in the language. It enables the creation of responsive and efficient applications, as well as the handling of long-running tasks such as network requests and animations.

    The event loop is a mechanism in JavaScript that enables asynchronous behavior. It's the process by which JavaScript engines handle concurrent execution of code. JavaScript is a single-threaded language, which means that only one piece of code can be executed at a time. However, the event loop allows JavaScript to handle multiple tasks and events asynchronously, without blocking the main thread.

    Here's how the event loop works:

    1. JavaScript code is executed synchronously, line by line, in the order in which it is written.

    2. When an asynchronous function is called, such as setTimeout(), it is moved to the Web API environment to be executed. The Web API environment is provided by the browser, and it handles the execution of code that requires waiting, such as waiting for a timer to complete.

    3. Once the Web API environment has completed its task, it adds the callback function to the task queue.

    4.  The event loop constantly checks the task queue to see if there are any functions waiting to be executed.

    5. If there is a function in the queue, it is moved to the call stack to be executed.

    6. When the function is executed, any synchronous code inside it is executed first, and then any asynchronous functions are moved to the Web API environment to be executed.

    The process repeats itself as long as there are functions in the task queue.

    ```javascript
    console.log("start");

    setTimeout(() => {
    console.log("setTimeout");
    }, 0);

    console.log("end");

    // output
    start
    end
    setTimeout
    ```

6. **What is event bubbling in JavaScript?**
    
    Event bubbling is a mechanism in JavaScript that describes how events propagate through the DOM (Document Object Model) hierarchy. When an event is triggered on an element, such as a mouse click or a key press, the event is first handled by the element itself, and then it bubbles up through its ancestors in the DOM tree.

    Here's how event bubbling works:

    1. An event is triggered on an element.

    2. The event is first handled by the element itself. If there is an event listener attached to the element, it will be executed.

    3. The event then propagates up through the DOM tree, from the innermost element to the outermost element.

    4. At each level of the DOM hierarchy, the event is handled by any event listeners attached to the element.

    5.  The event continues to bubble up through the DOM tree until it reaches the document object.

    6. If there are no more event listeners to handle the event, it is considered to be a "default action" of the event, such as submitting a form or following a link.

    Here's an example of how event bubbling works:

    ```html
        <div id="outer">
            <div id="inner">
                <button id="button">Click me</button>
            </div>
        </div>
    ```

    ```javascript
    const outer = document.getElementById("outer");
    const inner = document.getElementById("inner");
    const button = document.getElementById("button");

    outer.addEventListener("click", () => {
    console.log("outer clicked");
    });

    inner.addEventListener("click", () => {
    console.log("inner clicked");
    });

    button.addEventListener("click", () => {
    console.log("button clicked");
    });

    // output 
    button clicked
    inner clicked
    outer clicked
    ```
    When the "Click me" button is clicked, the event is first handled by the button element itself, and then it bubbles up through the DOM hierarchy. The event is then handled by the inner div element, and finally by the outer div element

    Event bubbling can be useful for creating more maintainable and flexible code, as it allows you to attach event listeners to parent elements instead of individual child elements. This can simplify your code and reduce the number of event listeners that need to be created. However, it's important to be aware of event bubbling and how it can affect your code, as it can sometimes lead to unintended consequences if not handled properly.

8. **What is the difference between a function declaration and a function expression in JavaScript?**

9. **What is the difference between an object and an array in JavaScript?**

10. **What is the difference between a callback function and a promise in JavaScript?
What is the purpose of the this keyword in JavaScript?**

11. **What is a constructor function in JavaScript and how does it work?**

11. **What is the difference between `null` and `undefined` in JavaScript?**
12. **What is the difference between `==` and `===` in JavaScript?**

13. **What is the difference between synchronous and asynchronous JavaScript?**

14. **What are the different ways to declare a function in JavaScript?**

15. **What is event bubbling in JavaScript?**
16. **What are the different ways to loop through an array in JavaScript?**
