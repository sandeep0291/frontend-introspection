
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
 2. **String:**

      The String type represents a sequence of characters. It is enclosed in single or double quotes. For example:

      ```javascript
      let name = 'John'; // single quotes
      let message = "Hello, world!"; // double quote
      ```

3. **Boolean:**

      The Boolean type represents a logical value, which can be either true or false. For example
      
4. **Null:**
    
      The Null type represents a deliberate non-value. It is often used to initialize a variable that will later be assigned a value.

5. **Undefined:**

      The Undefined type represents an undefined value. It is used when a variable has been declared but has not been assigned a value. For example:
      ```javascript
        let y;
        console.log(y); // Output: undefined
      ```

6. **Symbol:**

      The Symbol type represents a unique identifier. It is often used as a key in object properties.

      ```javascript
      let id1 = Symbol('id');
      let id2 = Symbol('id');
      console.log(id1 === id2); // Output: false
      ```


2. ### What is hoisting in JavaScript
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


3. ### What is the difference between `let`, `const`, and `var` in JavaScript

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

4. **What are closures in JavaScript?**

5. **What is the difference between synchronous and asynchronous JavaScript?**
6. **What is the difference between `==` and `===` in JavaScript?**
7. **What are the different ways to declare a function in JavaScript?**
8. **What is the difference between `null` and `undefined` in JavaScript?**
9. **What is event bubbling in JavaScript?**
10. **What are the different ways to loop through an array in JavaScript?**



