# Big O

## Contents
- [O(n) - Linear Time](#on---linear-time) 
- [O(1) - Constant Time](#o1---constant-time)
- [O(n^2) - Quadratic Time](#on2)
- [Simplifying Big O](#simplifying-big-o)
  - [Worst Case](#1-worst-case)
  - [Remove constants](#2-remove-constants)
  - [Different terms for inputs](#3-different-terms-for-inputs)
  - [Drop Non Dominants](#4-drop-non-dominants)

Big O notation also known as Big O asymptotic analysis. 

Any coder given enough time can solve the problem, what matters is how well the problem is solved. Big O can tell us how well the problem is solved.

**What is good code?**  
1. Readable
2. Scalable

Big O allows us to measure scalable. Big O shows us how long an algorithm takes to run.  

![Big-o complexity chart](./images/Screen%20Shot%202022-08-21%20at%203.40.48%20PM.png)

--- 

## O(n) - Linear Time

Finding Nemo example
```js
const nemo = ['nemo'];
const everyone = ['dory', 'bruce', 'marlin', 'nemo', 'gill', 'bloat', 'nigel', 'squirt', 'darla', 'hank'];
const large = new Array(10000).fill('nemo');

function findNemo(array) {
  for (let i = 0; i < array.length; i++) {
    if (array[i] === 'nemo') {
      console.log('Found Nemo!');
    }
  }
}

findNemo(large);
```

Here as the length of array increase the performance time also increase. So, it is linear time O(n).

* findNemo(nemo);  O(1)
* findNemo(everyone);  O(10)
* findNemo(large);  O(100000)
* findNemo(n); O(n)

Here, as the number of elements increase (number of inputs), the numer of operations increases linearly. Big O doesn't measure in seconds, instead it check how quickly our run time grows. We do this by using the size of the input (n) and compare to the number of operations that increase. That's what scability means.

Example:
```js
const compressAllBoxes = boxes => {
  boxes.forEach(box => console.log(box));
}
```
Here as the number of boxes increases, the number of operation increases proportionally. So, O(n) - Linear time.

--- 

## O(1) - Constant time

```js
function compressFirstBox(boxes) {
  console.log(boxes[0]);
}
```

Here, O(1) - Constant time.

Because, no matter how many boxes are passed into the function, we are just printing a first box.

![O(n)](./images/Screen%20Shot%202022-08-21%20at%205.04.30%20PM.png)

Exercise:

```js
function funChallenge(input) {
  let a = 10; // O(1)
  a = 50 + 3; // O(1)

  for (let i = 0; i < input.length; i++) { // O(n)
    anotherFunction(); // O(n)
    let stranger = true; // O(n)
    a++; // O(n)
  }
  return a; // O(1)
}
```

=> 3 + n + n + n + n = BIG O(3 + 4n) ~ O(n)

Exercise: 
```js
// What is the Big O of the below function? (Hint, you may want to go line by line)
function anotherFunChallenge(input) {
  let a = 5; // O(1)
  let b = 10; // O(1)
  let c = 50; // O(1)
  for (let i = 0; i < input; i++) { // O(n)
    let x = i + 1; // O(n)
    let y = i + 2; // O(n)
    let z = i + 3; // O(n)

  }
  for (let j = 0; j < input; j++) { // O(n)
    let p = j * 2; // O(n)
    let q = j * 2; // O(n)
  }
  let whoAmI = "I don't know"; // O(1)
}
```

=> BIG O(1+1+1+1+n+n+n+n+n+n+n) = BIG O(4+7n) ~ BIG O(n)

---

## Simplifying Big O

*Rules:*
1. Worst Case
2. Remove Constants
3. Different terms for inputs
4. Drop Non Dominants

---

### 1. Worst Case

In Big O, we always look for the worst case, even though there might be a best case scenario. 
For example, in finding nemo example, we can find nemo easily if it was located at the first place. i.e.

```js
const everyone = ['nemo', 'bruce', 'marlin', 'gill', 'bloat', 'nigel', 'squirt', 'darla', 'hank'];
```
But, we always look at the worst case scenario. i.e.

```js
const everyone = ['bruce', 'marlin', 'gill', 'bloat', 'nigel', 'squirt', 'darla', 'hank', 'nemo'];
```
---

### 2. Remove Constants

```js
function printFirstItemThenFirstHalfThenSayHi100Times(items) {
  console.log(items[0]);  // O(1)

  var middleIndex = Math.floor(items.length / 2); 
  var index = 0;

  while (index < middleIndex) {
    console.log(items[index]); // O(n/2)
    index++;
  }

  for (var i = 0; i < 100; i++) {
    console.log('hi'); // O(100)
  }
}
```

=> O(1 + n/2 + 100) (we are ignoring variable assignments and small calculations for this example)

We only care about number of inputs/elements (n). So, we drop constants because if n is larger dividing by 2 becomes less significant. Also, if n is large, we also don't care adding by some constants. 

Similarly, in this below function

```js
function compressBoxesTwice(boxes) {
  boxes.forEach(function (boxes) {
    console.log(boxes);
  })

  boxes.forEach(function (boxes) {
    console.log(boxes);
  })
}
```

=> O(2n) which will become O(n) after dropping constant.

---

### 3. Different terms for inputs

```js
function compressBoxesTwice(boxes, boxes2) {
  boxes.forEach(function(box) {
    console.log(boxes);
  })

  boxes2.forEach(function(box) {
    console.log(boxes);
  })
}
```

Here, boxes and boxes2 are different entities. Don't make a mistake to consider them as one and thinking that Big O will be O(2n). Instead boxes and boxes2 are two different entities. So, the big O will be O(a + b) where a is for input of boxes and b is for input of boxes2.

Different inputs should have different variables.
- `+` for steps in order
- `*` for nested steps

---

## O(n^2)

```js
// Log all pairs of array
const boxes = [1,2,3,4,5];

function logAllPairsOfArray(array) {
  for (let i = 0; i < boxes.length; i++) {
    for(let j = 1; j < boxes.length; j++) {
      console.log(boxes[i], boxes[j]);
    }
  }
}
```

When there is a loop inside loop (nested loop), we do multiplication. So, the big O of above code will be O(n*n) = O(n<sup>2</sup>) - Quadratic Time.

![O(n^2) Quadratic time](./images/Screen%20Shot%202022-08-22%20at%209.33.23%20PM.png)

O(n^2)'s performance is horrible because as the number of element increase, the number of operations increases significantly.

---

### 4. Drop Non Dominants

```js
function printAllNumbersThenAllPairSums(numbers) {
  console.log('these are the numbers:');
  numbers.forEach(function(number) {
    console.log(number); // O(n)
  });

  console.log('and these are their sums:');
  numbers.forEach(function(firstNumber) {
    numbers.forEach(function(secondNumber) {
      console.log(firstNumber + secondNumber); // O(n^2)
    })
  })
}
```

=> O(n + n^2). Rule number 4 states that we drop insignificant term. So, here we drop n and it comes O(n^2) because as the input increases, the size of n^2 becomes more important that n. So, we always keep the dominant term.

Similarly, for O(x^2+3x+100+x/2), if x=5, then 100 is more significant than the other terms, but as the value of x scales to 1000, then x^2 becomes more significant than the others. So, we only take x^2 and drop other non dominant terms. Then, it becomes O(x^2).

---

```
Data Structures + Algorithms = Programs
```
Data structures = ways to store data  
Algorithms = ways to use data structures to write out programs

---

## O(n!) - Factorial time 

This big O is the most expensive or most steepest one. O(n!) means we are adding nested loops for every input.

---

## 3 Pillars of Programming

1. Readable
2. Scalable 
    * Speed (Time Complexity)
    * Memory (Space Complexity)

---

## Space Complexity

When a program executes, it has two ways to remember things: the heap and the stack.  
The heap is where we store variables that we assign values to. And the stack is usually where we keep track our function calls. 

What causes time complexity?
* Variables
* Data Structures
* Function call
* Allocations

```js
function booo(n) {  
  for (let i = 0; i < n.length; i++) {  
    console.log('booooo!');
  }
}

booo([1,2,3,4,5]);
```

Time complexity of above function is O(n).  
The space complexity of above function is O(1) because of `let i=0` assignment.

```js
function arrayOfHiNTimes(n) {
  let hiArray = [];
  for (let i = 0; i < n; i++) {  
    hiArray[i] = 'hi';
  }
  return hiArray;
}

arrayOfHiNTimes(6); // O(n)
```

In the above function, we created a data structure array called hiArray and adding item 'hi' to that array, each item is additional memory space n times. From the big O rule, we are ignoring `let i = 0` cost since it is costant cost. So, the space complexity of above function is O(n).

There is often a trade off between time complexity and space complexity.  
Time complexity ⬇️ ~ Space complexity ⬆️

---

*Exercise:*

```js
// Find 1st, Find Nth...
const array = ['hi', 'my', 'teddy'];
array[0]; // O(1)
array[array.length - 1]; // O(1)
```

