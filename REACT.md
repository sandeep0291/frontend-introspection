# React Interview Question Bank

Listing all the possible React questions, divided into following types

A. [Fundamentals Theory](#fundamentals-theory)

B. [Code Snippets Tricky Questions](#code-Snippets-tricky-questions)

C. [Advanced Concepts](#advanced-concepts)



## Fundamentals Theory

1. ### What is React.lazy() and how is it used in React?

    ```javascript
    import React, { lazy, Suspense } from 'react';

    const MyComponent = lazy(() => import('./MyComponent'));

    function App() {
        return (
            <div>
            <Suspense fallback={<div>Loading...</div>}>
                <MyComponent />
            </Suspense>
            </div>
        );
    }

    export default App
    ```

    In this example, the MyComponent is loaded lazily using React.lazy(). The Suspense component is used to show a loading message while the component is being loaded. Once the component is loaded, it will be rendered like any other component in React.

    It's important to note that React.lazy() only works with default exports. If the module you want to load lazily doesn’t have a default export, you can create an intermediate module that reexports it as the default export.

2. ### What is the difference between useCallback() and useMemo() hooks in React?

    useCallback() and useMemo() are both React hooks that are used to optimize performance in functional components by avoiding unnecessary re-renders. While they are similar in some ways, there are some key differences between the two:

    useCallback() is used to memoize functions, meaning it will return a memoized version of the function that will only change if its dependencies change. It is typically used to optimize child components that rely on functions passed down as props. By memoizing the function using useCallback(), you can prevent unnecessary re-renders of the child component when the function reference changes.

    Here's an example of how to use useCallback():

    ```javascript
    import React, { useState, useCallback } from 'react';

    function MyComponent() {
        const [count, setCount] = useState(0);

        const handleClick = useCallback(() => {
            setCount(count + 1);
        }, [count]);

        return (
            <div>
            <p>Count: {count}</p>
            <button onClick={handleClick}>Increment</button>
            </div>
        );
    }
    ```

    In this example, handleClick is memoized using useCallback(). This means that the function will only be re-created if the count dependency changes, which helps to optimize performance.

    useMemo() is used to memoize the result of a function, meaning it will return a memoized version of the value that will only change if its dependencies change. It is typically used to optimize expensive computations or calculations.

    Here's an example of how to use useMemo():

    ```javascript
    import React, { useMemo } from 'react';

    function MyComponent({ number }) {
        const square = useMemo(() => {
            console.log('Computing square...');
            return number * number;
        }, [number]);

        return <div>{square}</div>;
    }
    ```
    In this example, the square value is memoized using useMemo(). This means that the value will only be re-computed if the number dependency changes, which helps to optimize performance.

    In summary, useCallback() is used to memoize functions, while useMemo() is used to memoize the result of a function. Both hooks can be used to optimize performance in React components by avoiding unnecessary re-renders.

3. ### How can you handle errors in React using Error Boundaries?

    Error boundaries are a new feature introduced in React 16 that allow you to catch errors that occur in a component's subtree, and handle them gracefully without crashing the whole application.

    Here's an example of how to create an error boundary in a component:

    ```javascript
    import React, { Component } from 'react';

    class ErrorBoundary extends Component {
        state = { hasError: false };

        static getDerivedStateFromError(error) {
            return { hasError: true };
        }

        componentDidCatch(error, info) {
            console.error('Error:', error);
            console.error('Error Info:', info);
        }

        render() {
            if (this.state.hasError) {
            return <h1>Something went wrong.</h1>;
            }

            return this.props.children;
        }
    }

    export default ErrorBoundary;
    ```

    In this example, ErrorBoundary is a component that acts as an error boundary. The getDerivedStateFromError() method is used to update the state of the component when an error occurs, and componentDidCatch() is used to log the error to the console.

    To use this error boundary in a component, you would wrap the component tree that you want to handle errors for with the ErrorBoundary component:

    ```javascript
    import React from 'react';
    import ErrorBoundary from './ErrorBoundary';

    function MyComponent() {
        return (
            <ErrorBoundary>
            <div>This component could throw an error.</div>
            </ErrorBoundary>
        );
    }
    ```

    In this example, the MyComponent component is wrapped with the ErrorBoundary component, which will catch any errors that occur in the div component.

    When an error is caught by an error boundary, the error is logged to the console, and the error boundary component's getDerivedStateFromError() method is called to update the state of the component. Then, the error boundary component's render() method is called, and you can render a fallback UI to inform the user that something went wrong.

    Error boundaries are a powerful tool for handling errors in React components, and can help you to build more robust and error-tolerant applications.

4. ### How does the new Context API work in React v16.6, and how can it be used to pass data between components?

    The new Context API in React v16.6 is a way to pass data down the component tree without having to explicitly pass props through every level of the tree. It's particularly useful when you have multiple components that need access to the same data, or when you have deeply nested components where passing props down the tree can become cumbersome.

    Here's an example of how to use the new Context API in React:

    ```javascript
    import React, { createContext, useContext } from 'react';

    // Create a new context
    const MyContext = createContext();

    // Create a provider component
    function MyProvider(props) {
        const value = {
            data: 'Hello, world!'
        };

        return (
            <MyContext.Provider value={value}>
            {props.children}
            </MyContext.Provider>
        );
    }

    // Create a consumer component
    function MyConsumer() {
        const { data } = useContext(MyContext);

        return (
            <div>
            <p>{data}</p>
            </div>
        );
    }

    // Use the provider and consumer components
    function MyComponent() {
        return (
            <MyProvider>
            <MyConsumer />
            </MyProvider>
        );
    }
    ```
    In this example, we first create a new context using the createContext() function. We then create a provider component called MyProvider that wraps its children with the MyContext.Provider component. The value prop is used to pass data down the component tree.

    We then create a consumer component called MyConsumer that uses the useContext() hook to access the data from the context. We can then render the data in the component.

    Finally, we create a top-level component called MyComponent that uses the MyProvider and MyConsumer components to pass and access data through the context.

    By using the new Context API, we can pass data down the component tree without having to pass props through every level of the tree. This can simplify our code and make it easier to manage data across multiple components.

5. ### What is the purpose of React.forwardRef() and how is it used

    React's forwardRef() is a function that allows you to pass a ref from a parent component to a child component, even if that child component is a function or a functional component that doesn't define its own ref.

    Here's an example of how to use forwardRef():

    ```javascript
    import React, { forwardRef } from 'react';

    const MyComponent = forwardRef((props, ref) => (
        <div ref={ref}>
            {props.children}
        </div>
    ));

    function ParentComponent() {
        const myRef = useRef(null);

        return (
            <div>
            <MyComponent ref={myRef}>
                Hello, world!
            </MyComponent>
            </div>
        );
    }
    ```

    In this example, we define a functional component called MyComponent, and use the forwardRef() function to forward the ref passed to it as a prop to the inner <div> element. We then define a parent component called ParentComponent that uses the ref attribute to pass a ref to the MyComponent.

    Now, when ParentComponent is rendered, the ref object passed to MyComponent will be forwarded to the inner <div> element. This allows us to access the DOM node of the <div> element using the current property of the ref object.

    The forwardRef() function is useful when you need to pass a ref to a child component, but the child component doesn't define its own ref. It's often used in conjunction with other APIs like useImperativeHandle() to expose functions or state to a parent component through a ref.

    It's important to note that forwardRef() should only be used when it's necessary to pass a ref to a child component. In most cases, you should try to avoid using refs and use other React APIs like props and state to manage your component's behavior.

6. ### What is the new "async mode" feature in React, and how can it be used to improve performance?

    React's Concurrent Mode is a new feature that was introduced in React v18. It allows React to work on multiple tasks at the same time, making it possible to build more responsive and smoother user interfaces.

    Traditionally, React renders components synchronously, which means that it processes updates one at a time. This can lead to performance issues, particularly when dealing with large or complex components or when there are many updates happening at once.

    Concurrent Mode works by allowing React to work on different parts of the component tree independently, breaking up the work into smaller units and prioritizing them based on their importance. This allows React to respond more quickly to user interactions and to keep the UI running smoothly, even under heavy load.

    One of the key benefits of Concurrent Mode is that it makes it easier to build more responsive user interfaces. For example, you can use it to create interactive elements like dropdown menus, which can be rendered quickly and smoothly, even when the user is scrolling or interacting with other parts of the page.

    To use Concurrent Mode in React, you need to enable it by wrapping your app in a <React.StrictMode> component. This will enable a number of new features, including Concurrent Mode.

    ```javascript
    import React from 'react';

    function App() {
        return (
            <React.StrictMode>
            <MyComponent />
            </React.StrictMode>
        );
    }
    ```

    In this example, we're using the <React.StrictMode> component to enable Concurrent Mode. This will ensure that any potential issues or warnings are caught early in development and that your app is optimized for performance.

7. ### What is the new "React.memo()" feature in React, and how can it be used to optimize component rendering?

    React's React.memo() is a higher-order component that can be used to optimize the rendering of functional components in React. It works by memoizing the result of the component's rendering, so that it can be reused if the component is rerendered with the same props.

    Here's an example of how to use React.memo():

    ```javascript
    import React, { memo } from 'react';

    function MyComponent(props) {
    // ...
    }

    export default memo(MyComponent);
    ```

    In this example, we define a functional component called MyComponent, and then use the memo higher-order component to wrap it. This memoizes the component's rendering result and only rerenders it if its props have changed.

    This can be especially useful when dealing with large or complex components that are expensive to render. By memoizing the component's rendering, we can avoid unnecessary rerenders and improve the performance of our app.

    It's important to note that React.memo() should only be used when necessary, as it can add some overhead to the rendering process. You should also be careful when using it with components that have callbacks or functions as props, as these can change even if the component's props haven't changed.

    Overall, React.memo() is a useful tool for optimizing the rendering of functional components in React, but it should be used judiciously to avoid unnecessary overhead and to ensure that your app remains performant.

8. ### How can you use React hooks to manage state in a functional component?

    React hooks are a way to manage state in functional components in React. Here's an example of how to use the useState hook to manage state in a functional component:

    ```javascript
    import React, { useState } from 'react';

    function MyComponent(props) {
        const [count, setCount] = useState(0);

        const handleClick = () => {
            setCount(count + 1);
        }

        return (
            <div>
            <p>You clicked {count} times</p>
            <button onClick={handleClick}>Click me</button>
            </div>
        );  
    }

    export default MyComponent;
    ```
    In this example, we define a functional component called MyComponent. We use the useState hook to create a state variable called count and a function called setCount that we can use to update the state. We initialize the state to 0.

    We define a handleClick function that we can use to update the state whenever the button is clicked. We pass this function to the onClick prop of the button element.

    Finally, we return a JSX element that displays the current state value and a button that the user can click to update the state.

    Using hooks to manage state in functional components is a powerful tool that can make your code more concise and easier to reason about. It can also help to simplify your application's overall architecture, making it easier to maintain and extend over time.

9. ### What is the difference between React's "controlled" and "uncontrolled" components, and when should you use each approach?

    In React, components can be classified as "controlled" or "uncontrolled" depending on how they manage their internal state.

    A "controlled" component is one where the component's state is managed by React, usually through the use of props. The component's internal state is not used to determine its behavior, but is instead determined by the values passed down from its parent component. An example of a controlled component would be an input field that displays its value based on the value passed to it as a prop, and triggers a callback function passed down as a prop when its value changes.

    An "uncontrolled" component, on the other hand, is one where the component manages its own internal state, usually using the DOM API. The component's internal state is used to determine its behavior, and may or may not be synced with the component's parent component. An example of an uncontrolled component would be an input field that manages its own value internally, and triggers a callback function passed down as a prop when its value changes.

    Here's an example of a controlled component:

    ```javascript
    import React, { useState } from 'react';

    function MyInput(props) {
        const [value, setValue] = useState(props.value);

        const handleChange = (event) => {
            setValue(event.target.value);
            props.onChange(event.target.value);
        }

        return (
            <input type="text" value={value} onChange={handleChange} />
        );
    }
    ```

    In this example, we define a controlled component called MyInput. We use the useState hook to create a state variable called value and a function called setValue that we can use to update the state. We initialize the state to the value passed to the component as a prop.

    We define a handleChange function that we can use to update the state whenever the input field's value changes. We also call a callback function passed to the component as a prop with the new value.

    Finally, we return an input element that displays the current state value and calls the handleChange function when its value changes.

    Here's an example of an uncontrolled component:

    ```javascript
    import React, { useRef } from 'react';

    function MyInput(props) {
        const inputRef = useRef(null);

        const handleClick = () => {
            props.onClick(inputRef.current.value);
        }

        return (
            <div>
            <input type="text" ref={inputRef} />
            <button onClick={handleClick}>Submit</button>
            </div>
        );
    }
    ```

    In this example, we define an uncontrolled component called MyInput. We use the useRef hook to create a reference to the input element, which we can access directly to get its value.

    We define a handleClick function that we can use to trigger a callback function passed to the component as a prop with the value of the input field.

    Finally, we return a div that contains an input element and a button element. When the user clicks the button, the handleClick function is called, which retrieves the value of the input field and calls the callback function with it.

    In general, controlled components are more flexible and easier to reason about, since their behavior is determined entirely by the values passed to them as props. Uncontrolled components, on the other hand, can be more efficient and may be easier to implement in some cases. The choice between controlled and uncontrolled components depends on the specific needs of your application and the tradeoffs you are willing to make between ease of use, performance, and flexibility.


10. ### How can you use the "useReducer()" hook in React to manage complex state in a component?

    The useReducer() hook in React allows you to manage complex state in a component by providing a way to update the state based on actions.

    Here's an example of how you can use useReducer() to manage a complex state:
    
    ```javascript
    import React, { useReducer } from 'react';

    const initialState = { count: 0 };

    function reducer(state, action) {
        switch (action.type) {
            case 'increment':
            return { count: state.count + 1 };
            case 'decrement':
            return { count: state.count - 1 };
            default:
            throw new Error();
        }
    }

    function Counter() {
        const [state, dispatch] = useReducer(reducer, initialState);

        return (
            <div>
            <h1>Count: {state.count}</h1>
            <button onClick={() => dispatch({ type: 'increment' })}>Increment</button>
            <button onClick={() => dispatch({ type: 'decrement' })}>Decrement</button>
            </div>
        );
    }
    ```

    In this example, we define an initial state object with a property called count set to 0. We define a reducer function that takes the current state and an action as arguments and returns the new state based on the action type.

    We create a Counter component that uses the useReducer hook to initialize the state with the initial state and the reducer function. The useReducer hook returns an array with two values: the current state and a dispatch function that we can use to dispatch actions to the reducer.

    We render the current state count property and two buttons, one that dispatches an increment action when clicked, and one that dispatches a decrement action when clicked.

    When a button is clicked, the corresponding action is dispatched to the reducer, which updates the state based on the action type.

    This is just a simple example, but you can use the useReducer hook to manage complex state that requires more than just simple state updates. You can dispatch actions that carry payloads with additional data, and you can use the reducer function to perform more complex state updates based on the action type and payload.

    By using useReducer, you can manage complex state in a more declarative way that is easier to reason about and maintain over time.
    
11. ### State is tied to a position in the tree
    When you give a component state, you might think the state “lives” inside the component. But the state is actually held inside React. React associates  each piece of state it’s holding with the correct component by where that component sits in the UI tree.

    Different component same position resets state, while **same component at same position preserves the state**.
    ```javascript
    (
        <div>
          {isFancy ? (
            <Counter isFancy={true} /> 
          ) : (
            <Counter isFancy={false} /> 
          )}
        </div>
    )
    ```
    In example given, even if there are two instances of **Counter** component, but they are conditionally rendered at same place in DOM. So they share the same state implicitly whenever there parent is re-rendering (by changing value of isFancy state value).
    <img width="727" alt="image" src="https://user-images.githubusercontent.com/51256048/226250833-66f9edd5-8496-44da-bdbc-aa8d4acb4a6e.png">

    If you want to reset state at when same component at the same position, there are two ways:
    1. Render components in different positions
    ```javascript
    (
        <div>
          {isPlayerA &&
            <Counter person="Taylor" />
          }
          {!isPlayerA &&
            <Counter person="Sarah" />
          }
        </div>
    )
    ```
    2. Give each component an explicit identity with **key**
    Keys aren’t just for lists! You can use keys to make React distinguish between any components
    ```javascript
    (
        <div>
          {isPlayerA ? (
            <Counter key="Taylor" person="Taylor" />
          ) : (
            <Counter key="Sarah" person="Sarah" />
          )}
        </div>
    )
    ```
    
