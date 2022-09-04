# Stacks and Queues

Stacks and Queues are linear data structure. Linear data structure allows us to traverse data sequentially. Stacks and queues are similar data structure because these can be implemented in similar ways and the only difference is how the item gets removed. Unlike an array there is no random access operation. 

We mainly use stacks and queues to run commands like push, peek and pop all of which deal exclusively with the element at the beginning or end of the data structure. This operation on beginning or end of data structure is not a limitation but a feature in the sense that sometimes we want to limit the operation for a user to only allow him/her to perform action on the beginning or end.

---

## Stacks

* lookup - O(n)
* pop    - O(1)
* push   - O(1)
* peek   - O(1)

Stack is **LIFO** (Last In First Out). Stacks are important for language specific engines. Programming languages are modeled with Stacks architecture in mind. When functions get called, they follows last in first out. A function within a function within a function gets called and then we start popping until we get to the very beginning. Another useful use case of stacks is browser history. When we go back and forth in browser website, it is using stacks. Idea of Undo and Redo of texts also comes from stacks.

Methods associated with Stacks:
* Pop: Remove the last item
* Push: Add an item
* Peek: View the last item

---

## Queues

Queues are **FIFO** (first in first out). 

* lookup - O(n)
* enqueue - O(1)
* dequeue - O(1)
* peek - O(1)

Queues are used in waitlist app, restaurant apps, ride sharing apps, printer.

* enqueue - add an item at the last position of the queue
* dequeue - remove first item from queue
* peek - view first item of the queue

## Stacks vs Queues

Stacks:  
Stacks can be implemented using Arrays or Linked Lists. Both are gonna work well. It depends upon the priority and preference. Arrays allows cache locality which makes its faster when accessing items in memory because they are right next to each other. On the other hand, linked list has data scattered all over memory and also linked list has extra memory associated with them to hold those pointers, but they have dynamic memory. We can keep adding to things to the linked list versus an array where it can be static or dynamic array. If its static array, we have to double up their memory and create new array. So, we have to think about operations we are gonna do and what our priorities are.

Queues:  
We never wanan build a queue with arrays because when we remove item from queue implemented using arrays, we have to shift the arrays by O(n). If we implemented queue using linked list, we only have to remove the head item and shift the head which is gonna be O(1). 

---

## How JavaScript Works?

* Difference between asynchronous and asynchronous in JavaScript?
* Javascript is a single threaded language that can be non-blocking?

<image src="./images/Screen Shot 2022-09-04 at 10.31.18 AM.png" alt="Javascript Engine, memory heap and call stack" />

JavaScript Engine: Its the engine each browser implements and for chrome its V8. The V8 engine reads the javascript that we write and changes it into machine readable instructions for the browser. The engine consists of 2 parts: Memory heap and Call stack. Memory heap is where the memory allocation happens and the call stack is where the code is read and executed. It tells us where we are in the program.

Memory leak: Memory leak happens when there is a lots of unused variables laying around in the memory heap.

Call stacks: Call stacks reads and executes our script. Suppose we have following code:

```JavaScript
console.log('1');
console.log('2');
console.log('3');
```

The JavaScript engine reads the above code `console.log('1')` and places it into the call stack, it runs and outputs 1 in console. Then, it removes (pops) the first console.log from call stack cause it is finished running and place second console.log in the call stack and execute it. It then removes (pops) seond console.log from the call stack and runs third console.log and removes it. 

Image we have the following code:
```js
const one = () => {
  const two = () => {
    console.log('4');
  }
  two();
}
one()
```

The call stack will be:  
two()  
one()

First two is executed in the call stacks and outputs 4 and gets popped out, and then one is executed in the call stack, and popped out.

`Javascipt is a single threaded language that can be non-blocking??`  

`Single threaded`: Single threaded means there is only one call stack i.e. it can only do one thing at a time. Call stack is last in first out (LIFO). Whatever is at the top of the call stack runs first and then below that, below that, below that until the call stack is empty.  
Other languages have multiple call stacks which is called Multi threaded. In multi threaded language there is issues like Deadlocks.  

Above we learned synchronous programming. Sychronous programming reads the code line by line. The second line doesn't gets executed until the first line finishes its job.

### Stack overflow

Stack overflow happens when call stack gets bigger and bigger that it doesn't have space anymore.

<image src="./images/Screen Shot 2022-09-04 at 11.37.25 AM.png" height="300px" />

Example of stack overflow:  
```js
// Recursion
function foo() {
  foo();
}
foo();
```
Above we keep adding foo function to the call stack until the call stack overflows.

`Non-blocking`: JavaScript is asynchronous. 

<image src='./images/Screen Shot 2022-09-04 at 12.51.58 PM.png' alt="JavaScript run time environment" height="400px" />

```JavaScript
console.log('1');
setTimeout(() => {
  console.log('2')
} ,2000)
console.log('3');
```

Here setTimeout is asynchronous task. From the image above we can see setTimeout is a part of Web APIs and not the part of JavaScript. Lets see how the above code works by looking at the diagram. We have to look at following terms:

- Call stack
- Web API 
- Callback Queue
- Event Loop

Firstly console.log('1') goes into the call stack and executes and logs 1 into the browser. We then get setTimeout into our call stack. Because setTimeout is not part of javascript but web API, call stack triggers the web API which triggers the setTimeout. And, because web API is notified, setTimeout is popped out of call stack. The web API starts a timer of 2 seconds, and now because the call stack is empty the javascript engine now goes to console.log(3) and executes it. We still have setTimeout of 2 seconds in web API, after 2 seconds when the time limit is up, the web API is gonna say the setTimeout is completed, let's see what's inside of it. We have console.log(2). Now setTimeout is done, we have a callback  of setTimeout in callback queue. The event loop checks if the call stack is empty and it keeps checking all the time if the stack is empty. If the call stack is empty and nothing is running in javascript engine, the event loop checks if we have any callbacks in callback queue. In our case, we have callback in callback queue. So, now the callback in queue is popped out and moved to call stack, and then the callback is executed and console.log(2) is logged in browser. Again, the event loop checks the callback queue and as nothing is in there, the program is run completely. If setTimeout has 0 seconds also, the console.log(2) is outputted after console.log(3) because as setTimeout is part of web API, console.log(2) has to go through the whole process of call stack -> web API -> callback queue -> event loop. 

---

## Stack Implementation using Linked List

```js
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class Stack {
  constructor() {
    this.top = null;
    this.bottom = null;
    this.length = 0; 
  }

  peek() {
    return this.top;
  }

  push(value) {
    const newNode = new Node(value);
    if (this.length === 0) {
      this.top = newNode;
       this.bottom = newNode;
    } else {
      const holdingPointer = this.top;
      this.top = newNode;
      this.top.next = holdingPointer;
    }
    this.length++;
  }

  pop() {
    if (!this.top) {
      return null;
    }
    if (this.top === this.bottom) {
      this.bottom = null;
    }
    this.top = this.top.next;
    this.length--;
  }
}

const myStack = new Stack();
myStack.push('google');
myStack.push('udemy');
myStack.push('discord');
myStack.pop();
myStack.pop();
myStack.pop();
// console.log(myStack.peek());
```

## Stack implementation using Array

```js
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class Stack {
  constructor() {
    this.array = [];
  }

  peek() {
    return this.array[this.array.length - 1];
  }

  push(value) {
    this.array.push(value)  
  }

  pop() {
   this.array.pop();
  }
}

const myStack = new Stack();
myStack.push('google');
myStack.push('udemy');
myStack.push('discord');
myStack.pop();
myStack.pop();
myStack.pop();
console.log(myStack.peek());
```

---

## Queue Implementation

```js
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class Queue {
  constructor() {
    this.first = null;
    this.last = null;
    this.length = 0;
  }

  peek() {
    return this.first;
  }

  enqueue(value) {
    const newNode = new Node(value);
    if (this.length === 0) {
      this.first = newNode;
      this.last = newNode;
    } else {
      this.last.next = newNode;
      this.last = newNode;
    }
    this.length++;
  }

  dequeue() {
    if (!this.first) {
      return null;
    }
    if (this.first === this.last)  {
      this.last = null;
    }
  
    this.first = this.first.next;
    this.length--;
  }
}

const myQueue = new Queue();
myQueue.enqueue('Joy');
myQueue.enqueue('Matt');
myQueue.enqueue('Pavel');
myQueue.enqueue('Samir');
myQueue.dequeue();
myQueue.dequeue();
myQueue.dequeue();
myQueue.dequeue();
myQueue.peek();

// Joy
// Matt 
// Pavel
// Samir
```

## Queue Implementation using Stacks

```js
class CrazyQueue {
  constructor() {
    this.first = [];
    this.last = [];
  }

  enqueue(value) {
    const length = this.first.length;
    for (let i = 0; i < length; i++) {
      this.last.push(this.first.pop())
    }
    this.last.push(value);
  }

  dequeue() {
    const length = this.last.length;
    for (let i = 0; i < length; i++) {
      this.first.push(this.last.pop());
    }
    this.first.pop();
  }

  peek() {
    if (this.last.length > 0) {
      return this.last[0];
    }
    return this.first[this.first.length - 1];
  }
}

const myQueue = new CrazyQueue();
myQueue.enqueue('Joy');
myQueue.enqueue('Matt');
myQueue.enqueue('Pavel');
myQueue.dequeue();
myQueue.dequeue();
myQueue.dequeue();
console.log(myQueue.peek());
```

---

## Review

Stacks and queues are fast for insertion, deletion, peeking first item in a queue, peeking top item in stack. We also have our data ordered in stacks and queues.

Stacks and queues are slow for lookup/searching through data.
