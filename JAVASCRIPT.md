# JavaScript Interview Question Bank

Listing all the possible JavaScript questions, divided into following types

A. [Fundamentals Theory](#fundamentals-theory)

B. [Code Snippets Tricky Questions](#code-Snippets-tricky-questions)

C. [Advanced Concepts](#advanced-concepts)

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

    ```javascript
    console.log(x); // Output: undefined
    var x = 10;
    ```

    ```javascript
    foo(); // Output: "Hello, world!"

    function foo() {
    console.log("Hello, world!");
    ```

    ```javascript
    foo(); // Output: TypeError: foo is not a function

    var foo = function() {
    console.log("Hello, world!");
    };
    ```

    In this example, a function expression is used to create the foo() function. However, when we try to call the function before it has been declared, we get a TypeError instead of a reference error. This is because the variable declaration is hoisted, but the function expression is not.

    ```javascript
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

    ***In JavaScript hoisting, function declarations are hoisted before variable declarations. This means that functions can be called before they are declared in the code, whereas variables need to be declared before they can be used.***

    ```javascript
    var x = 1;
    function foo() {
        console.log(x);
        var x = 2;
        console.log(x);
    }
    foo();
    // output
    // undefinde and 2
    ```
    At first glance, it might seem like the output should be 1 and 2, since x is declared and assigned the value 1 before the foo function is called. However, due to hoisting, the var x = 2 statement is actually moved to the top of the foo function, above the console.log(x) statement.


3.  ### What is the difference between `let`, `const`, and `var` in JavaScript

    `let`, `var`, and `const` are all used to declare variables in JavaScript, but they have different scoping rules and behaviors.

    - `var` declarations are function scoped, meaning they are accessible within the function they are declared in or any nested functions. They can also be accessed outside the function if they are declared in the global scope.
    - `let` and `const` are block scoped, meaning they are only accessible within the block they are declared in, such as a loop or conditional statement. The difference between `let` and `const` is that `let` allows the variable to be reassigned, while `const` does not.

    For example:

    ```javascript
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
    closure(5); // Output: 15
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

    1. Snippet
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

    2. Snippet
    ```
    const seconds = new Date().getTime() / 1000;

    setTimeout(() => {
      // prints out "2", meaning that the callback is not called immediately after 500 milliseconds.
      console.log(`Ran after ${new Date().getTime() / 1000 - seconds} seconds`);
    }, 500);

    while (true) {
      if (new Date().getTime() / 1000 - seconds >= 2) {
        console.log("Good, looped for 2 seconds");
        break;
      }
    }
    ```
    <details>
      <summary>Answer</summary>
      <p>
        //After roughly 2 seconds <br />
        Good, lopped for 2 seconds <br />
        Ran after 2.000999927520752 seconds

        Here is explaination:
        1. asynch code pushed to Web API to handle, callback pushed to task queue.
        2. synch while loop is executed for 2 secs
        3. console.log('Good....') executed
        4. once call stack is empty console.log('Ran after...') gets pushed and executed.
      </p>
    </details>


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
    One key difference between function declarations and function expressions is hoisting. Function declarations are hoisted to the top of their scope, which means they can be called before they are declared in the code. Function expressions are not hoisted, so they cannot be called before they are defined.

    Another difference is that function declarations create a variable in the current scope with the same name as the function name, whereas function expressions create a variable that holds the function.

    Function declarations are generally preferred when you want to define a function that will be used throughout your code, while function expressions are useful for defining functions on the fly, as arguments to other functions, or for creating closures.

    1. As arguments to other functions:

        Function expressions can be used as arguments to other functions. For example, the Array.prototype.map() method takes a function as an argument and applies it to each element of an array. Here, we define the function to be passed to map() using a function expression:

        ```javascript
        const numbers = [1, 2, 3];
        const doubled = numbers.map(function(num) {
            return num * 2;
        });
        console.log(doubled); // Output: [2, 4, 6]
        ```
    2. For creating closures:
       Closures allow you to create a function that has access to variables in its outer scope, even after the outer function has returned. You can use a function expression to create a closure. For example:

       ```javascript
        function makeCounter() {
            let count = 0;
            return function() {
                count++;
                console.log(count);
            };
        }
        const counter = makeCounter();
        counter(); // Output: 1
        counter(); // Output: 2
       ```
       Here, the makeCounter() function returns a function that increments and logs a count variable. We assign the returned function to a variable named counter, and each time we call it, the count variable is incremented and logged.

    3. Functions on the fly:'

        Function expressions can be used to define functions "on the fly" when they are needed. For example, if you have a conditional statement that requires a different function to be executed based on a condition, you can define the function using a function expression:

        ```javascript
            function sayHello(isFriendly) {
                const greeting = isFriendly ? "Hi" : "Hello";
                const sayGreeting = function(name) {
                    console.log(`${greeting}, ${name}!`);
                };
                return sayGreeting;
            }

            const greet = sayHello(true);
            greet("Alice"); // Output: Hi, Alice!

            const sayGoodbye = sayHello(false);
            sayGoodbye("Bob"); // Output: Hello, Bob!
        ```

        In this example, the sayHello() function takes a boolean argument isFriendly. If isFriendly is true, the function returns a function that says "Hi", otherwise it returns a function that says "Hello". We assign the returned function to a variable named greet or sayGoodbye, depending on the value of isFriendly, and call it with a name argument.

9. **What is the difference between an object and an array in JavaScript?**

10. **What is the difference between a callback function and a promise in JavaScript?**

    The main difference between a callback function and a promise is that a promise provides a more structured way of handling asynchronous operations by allowing you to chain multiple operations together and handle errors in a more centralized way. However, callbacks are still commonly used, especially in older code or for simple tasks where a full promise may be overkill.

11. **What is the purpose of the this keyword in JavaScript?**
    In JavaScript, the this keyword refers to the object that the current code is being executed in. The exact value of this depends on how and where the current function is called.

    Here are some common use cases for the this keyword in JavaScript:

    1. Function context: 
    
       When a function is called as a method of an object, the this keyword refers to the object itself. For example:

        ```javascript
        const myObject = {
            myMethod() {
                console.log(this);
            }
        };

        myObject.myMethod(); // logs myObject
        ```
    2. Constructor function context

        When a function is called using the new keyword to create a new object, the this keyword refers to the new object being created. For example:

        ```javascript
        function Person(name, age) {
            this.name = name;
            this.age = age;
        }

        const person = new Person('John', 30); // creates a new Person object
        console.log(person); // logs { name: 'John', age: 30 }
        ```
    3. Global context

        When a function is called without any object context, the this keyword refers to the global object (window in the browser or global in Node.js). For example:

        ```javascript
        function myFunction() {
            console.log(this);
        }

        myFunction(); // logs the global object
        ```
    4. Explicit context:

        You can also set the this keyword explicitly using the call() or apply() methods. These methods allow you to call a function with a specific object context. For example:

        ```javascript
        const myObject = {
            myMethod() {
                console.log(this);
            }
        };

        const anotherObject = { name: 'Jane' };

        myObject.myMethod.call(anotherObject); // logs anotherObject
        ```
        The this keyword can be a powerful tool in JavaScript, but it can also be a source of confusion and bugs if not used properly. Understanding the context and value of this in your code is important for writing effective and bug-free JavaScript.

11. **What is a constructor function in JavaScript and how does it work?**

    In JavaScript, a constructor function is a special type of function that is used to create and initialize objects. It works by defining a template for a new object and allowing you to set initial values for its properties and methods.

    To create a constructor function, you can use the function keyword followed by the name of the function, and then define the properties and methods that you want to include in the object using the this keyword:

    ```javascript
    function Person(name, age) {
        this.name = name;
        this.age = age;
        
        this.greet = function() {
            console.log(`Hello, my name is ${this.name} and I'm ${this.age} years old.`);
        }
    }
    ```

    In this example, the Person function is a constructor function that takes two arguments (name and age) and initializes the object with those values using the this keyword. It also defines a greet() method that logs a message to the console using the object's name and age properties.

    To create a new object using the Person constructor, you can use the new keyword followed by the name of the constructor function and any arguments that it requires:

    ```javascript
    const person = new Person('John', 30);
    person.greet(); // logs "Hello, my name is John and I'm 30 years old."
    ```

    In this example, we create a new person object using the Person constructor function with the values 'John' and 30 for its name and age properties, respectively. We then call the greet() method on the person object to log a message to the console.

    Constructor functions are a powerful tool in JavaScript for creating and initializing objects with similar properties and methods. They allow you to define a template for your objects and avoid repeating code for each new object that you create.

12. **What is prototype and prototype chaining in JavaScript?**

    In JavaScript, each object has a special internal property called the prototype. This property is a reference to another object that is used as a fallback source for property and method lookups. When an object is created using a constructor function, its prototype property is set to the prototype property of the constructor function.

    Prototype chaining is the mechanism by which objects in JavaScript inherit properties and methods from their prototype objects. When you try to access a property or method on an object, JavaScript first checks if the object itself has that property or method. If it doesn't, it then looks at the object's prototype object and checks if that object has the property or method. If it doesn't, it looks at the prototype object's prototype object, and so on, until it reaches the end of the prototype chain.

    ```javascript
    function Animal(name) {
        this.name = name;
    }

    Animal.prototype.sayHello = function() {
        console.log(`Hello, my name is ${this.name}.`);
    };

    function Dog(name, breed) {
        Animal.call(this, name);
         // .call() is a method on every function that allows you to invoke the function specifying 
        // in what context the function will be invoked.
        // here this is Dog context, now Dog will have Anima
        this.breed = breed;
    }

    // Now how we get the methods of Animal
    // By Mapping Dog.prototype to Aimal.prototype
    Dog.prototype = Object.create(Animal.prototype);
    // finally resetting constructor as we have overriden Dog.prototype.constructor function with Animal.protoype.constructo
    Dog.prototype.constructor = Dog;

    Dog.prototype.bark = function() {
        console.log('Woof!');
    };

    const myDog = new Dog('Rex', 'Labrador');
    myDog.sayHello(); // logs "Hello, my name is Rex."
    myDog.bark(); // logs "Woof!"
    ```
    In this example, we define two constructor functions: Animal and Dog. The Animal constructor function sets the name property on the created object and defines a sayHello() method on its prototype object. The Dog constructor function calls the Animal constructor function to set the name property on the created object and also sets its own breed property. It then creates a new prototype object that is based on the Animal.prototype object and sets the Dog.prototype property to this new object. Finally, it defines a bark() method on the Dog.prototype object.

    When we create a new myDog object using the Dog constructor function, it inherits the sayHello() method from its prototype object via the prototype chain. We can also call the bark() method on the myDog object, which is defined on its own prototype object.

    In summary, the prototype property and prototype chaining are important concepts in JavaScript that allow objects to inherit properties and methods from other objects in a flexible and efficient way. Understanding how they work is key to writing effective and reusable code in JavaScript.

13. **What is Lexical Scope in javascript**

    Lexical scope is a way of determining the scope of a variable or a function in JavaScript based on where it is defined in the source code. In other words, it refers to the visibility of variables and functions within a particular block of code, and it's determined at the time the code is written, not when it's executed.

    JavaScript has a feature called lexical scoping or static scoping, which means that the visibility of a variable or function depends on where it was declared in the source code. The scope of a variable or function is defined by its surrounding code block.

    ```javascript
    function outer() {
        const x = 10;

        function inner() {
            console.log(x); // logs 10
        }
        inner();
    }
    outer();
    ```
    In this example, the x variable is defined in the outer function, and the inner function is defined inside the outer function. When the inner function is called, it can access the x variable because it is defined in its outer scope (the outer function). This is an example of lexical scoping in action.

    In summary, lexical scope is a fundamental concept in JavaScript that allows variables and functions to be visible or invisible to other parts of the code based on where they are defined. Understanding how lexical scope works is essential for writing clean and maintainable code in JavaScript.


14. **What is difference b/w call bind and apply**

    call, bind, and apply are three methods in JavaScript that are used to manipulate the this keyword and arguments passed to a function. While all three methods are used to invoke a function with a specified this value, they differ in how they handle additional arguments.

    Here are the key differences between call, bind, and apply:

    1. call: The call method is used to call a function with a given this value and arguments provided individually. It takes the this value as the first argument, followed by the individual arguments.

        Example:

        ```javascript
        function greet(name) {
            console.log(`Hello, ${name}! My name is ${this.name}.`);
        }

        const person = { name: 'Alice' };

        greet.call(person, 'Bob'); // logs "Hello, Bob! My name is Alice."
        ```

    2. apply: The apply method is similar to call, but it takes the arguments as an array instead of individually. It takes the this value as the first argument, followed by an array of arguments.

        Example:

        ```javascript
        function sum(a, b, c) {
            return a + b + c;
        }

        const numbers = [1, 2, 3];

        const result = sum.apply(null, numbers);
        console.log(result); // 6 
        ```
    3. bind: The bind method returns a new function that, when called, has the this value set to a specified value and any number of arguments passed to it. It does not immediately invoke the function, but instead returns a new function that can be called later with the specified this value and arguments.

        Example:
        ```javascript
        function greet(name) {
            console.log(`Hello, ${name}! My name is ${this.name}.`);
        }

        const person = { name: 'Alice' };

        const greetPerson = greet.bind(person);

        greetPerson('Bob'); // logs "Hello, Bob! My name is Alice."
        ```
    

## Code Snippets Tricky Questions

1. Snippet 1
    ```javascript
    console.log("1" + 2 + 3);
    console.log(4 + 5 + "6");
    ``` 
    <details>
      <summary>Answer</summary>
      <p>
      123
      
    96
      </p>
    </details>

2. Snippet 2
    ```javascript
    var x = 1;
    console.log(x++ + ++x);
    ``` 
    <details>
      <summary>Answer</summary>
      <p>
      4

      In JavaScript, both x++ and ++x are used to increment the value of a variable by 1. However, there is a difference in how they behave.

      The x++ operator is called the post-increment operator. It first returns the value of x, and then increments x by 1. Here's an example:

    ```javascript
    let x = 1;
    let y = x++; // y is assigned the value of 1, then x is incremented to 2
    console.log(x); // outputs 2
    console.log(y); // outputs 1
    ```
    The ++x operator is called the pre-increment operator. It first increments x by 1, and then returns the value of x. Here's an example:

    ```javascript
    let x = 1;
    let y = ++x; // x is incremented to 2, then y is assigned the value of 2
    console.log(x); // outputs 2
    console.log(y); // outputs 2
    ```
    So, the difference between x++ and ++x is the order in which the increment operation is performed relative to the current value of x. If you need to use the incremented value in the same statement, you should use ++x. If you need to use the original value before incrementing, you should use x++.
      </p>
    </details>

3. Snippet 3
    ```javascript
    var x = [typeof x, typeof y][1];
    var y = typeof [x, y];
    console.log(x + " " + y);
    ``` 
    <details>
      <summary>Answer</summary>
      <p>
      undefined object

      Here's what happens:

     1. The first line of code declares a variable x and initializes it with the value of the expression [typeof x, typeof y][1]

        At this point, x is undefined because it hasn't been initialized yet, and y is also undefined because it hasn't been declared yet. The expression [typeof x, typeof y][1] creates an array with two elements: the first element is the result of typeof x, which is "undefined", and the second element is the result of typeof y, which is also "undefined". The expression [typeof x, typeof y] evaluates to ["undefined", "undefined"], and [1] returns the second element of this array, which is "undefined". So, x is assigned the value of "undefined".

    2. The second line of code declares a variable y and initializes it with the value of the expression typeof [x, y].

       At this point, x is "undefined", and y is still undefined. The expression [x, y] creates an array with two elements: the first element is the value of x, which is "undefined", and the second element is the value of y, which is still undefined. The expression typeof [x, y] returns "object", because arrays are considered objects in JavaScript. So, y is assigned the value of "object".

    3. The last line of code logs the values of x and y to the console, separated by a space.

       At this point, x is "undefined", and y is "object". The expression x + " " + y concatenates the values of x and y as strings, separated by a space. So, the output is "undefined object".
      </p>
    </details>

4. Snippet 4
    ```javascript
    function foo(a, b) {
        return arguments.length;
    }
    console.log(foo(1, 2, 3));
    ``` 
    <details>
      <summary>Answer</summary>
      <p>
      3

      Here's what happens:

    1. The function foo is declared with two parameters a and b.

    2. Inside the function body, the built-in arguments    object is used to determine the number of arguments passed to the function. The arguments object is an array-like object that contains all the arguments passed to the function, regardless of the number of parameters defined in the function declaration.

    3. The arguments.length property returns the number of arguments passed to the function.

    4. The function is called with three arguments 1, 2, and 3.

    5. The console.log statement logs the return value of the function foo to the console.

    6. Inside the function, the arguments.length property returns the number of arguments passed to the function, which is 3 in this case.

    7. The return value of the function is 3.

    8. The console.log statement logs the return value 3 to the console.

    So, the output of the code is 3.
      </p>
    </details>

5. Snippet 5
    ```javascript
   var obj = {
        x: 1,
        getX: function() {
            return this.x;
        }
    };
    console.log(obj.getX());
    var getX = obj.getX;
    console.log(getX());
    ``` 
    <details>
      <summary>Answer</summary>
      <p>
      1

    undefined
      </p>
    </details>

6. Snippet 6
    ```javascript
    console.log(typeof typeof 1);
    ``` 
    <details>
      <summary>Answer</summary>
      <p>
      string
      </p>
    </details>

7. Snippet 7
    ```javascript
    function Person(name) {
        this.name = name;
    }

    Person.prototype.printName = function() {
        console.log(this.name);
    };

    var person1 = new Person("Alice");
    var person2 = new Person("Bob");

    person1.printName();
    person2.printName();

    person1.__proto__.printName = function() {
        console.log("Hacked!");
    };

    person1.printName();
    person2.printName();
    ``` 
    <details>
      <summary>Answer</summary>
      <p>
      Alice

    Bob

    Hacked!

    Hacked!
      </p>
    </details>

8. Snippet 8
    ```javascript
    var a = [1, 2, 3];
    a[10] = 10;
    console.log(a);
    console.log(a.length)
    ``` 
    <details>
      <summary>Answer</summary>
      <p>
      [1, 2, 3, empty × 7, 10] 

    11
      </p>
    </details>

9. Snippet 9
    ```javascript
    var a = [1, 2, 3];
    var b = a;
    b.push(4);
    console.log(a);
    console.log(b);
    ``` 
    <details>
      <summary>Answer</summary>
      <p>
       [1, 2, 3, 4]

     [1, 2, 3, 4]
      </p>
    </details>

10. Snippet 10
    ```javascript
    var a = 1;
    function foo() {
        console.log(a);
        var a = 2;
    }
    foo();
    ``` 
    <details>
      <summary>Answer</summary>
      <p>
       undefined
      </p>
    </details>

**Tricky questions on event loop concept**

1. Snippet 1
    ```javascript
   console.log("A");
    setTimeout(function() {
        console.log("B");
    }, 1000);
    setTimeout(function() {
        console.log("C");
    }, 0);
    console.log("D");

    ``` 
    <details>
      <summary>Answer</summary>
      <p>
      A D C B
      </p>
    </details>

2. Snippet 2
    ```javascript
    console.log("A");
    setTimeout(function() {
        console.log("B");
    }, 0);
    Promise.resolve().then(function() {
        console.log("C");
    });
    console.log("D")
    ``` 
    <details>
      <summary>Answer</summary>
      <p>
      A D C B
      </p>
    </details>

**Tricky question on == and ===**

1. Snippet
    ```javascript
    console.log(5 == "5");
    console.log(5 === "5");

    console.log(0 == "");
    console.log(0 === "");

    console.log(null == undefined);
    console.log(null === undefined);

    console.log("0" == false);
    console.log("0" === false);
    ``` 
    <details>
      <summary>Answer</summary>
      <p>
      true, false

    true, false

    true, false
    
    true, false

    true, false
      </p>
    </details>

## Advanced Concepts

1. ### Garbage Collection Methods
    1. **Reference Counting:** An object is said to be "garbage", or collectible if there are zero references pointing to it.
    2. **Mark-and-sweep:** This algorithm reduces the definition of "an object is no longer needed" to "an object is unreachable". Starts from global Object and check if any object is reachable from prototype changing
2. ### Several runtimes communicating together
    A web worker or a cross-origin iframe has its **own stack, heap, and message queue**. Two distinct runtimes can only communicate through sending messages via the **postMessage method**. This method adds a message to the other runtime if the latter listens to message events.
3. ### Debouncing and Throttling
    1. **Debouncing:** For search input field
    Snippet:
    ```javascript
    const debounce = (callBack, delay) => {
      let timeId = null;

      return (...args) => {
        clearTimeout(timeId);
        timeId = setTimeout(() => {
          callBack(args);
        }, delay);
      };
    };
    ```
    2. **Throttle:** For scrolling or resizing event handlers
    Snippet
    ```javascript
    const throttling = (callBack, delay) => {
      let shouldWait = false;
      return (...args) => {
        if (shouldWait) return;
        callBack(...args);

        shouldWait = true;
        setTimeout(() => {
          shouldWait = false;
        }, delay);
      };
    };
    ```
