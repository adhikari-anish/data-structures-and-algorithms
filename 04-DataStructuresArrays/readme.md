# Data Structures - Arrays

Arrays, sometimes called list organizes items sequentially which means one after another in a memory.

|   |       |
|---|-------|
| 0 | Juice |
| 1 | Apple |
| 2 | Cheese|
| 3 | Kale  |
| 4 | Mango |
| 5 | Grapes |
| 6 | Eggs |
| 7 | Bread |

Arrays are probably the most simplest and widely used data structures. Arrays have a least amount of rules. Because arrays are stored in contiguous memory i.e. in order, they have the smallest footprint of any data structure.  
*If all we need is to store some data and iterate one after another, arrays are the best choice, especially if we know the indices of the item we are storing.*

* lookup = O(1)
* push = O(1) in case of high level language (dynamic arrays) or O(n) in case of low-level language (static arrays)
* insert = O(n)
* delete = O(n)

```js
const strings = ['a', 'b', 'c', 'd'];


```

If we were on a 32-bit system i.e. we have 4 shelves to store the letter 'a' in 0's and 1's, we just multiply 4*4, 4 items each taking 4 shelves in our memory. That means we are using up 16 bytes of storage. 

The computer now knows where to find the array's item. Therefore, when we do `strings[2]`, we're telling the computer hey go to the array strings and grab the third item from where the array is stored on memory and computer will return `c`.

### Operations with arrays:
1. push  
adds new element to the end of an array.  
`string.push('e');` => O(1)

2. pop  
removes last element in the array.   
`string.pop();` => O(1)  

3. unshift
add items in the beginning of an array.  
`strings.unshift('x')`  => O(n)  
When we add item using unshift, we are shifting all elements by one index to the right side. By doing this, we looped through every element and reassigned every element's indexes. So, the time complexity of this operation is O(n), where n is the length of an array. So, right away we know that with arrays, maybe its not the best data structure for adding items at the beginning of the array.

4. splice
`strings.splice(2, 0, 'alien')`  
we are adding 'alien' item at index 2, and shifting the elements after index 2 by one to the right. Here, big O is O(n/2) ~ O(n) because we looped half the array.

*<mark>As we are going through data structure we are able to think about code beyond just making it work. We now think what is happening under the hood, why might this operation be longer than that operation.</mark>*

---

# Static vs Dynamic Arrays

One limitation of static arrays are they are fixed in size, meaning we need to specify the number of elements in an array (length) ahead of time.

We solve the above issue by using dynamic arrays. Dynamic arrays allow us to copy static array and rebuilt an array at a new location with more memory if we wanted more memory. 

With javascript and python, it automaitcally allocates memory according to the increase in size of the array.

The benefit of static or dynamic array comes with the need. If you want more control over memory, then low level languages like C++ is better, and if you don't care about memory then high level languages like JavaScript is a better choice. That's why low level languages are fast than high level languages because of control over memory management.

In case of static arrays, if we need to insert an element and there is no enough memory, we create dynamic array in different location, loop over static array and copy the elements and insert into dynamic array with more space (usually double the size). In such case, the insert operation in an array becomes O(n) because we are looping over the static array.

---

# Implementing An Array

Even though array is already builtin in javascript and other languages, we can build it on our own. We can create our own data structure even if there are builtin. Most common data structures are already implemented in most of the languages because they are so useful but we are able to build any data structures from scratch and most data structures are build on top of other data structures. 

Arrays in JS are just objects with integer based keys that act like indices.
 
 We can implement array as follows:

 ```js
 class MyArray {
    constructor() {
        this.length =  0;
        this.data = {};
    }
    
    get(index) { // O(1)
        return this.data[index];
    }
    
    push(item) {  // O(1)
        this.data[this.length] = item;
        this.length++;
        return this.length;
    }
    
    pop() {  // O(1)
        const lastItem = this.data[this.length - 1];
        delete this.data[this.length - 1];
        this.length--;
        return lastItem;
    }
    
    delete(index) {  // O(n)
        const item = this.data[index];
        this.shiftItems(index);
        return item;
    }
    
    shiftItems(index) {
        for (let i = index; i < this.length - 1; i++) {
            this.data[i] = this.data[i+1];
        }
        delete this.data[this.length - 1]
        this.length--;
    }
}

const newArray = new MyArray();
newArray.push('hi');
newArray.push('you');
newArray.push('!');

// newArray.pop();
// newArray.pop();
// newArray.pop();

newArray.delete(0)
newArray.push('are');
newArray.push('nice');
newArray.delete(1);
console.log(newArray);
```

<u>*Trick:*</u>  
If there is a question related to string, turn it into an array first, perform operation and turn it back into string after the operation is completed.

## Arrays when to use and when not to

Props (When to):
* Fast lookups - i.e. accessing information when you know which index you wanna lookup
* Fast push/pop - adding items at the end of an array and taking things out from the end of an array
* Ordered - having something in order and close to each other in memory makes it really fast

Cons (When not to):
* Slow inserts - because we have to shift array whenever its not at the end of an array.
* Slow deletes - because we have to shift array whenever its not at the end of an array.
* Fixed size (if using static array)
