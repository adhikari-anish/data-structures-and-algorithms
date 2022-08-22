# Big O

## Contents
- [O(n) - Linear Time](#on---linear-time) 
- [O(1) - Constant time](#o1---constant-time)
- [Simplifying Big O](#simplifying-big-o)
  - [Worst Case](#1-worst-case)
  - [Remove constants](#2-remove-constants)

Big O notation also known as Big O asymptotic analysis. 

Any coder given enough time can solve the problem, what matters is how well the problem is solved. Big O can tell us how well the problem is solved.

**What is good code?**  
1. Readable
2. Scalable

Big O allows us to measure scalable. Big O shows us how long an algorithm takes to run.  

![Big-o complexity chart](../images/Screen%20Shot%202022-08-21%20at%203.40.48%20PM.png)

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

![O(n)](../images/Screen%20Shot%202022-08-21%20at%205.04.30%20PM.png)

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
