# Linked Lists

A linked lists is a simple data structure that contains a set of nodes, and each node has two elements: a value of data (red block) that you want to store and a pointer (green block) to the next node in line.   
The first node is called head and the last node is called tail. 

<image src="./images/Screen Shot 2022-09-01 at 8.20.36 AM.png" height="200px" />

We call linked list null terminated because tail/last node always points to null. 

---

## Why Linked Lists?

Big O of linked list:
* prepend O(1)
* append O(1)
* lookup O(n)
* insert O(n)
* delete O(n)

Linked list is like hash table, unlike arrays they store data randomly in memory. The advantage of linked list over hash table is that data in linked list can be sorted easily because there are pointers in linked list. Arrays stores data sequentially so, in modern computers there are cache features and arrays perform better than linked list and hash tables in such scenario. Continue reading to find more about why linked list.

---

## What is a Pointer? 

A pointer is a reference to another place/object/node in memory. 

```js
let obj1 = { a: true };
let obj2 = obj1;
```

obj2 stores the reference to obj1. In other words, obj2 points to the memory location of obj1.

```js
let obj1 = { a: true };
let obj2 = obj1;
obj1.a = 'booya';
delete obj1
obj2 = obj1
console.log('2', obj2);
```

If we delete obj1 and obj2 is using obj1. Then, still obj1 will be there. This is how javascript works. If we delete obj1 and nothing is using it, then obj1 will be automatically delete in high level programming languages like javascript. Javascript is a garabage collected language, i.e. memory is managed automatically. However, in low level languages we have to manually delete the unused object. In order words, we have to manage our memory manually. We have to delete unreferenced item. This can cause issues if we leave the memory that is not being in memory used which is a valuable resource. But, there is a benefit of non-garabage collected language where we get to manage our own memory.

---

## Implementing Linked List

```js
// 10 --> 5 --> 16

// structure of linked list
// let myLinkedList = {
//   head: { // head is a first item/node in a linked list
//     value: 10,
//     next: {
//       value: 5,
//       next: {
//         value: 16,
//         next: null
//       }
//     }
//   }
// }

class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor(value) {
    this.head = {
      value: value,
      next: null    // since 10 is the only one node to begin with, next will point to null
    }
    this.tail = this.head; // becuase we only have one item the head is going to be tail
    this.length = 1  // we can keep track of the linked list. though this is optional
  }
  
  append(value) {
    const newNode = new Node(value);
    this.tail.next = newNode;  // point the pervious tail node's next to new node
    this.tail = newNode;      // update the tail to new node
    this.length++;
  }

  prepend(value) {
    // 1 --> 10 --> 5 --> 16
    const newNode = new Node(value);
    newNode.next = this.head;
    this.head = newNode;
    this.length++;
  }
  
  printList() {
    const array = [];
    let currentNode = this.head;
    while (currentNode !== null) {
      array.push(currentNode.value);
      currentNode = currentNode.next; 
    }
    return array;
  }

  insert(index, value) {
    // check params
    if (index >= this.length) {
      return this.append(value);
    }
    const newNode = new Node(value)
    const leader = this.traverseToIndex(index - 1);
    const holdingPointer = leader.next;
    leader.next = newNode;
    newNode.next = holdingPointer;
    this.length++;
  }

  remove(index, value) {
    // check params
    const leader = this.traverseToIndex(index - 1);
    const unwantedNode = leader.next;
    leader.next = unwantedNode.next;
    this.length--;
    
    
  }

  traverseToIndex(index) {
    // check params
    let counter = 0;
    let currentNode = this.head;
    while (counter !== index) {
      currentNode = currentNode.next;
      counter++;
    }
    return currentNode;
  }
}

const myLinkedList = new LinkedList(10); // 10 is the starting value of linked list
myLinkedList.append(5); 
myLinkedList.append(16); 
myLinkedList.prepend(1); 
myLinkedList.insert(2, 99);
myLinkedList.insert(20, 88);
myLinkedList.remove(2);
myLinkedList.remove(2);
console.log(myLinkedList.printList());
```

--- 

## Doubly Linked list

Doubly linked list is similar to singly linked list except it links to the node before it. 

* prepend : O(1)
* append : O(1)
* lookup : O(n)
* insert : O(n)
* delete : O(n)

<image src="./images/Screen Shot 2022-09-03 at 2.22.58 PM.png" alt="Doubly linked list" />

Doubly linked list allows us to traverse backward. Searching through doubly linked list is more efficient. Lookup can technically be O(n/2) becuase we can start at both ends and if we know in which half of the list we are looking for is, we can pick optimum place to start. The downside to doubly linked list is it takes a little bit more memory in holding the additional block to store the backward pointer.

Implementation:
```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
    this.prev = null;
  }
}

class DoublyLinkedList {
  constructor(value) {
    this.head = {
      value: value,
      next: null,
      prev: null
    }
    this.tail = this.head;
    this.length = 1 
  }
  
  append(value) {
    const newNode = new Node(value);
    newNode.prev = this.tail;
    this.tail.next = newNode; 
    this.tail = newNode; 
    this.length++;
  }

  prepend(value) {
    // 1 --> 10 --> 5 --> 16
    const newNode = new Node(value);
    newNode.next = this.head;
    this.head.prev = newNode;
    this.head = newNode;
    this.length++;
    return this;
  }
  
  printList() {
    const array = [];
    let currentNode = this.head;
    while (currentNode !== null) {
      array.push(currentNode.value);
      currentNode = currentNode.next; 
    }
    return array;
  }

  insert(index, value) {
    // check params
    if (index >= this.length) {
      return this.append(value);
    }
    const newNode = new Node(value)
    const leader = this.traverseToIndex(index - 1);
    const follower = leader.next;
    leader.next = newNode;
    newNode.prev = leader;
    newNode.next = follower;
    follower.prev = newNode;
    this.length++;
  }

  remove(index) {
    // check params
    const leader = this.traverseToIndex(index - 1);
    const unwantedNode = leader.next;
    leader.next = unwantedNode.next;
    leader.next.prev = leader;
    this.length--;    
    console.log(this)
  }

  traverseToIndex(index) {
    // check params
    let counter = 0;
    let currentNode = this.head;
    while (counter !== index) {
      currentNode = currentNode.next;
      counter++;
    }
    return currentNode;
  }
}

const myLinkedList = new DoublyLinkedList(10); 
myLinkedList.append(5); 
myLinkedList.append(16); 
myLinkedList.prepend(1); 
myLinkedList.insert(1, 99);
myLinkedList.insert(20, 88);
myLinkedList.remove(1);
myLinkedList.remove(2);
console.log(myLinkedList.printList());
```

---

## Singly vs Doubly Linked List

### Singly linked list: 
Pros:  
1) Simple implementation as compared to doubly linked list
2) Requires less memory
3) There is less operation as we dont have to move around the previous property, it is a little bit faster than doubly linked list

Cons:  
1) It cannot be traversed backwards. If we ever lose reference to the this.head node, the list can be lost in memory forever. 

So, singly linked list is appropriate to use when we have less memory or memory is really expensive, and when we wanna do fast insertion and deletion, and we dont have much searching.

### Doubly linked list
Pros:
1) It can be iterated both from front and back.
2) If we need to delete the previous node, we dont have to traverse from the head node and find what the previous node is, which is not possible in singly linked list. 

Cons: 
1) Complex to implement than singly linked list.
2) Needs more memory and storage because of extra property (previous node).
3) Needs to perform extra operations because of the extra property. 

So, doubly linked list are good when there is no limitation on memory and when we want good operation for searching for elements, such as searching backwards.

---

Exercise:

One of the popular question when it comes to linked list is: <b>To reverse the linked list</b>

```js
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor(value) {
    this.head = {
      value: value,
      next: null  
    }
    this.tail = this.head; 
    this.length = 1 
  }
  
  append(value) {
    const newNode = new Node(value);
    this.tail.next = newNode;  
    this.tail = newNode; 
    this.length++;
  }

  prepend(value) {
    // 1 --> 10 --> 5 --> 16
    const newNode = new Node(value);
    newNode.next = this.head;
    this.head = newNode;
    this.length++;
  }
  
  printList() {
    const array = [];
    let currentNode = this.head;
    while (currentNode !== null) {
      array.push(currentNode.value);
      currentNode = currentNode.next; 
    }
    return array;
  }

  insert(index, value) {
    // check params
    if (index >= this.length) {
      return this.append(value);
    }
    const newNode = new Node(value)
    const leader = this.traverseToIndex(index - 1);
    const holdingPointer = leader.next;
    leader.next = newNode;
    newNode.next = holdingPointer;
    this.length++;
  }

  remove(index, value) {
    // check params
    const leader = this.traverseToIndex(index - 1);
    const unwantedNode = leader.next;
    leader.next = unwantedNode.next;
    this.length--;
  }

  reverse() {
    if (!this.head.next) {
      return this.head;
    }
    let first = this.head;
    this.tail = this.head;
    let second = first.next;

    while (second) {
      const temp = second.next;
      second.next = first; 
      first = second;
      second = temp; 
    }
    this.head.next = null;
    this.head = first;
  }

  traverseToIndex(index) {
    // check params
    let counter = 0;
    let currentNode = this.head;
    while (counter !== index) {
      currentNode = currentNode.next;
      counter++;
    }
    return currentNode;
  }
}

const myLinkedList = new LinkedList(10);
myLinkedList.append(5); 
myLinkedList.append(16); 
myLinkedList.prepend(1); 
myLinkedList.insert(2, 99);
myLinkedList.insert(20, 88);
myLinkedList.remove(2);
myLinkedList.remove(2);
myLinkedList.reverse();
// console.log(myLinkedList.printList());
```

## Review

Linked list is a low level data structure and one of the popular topic in interview question. It doesn't come with many built in programming languages so, we have to build on our own. It is used in other data structures like hash table, stacks, queues, etc.   
The primary reason to choose linked list over something like array is because of its simplicity and its ability to grow and shrink as needed. Working with linked list can little be weird and difficult to manage all the pointers in your head but they are pretty light weight and self contained in that they can be quite flexible as well. We can see linked list in: implementing file systems on computers, browsers history.

Pros
* Fast insertion
* Fast deletion
* Ordered
* Flexible Size

Cons
* Slow lookup
* More memory