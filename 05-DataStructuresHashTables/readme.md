# Hash Tables

## Introduction

Hash tables, or hash maps, maps, unordered maps, dictionaries, objects are many different ways to call this data structure, and different language has different names for it and slight variations on the hash tables. Objects in js is a type of hash table. 

Arrays and objects (or hash tables) are most common interview questions. Almost every language has builtin hash table.

* JavaScript - objects
* Python - dictionaries
* Java - maps
* Ruby - hashes

Hash table are very important in all across computer science. They are seen in databases, caches and are extremely useful. 

In arrays, we are only able to store data in certain indexes. But, with hash tables we are able to store both key and value pair.   
Let's say we have `basket.grapes = 10000`. Here grapes is key and 10000 is value. A way hash table works is that we have a key (grapes) and this key is used as index of where to find the value in memory. This is done with hash function. Lets assume hash function like a black box for now. This works like: we are gonna pass grapes into the hash function, our black box. This hash function is gonna do some magic and will throw key as a index where we wanna save our value which is 10000 here. It stores both key and value (below images shows only value for simplicity).

<img src="./images/Screen Shot 2022-08-28 at 6.41.02 PM.png" height="300" alt="Hash table working">

---

## What is a hash function?
Hash function is used all across computer science. A hash function is a function which generates a value of fixed length for each input it gets.

There are many types of hash functions. One of them is md5. The md5 hash of hello is 5d41402abc4b2a76b9719d911017c592. Some key aspects of hash function are:
* Its one way. It means we dont know what the input was by looking into output. 
* The output of a given input is going to be same for every execution. This is called idempotent.

The benefit of hash function is it is very fast, because no matter how big the collection of data is, we only need to know the key and we instantly gets the value associated with the key. 

The hash function needs to be very fast because every time we add a property to a memory or retrieve a property from memory, we need hash function to be very fast. And, hash function in all programming languages is implemented with optimum hashing function that is very fast. Hash function like SHA-256 takes long time to generate hash, and it is complex hashing function that is used in places like cryptography.

In short, we have a key (grapes) that goes into hash function which hashes key very fast, and outputs memory address where we wanna store our data i.e. grapes and 10000.

---

## Hash Collisions

Hash function has following time complexities:

- insert - O(1)
- lookup - O(1)
- delete - O(1)
- search - O(1)

```js
let user = {
  age: 34,
  name: 'Max',
  magic: true,
  scream: function() {
    console.log('ahhhhh!');
  }
}

user.age // O(1)
user.spell = 'abra kadabra'; // O(1)
user.scream(); // O(1)
```

There is also cons of hash table. Computer allocates certain memory to the hash table. A hash table randomly assigns space in memory, and there maybe possibility of assigning same memory location for two different data which is known as hash collision.

<image src='./images/Screen Shot 2022-08-28 at 9.27.34 PM.png' alt='hash collision' height="200" />

<image src='./images/Screen Shot 2022-08-28 at 9.33.35 PM.png' alt="hash collision" height='300' />

In the second picture, there is a collision in memory address 152. With enough data and limited memory we cannot avoid hash collision. When there is a collision, it slows down the reading and writing with a time complexity O(n/k) where k is the size of the hash table. O(n/k) ~ O(n) by removing constant. Collision will likely happen in any hash table implementation, but we never have to implement ourselves.

There is two many ways to solve with hash collision like Separate chaining (linked lists), open addressing, Robin Hood hashing, etc. 

---

## Hash Tables in Different languages

Hash tables are implemented differently in different languages but most of the time the key and the value can be any type of data structure i.e. keys and values can be strings, functions, arrays, booleans etc. In Javascript, you can only have string as keys of objects. But with new es6 features, there are other kinds of hash tables like Maps and Sets. Unlike objects, Maps maintains orders in a hash table. Sets is another feature similar to maps but it only stores the keys, no values.

---

## Implementing A Hash Table

```js
class HashTable {
  constructor(size) {
    this.data = new Array(size);
  }

  // hash function
  _hash(key) {
    let hash = 0;
    /**
    * we are looping over the key here and it is very fast. we dont consider O(n), we consider it O(1)
    */
    for (let i = 0; i < key.length; i++) {
      hash = (hash + key.charCodeAt(i) * i) % this.data.length
    }
    return hash;
  } // O (1)

  set(key, value) {
    /**
    * generting the memory address by passing key to the hash function
    */
    let address = this._hash(key);
    if (!this.data[address]) { // in a hash table we can have collisions because we have only 50 shelves
      this.data[address] = [];
    }
    this.data[address].push([key, value])
    return this.data
  }  // O(1)

  get(key) {
    let address = this._hash(key);
    const currentBucket = this.data[address];
    console.log(currentBucket)
    if (currentBucket) {
      for (let i = 0; i < currentBucket.length; i++) {
        if (currentBucket[i][0] === key) {
          return currentBucket[i][1];
        }
      }
    }
    return undefined;
  } // if there is no collision, we consider it O(1). In real life we can consider it O(1)
}

const myHashTable = new HashTable(50); // we have 50 shelves in our memory
myHashTable.set('grapes', 10000);
myHashTable.set('apples', 54);
myHashTable.get('grapes');
```

The downside of array is that while getting keys, we have to loop over all the memory space even if there is only few data. In the above case we have only 3 data in our hashtable i.e. grapes, apples and oranges, but we had to loop over all 50 shelves/memory spaces to find just 3 keys. With arrays we had to loop only 3 times, because there would have been only 3 data in the array and no other memory spaces.