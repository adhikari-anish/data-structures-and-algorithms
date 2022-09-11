# Introduction

Algorithms are just functions that programmers write. Algorithms are steps in a process that we take to perform a desired action with computers.

Algorithms allow us to use language built in data structures like arrays and objects or primitives like integers and booleans and, even custom data types.

```
Data Structures + Algorithms = Programs
```

---

## Recursion Introduction

Recursion is technically an algorithm but its a concept. Recursion is simply a function that refers to itself inside that function. Recursion is good for tasks that have repeated sub-tasks to do. Recursion is used in searching and sorting alogrithm.

The problem with recursion is that the computer needs to allocate memory to remember things. Stack over flow can occur when we have recursion and there's no way to stop this recursive call. We can run into problem of stack overflow.

## Anatomy of Recursion

Every recursive function must have base case or stop point.

```js
let counter = 0;
function inception() {
  debugger;
  if (counter > 3) {
    return 'done!'; // base case
  }
  counter++;
  return inception(); // recursive case
}
inception();
```

Rules:  
1. Identify the base case
2. Identify the recursive case
3. Get closer and closer and return when needed. Usually you have 2 return statements, one for base case and one for recursive case.

So, recusrion works like: The function gets closer and closer to the base case i.e. the exit/ return statement, and once it gets to the base case, it finally returns and pop functions off the stack.

---

## Exercise Factorial

Write two functions that finds the factorial of any number. One should use recursive, the other should just use a for loop

```js
// Write two functions that finds the factorial of any number. One should use recursive, the other should just use a for loop

function findFactorialRecursive(number) { // O(n)
  if (number === 2) {
    return 2;
  }
  return (number * findFactorialRecursive(number - 1));
}

findFactorialRecursive(5);

function findFactorialIterative(number) { // O(n)
  let answer = number;
  if (number === 2) {
    answer = 2;
  }
  for (let i = number; i > 1; i--) {
    answer = answer * (i - 1);
  }
  return answer;
}

findFactorialIterative(3);
```
---

## Exercise Fibonacci

```js
// Given a number N return the index value of the Fibonacci sequence, where the sequence is:

// 0, 1, 1, 2, 3, 5,8, 13, 21, 34, 55, 89, 144, ...
// the pattern of the sequence is that each value is the sum of the 2 previous values, that means that for N=5 -> 2 + 3

function fibonacciIterative(n) { // O(n-2) ~ O(n)
  if (n < 2) {
    return n;
  }

  let a = 0;
  let b = 1;
  let sum;
  
  for (let i = 1; i < n; i++) {
    sum = a + b;
    a = b;
    b = sum;
  }

  return sum;
}

console.log('iterative', fibonacciIterative(42));

function fibonacciIterativeRecursive(n) { // O(2^n)

  if (n < 2) {
    return n;
  }

  return fibonacciIterativeRecursive(n - 2) + fibonacciIterativeRecursive(n - 1);

}

console.log('recursive', fibonacciIterativeRecursive(42));
```

---

<img src="./images/Screen Shot 2022-09-11 at 10.48.12 AM.png" height="250px" />

In recursion solution, it takes exponential time i.e. the size of the tree grows exponentially when n increases, whereas iterative approach is O(n). So, here although recursive looks more readable it may not be ideal solution, becuase big O calculation is pretty big.

But, there are some trade off in recursion. There are pros and cons. We can make recursive function from O(2^n) to O(n) by using dynamic programming and memoization.

---

## Recursive Vs Iterative

>Anything you do with a recursion can be done iteratively (loop)

So, why recursion??

For some problems, recursion is easier to write. It depends on the situation. There is always pros and cons in programming, and good engineer is who can make the right decisions based on those pros and cons.

There are times when recursion can keep our code DRY.

### Recursion pros and cons:
Pros:  
* DRY
* Readability

Cons:  
* Large Stack: Recursion creates a extra memory footprint becuase every time we add a function to the call stack, it adds extra piece of memory. So, we can have cases of stack overflow.

There is something called `Tail Call Optimization` in many programming languages and in javascript with es6 it allows recursion to be called without increasing the call stack.

---

## When To Use Recursion??

When it gets too complicated problems like traversing or searching through trees or graphs, recursion is very useful and better than iterative approaches. And, with sorting through items also there are cases that recursion is prefered.

Rule: 

Every time you are using a tree or converting something into a tree, consider recursion.
1. Divide into a number of subproblems that are smaller instances of the same problem.
2. Each instance of the subproblem is identical in nature.
3. The solutions of each subproblem can be combined to solve the problem at hand.

<mark>Divide and Conquer using Recursion</mark>
