# Most commonly asked React interview questions and their answers

Job interviews may seem scary, specially if you've just starting your career as a developer. However, as you gain more experience, you'll realize that most interviews follow a similar pattern and ask similar questions. In this article, I'll share some of the most commonly asked React interview questions and their answers.

These are the questions that I've personally been asked during most of my job interviews. And also knowing the answers to these questions will make you a better React developer overall.

This article is not just going to be about questions and answers, but also I want to tell you **how** to answer these questions in order to take control of the interview process and predict the next question.

## What are the Higher Order Components (HOC) in React? ( and possible follow up questions )

If I say that I've been asked about HOCs in 95% of my interviews, I wouldn't be exaggerating. In order to impress the interviewer, I want you to answer to this question in the following way:

In simple terms, a **HOC** is a function that takes a component as an argument and returns a new component.

```jsx
// very simplified example
import React, { useEffect } from "react";

// higher-order component
const withLogging = (WrappedComponent) => {
  return (props) => {
    useEffect(() => {
      console.log("Component has been mounted!");
    }, []);

    return <WrappedComponent {...props} />;
  };
};

// component
const MyComponent = (props) => {
  return <div>Hello, {props.name}!</div>;
};

// enhanced Component using the HOC
const EnhancedComponent = withLogging(MyComponent);

// usage in the app
const App = () => {
  return <EnhancedComponent name="John" />;
};

export default App;
```

You can also say that higher-order components (HOCs) are functions that take a component as input and return a new component with added functionality.

Then you can say that the main advantage of using HOCs is that they allow you to reuse the code and share common functionality between components.

But just don't stop there! This question will provide a perfect opportunity to show off your knowledge of React by providing a really good example of a HOC, which is **React Memo**.

### What is React Memo?

Now, once you're done explaining what a HOC is, you can say that React Memo is a HOC that will help you optimize your React application by caching the result of the component and re-rendering it only if the props have changed:

```jsx
import React, { memo } from "react";

// component
const MyComponent = ({ name }) => {
  console.log("Rendering MyComponent...");
  return <div>Hello, {name}!</div>;
};

// enhanced Component using the memo HOC
const MemoizedComponent = memo(MyComponent);

// usage in the app
const App = () => {
  return (
    <>
      <MemoizedComponent name="John" />
      <MemoizedComponent name="Jane" />
    </>
  );
};

export default App;
```

By mentioning React Memo, you'll show that you're not just familiar with the concept of HOCs, but also you know how to use them in your application.

As you mention React Memo, the interviewer will most likely ask you about the `useMemo()` and `useCallback()`. Honestly, I've been asked about these hooks in almost every interview. So let's talk about them.

### What is useMemo() hook in React?

The `useMemo()` Hook in React helps optimize performance by preventing expensive and functions from running unnecessarily. It returns a memoized value, allowing you to reuse computed results and avoid unnecessary calculations.

Memoization is a proccess of caching a value so that it does not need to be recalculated.

The useMemo Hook only runs when one of its dependencies update. This Hook accepts two arguments: a function and a dependencies array. The function argument returns a value that is cached by the Hook. The dependencies array argument is used to specify which values should trigger the function to re-run.

```jsx
import React, { useMemo } from "react";

// component
const MyComponent = () => {
  // expensive calculation
  const expensiveResult = useMemo(() => {
    console.log("Performing expensive calculation...");
    // simulating a time-consuming operation
    // e.g., fetching data, complex computation
  }, []);

  return <div>Result: {expensiveResult}</div>;
};

// Usage in the app
const App = () => {
  return <MyComponent />;
};

export default App;
```

### What is useCallback() hook in React?

`useCallback()` is a React Hook that returns a memoized version of a function, ensuring that the function reference remains consistent across re-renders.

```jsx
import React, { useState, useCallback } from "react";

// component
const MyComponent = () => {
  const [count, setCount] = useState(0);

  // increment function
  const increment = useCallback(() => {
    setCount((prevCount) => prevCount + 1);
  }, []);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
};

// usage in the app
const App = () => {
  return <MyComponent />;
};

export default App;
```

### What is the difference between useMemo() and useCallback() in React?

The `useMemo()` Hook is similar to `useCallback()` in that it also accepts a function and a dependencies array. However, the difference is that `useMemo()` returns the result of the function, whereas `useCallback()` returns the function itself.

According to [w3schools](https://www.w3schools.com/react/react_usecallback.asp):

> The useCallback and useMemo Hooks are similar. The main difference is that useMemo returns a memoized value and useCallback returns a memoized function.

### What is the difference between useMemo() and React Memo?

The `useMemo()` Hook is used to memoize a value, whereas React Memo is used to memoize a component.

### How to prevent unnessary re-renders in React?

1. **Use React.memo:** Wrap your functional component with React.memo() to memoize the component and prevent re-renders when the props remain the same.

2. **Use useCallback:** Utilize useCallback() hook to memoize functions and ensure consistent function references across re-renders. This is particularly useful when passing callbacks to child components.

3. **Use useMemo:** Employ useMemo() hook to memoize expensive computations or calculations. By caching the result and recalculating only when the dependencies change, you can avoid redundant work.

Now that we've talked about HOCs and possible follow up questions, let's talk about another important questions that you'll most likely be asked during your interview.

## What is useEffect() hook in React? ( and possible follow up questions )

The `useEffect()` hook is used to perform side effects in functional components. It is a close replacement for `componentDidMount()`, `componentDidUpdate()`, and `componentWillUnmount()` lifecycle methods in React class components.

The `useEffect()` hook accepts two arguments: a function and a dependencies array. The function argument is called after the component renders. The dependencies array argument is used to specify which values should trigger the function to re-run.

```jsx
import React, { useState, useEffect } from "react";

// component
const MyComponent = () => {
  const [count, setCount] = useState(0);

  // useEffect hook
  useEffect(() => {
    console.log("Component has been updated!");
  });

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
};

// usage in the app
const App = () => {
  return <MyComponent />;
};

export default App;
```

### What is the cleanup function in useEffect() hook?

The `useEffect()` hook can optionally return a cleanup function. This function is called before the component is removed from the DOM. It is used to perform any cleanup, such as clearing timers or removing event listeners.

### How to prevent useEffect() from running on every render?

By default, the `useEffect()` hook runs after every render. However, you can specify a second argument, known as the dependencies array, to control when the hook is run.

### What is the dependencies array in useEffect() hook?

The dependencies array is the second argument to the `useEffect()` hook. It is used to specify which values should trigger the function to re-run. If the dependencies array is empty, the hook will only run once, similar to `componentDidMount()`.

## What is Redux and why do we need it? ( and possible follow up questions )

Allright, this one could be tricky if you're not an experienced developer. Redux is complicated and most junior developers don't know how to explain it. But you don't need to know the first thing about Redux and nail this question anyways! You might be asking how?

Well, the answer is simple. You don't need to know what Redux is, but you need to know why we need it. And the answer is simple: we need Redux to manage the state of our application.

There are many ways to manage the state of your application, and you're not limited to Redux. You can use React Context API, MobX. In my experience, the interviewer wants to know that you're aware of the fact that we need to manage the state of our application.

**Important note**: While you may not be familiar with Redux, you should be familiar with the concept of state management. So, if you're not familiar with Redux, you can say that you're familiar with the concept of state management and you're aware of the fact that we need to manage the state of our application.

And for that, you have to master on of the state management approaches, I personally recommend Context API.

Context API is built-in React and it's very easy to use. If you're not familiar with Context API, you can read this [fantastic article](https://kentcdodds.com/blog/how-to-use-react-context-effectively) by [Kentcdodds](https://kentcdodds.com).

## What is Virtual DOM in React? ( and possible follow up questions )

The Virtual DOM is a lightweight JavaScript object that represents the real DOM. It is a node tree that lists the elements, their attributes and content as Objects and their properties. React’s render function creates a node tree out of the React components.

### What is the difference between Virtual DOM and Real DOM?

The Virtual DOM is an in-memory representation of Real DOM. The representation of a UI is kept in memory and synced with the “real” DOM. It’s a step that happens between the render function being called and the displaying of elements on the screen. This entire process is called reconciliation.

### How does Virtual DOM work?

When a component’s state data changes, the Virtual DOM creates a new Virtual DOM object, using the updated state data. Then the entire Virtual DOM is re-rendered.

This new representation of the UI is compared with the previous version of the Virtual DOM. React figures out the difference between the two Virtual DOMs and updates only the parts of the actual DOM that have changed.

This makes the app faster, and the user experience is closer to that of a native app.

### What are the advantages of Virtual DOM?

1. **Performance:** Manipulating the DOM is slow. Manipulating the Virtual DOM is much faster, because nothing gets drawn onscreen. Think of manipulating the Virtual DOM as editing a blueprint, as opposed to moving rooms in an actual house.

2. **Simplicity:** The Virtual DOM is a simple, lightweight JavaScript object. This makes it easy for React to compare the Virtual DOM with the previous version and determine what has changed.

3. **Cross-platform:** One of the biggest advantages of the Virtual DOM is that it increases the cross-platform compatibility of React. The Virtual DOM was one of the reasons why React could be used to develop native apps for iOS and Android with React Native.

## What is the difference between state and props in React?

Props (short for properties) and state are both plain JavaScript objects. While both hold information that influences the output of render, they are different in one important way: props get passed to the component (similar to function parameters) whereas state is managed within the component (similar to variables declared within a function).

## What are the Hooks in React? ( and possible follow up question )

Hooks are a new addition in React 16.8. They let you use state and other React features without writing a class.

### What are the rules of using Hooks in React?

1. **Only call Hooks at the top level:** Don’t call Hooks inside loops, conditions, or nested functions.

2. **Only call Hooks from React functional components:** Don’t call Hooks from regular JavaScript functions. Instead, you can:

   - Call Hooks from React function components.
   - Call Hooks from custom Hooks.

## What is Error Boundary in React?

Error boundaries are React components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI instead of the component tree that crashed.

## What is the difference between controlled and uncontrolled components in React?

In a controlled component, form data is handled by a React component. The alternative is uncontrolled components, where form data is handled by the DOM itself.

## Conclusion

This was a list of some of the most commonly asked React interview questions and their answers. Before letting you go, I want to mention a few helpful tips that you may find helpful during your own job interviews.

1. If you don't know the answer, don't freak out! No one expect you to know the answer to every question. If you don't know the answer, just say that you don't know the answer. But don't stop there! You can say that you don't know the answer, but you're willing to learn. This will show that you're a fast learner and you're willing to learn new things. So try to ask a few questions about the topic and try to figure out the answer with the help of the interviewer

2. Don't try to memorize the answers! I know that it's tempting to memorize the answers, but don't do it! You'll most likely forget the answers during the interview and you'll look like a fool. Instead, try to understand the concept behind the question and try to answer it in your own words.

3. Don't be afraid to ask questions! If you don't understand the question, don't be afraid to ask the interviewer to repeat the question. Also, if you don't understand the question, you can ask the interviewer to explain the question in more details. This will show that you're interested in the topic and you're willing to learn.

I hope you found this article helpful. If you have any questions or feedback, please feel free to reach out to me on [Twitter](https://twitter.com/Yazdun).
