# Trees

Trees are a hierarchical data structure. As opposed to linked lists or arrays that are linear, trees can have 0 or more child nodes. A tree usually starts with a root node or a parent node, and every child of the tree descends from this root node, kind like an inversed tree. Every child of a node descends from only one parent. Parent child relationship is unidirectional. There are also leaf nodes which are the end of tree data structure. There may also sub-trees (circled with red in the diagram) in tree data structure. 

Trees are important data structure and we work with them everyday. For e.g. DOM is a tree data structure.

<image src="./images/Screen Shot 2022-09-04 at 10.13.25 PM.png" alt="Tree data structure" height="200px" />

Linked list is a kind of tree data structure with linear data structure. There are nodes. 

There are many different types of tree data structures. But, there are only few we need and others are just minor alteration.

---

## Binary Trees

A binary tree is a kind of tree data structure in which each node can only have 0, 1 or 2 nodes, and each child can only have one parent. 

<image src="./images/Screen Shot 2022-09-04 at 10.49.24 PM.png" height="200px" alt="Binary tree" />


The below image is not a binary tree since root node contains 3 child nodes.

<image src="./images/Screen Shot 2022-09-04 at 10.51.43 PM.png" height="200px" alt="Not a binary tree"  />

<image src="./images/Screen Shot 2022-09-04 at 10.57.09 PM.png" />

Perfect Binary Tree: A perfect binary tree has all the leaf nodes full and there's no node that only has one child. A node has either 0 children or 2 children. Also, bottom layer of the tree is completely filled.

Full Binary tree: A node has either 0 or 2 children but never one child.

A perfect binary tree is efficient. 
2 important properties of perfect binary tree: 

1) In perfect binary tree the number of nodes double as we go down the tree. In above diagram: 
* level 1: 1
* level 2: 2
* level 3: 4 

2) The number of nodes on the last level is equal to the sum of number of nodes in all the other levels + 1 which means about half of our nodes are on the last level. And this brings a really interesting point: by organizing our data in this way we have half data in last level. If somehow we can avoid visiting every node even if the node we are looking for is at the bottom, perhaps there is some efficiencies we can have.

In above diagram:   
Number of nodes in last level (4) = Sum of all nodes + 1 (1+2+1 = 4)

Big O notation of Binary Search Tree
* lookup : O(log N)
* insert : O(log N)
* delete : O(log N)

---

## O(log n)

We can calculate the number of nodes in a level by using: 2^n where n is a level.

Level 0: 2^0 = 1  
Level 1: 2^1 = 2  
Level 2: 2^2 = 4  
Level 3: 2^3 = 8  

We can find the number of nodes in a tree by:  
No. of nodes = 2^h - 1 where h is a height of the tree  
So,
nodes = 2^h - 1  
log nodes = height(steps)

O(log N) means the choice of the next element on which to perform some sort of action is one of several possibilities and only one needs to be chosen. 

Good way to think about O(log N) is when we are looking through a phone book. We don't actually check every single person in a phone book. Instead what we do is divide and conquer by looking based on where their names alphabetically begin. We would open up the book to where the name would start with and then keep dividing and conquering until we get to that person. We only need to explore a subset (or pages) of each section before we eventually find someones phone number. 

O(log n) is fast because we don't need to check/operate on every single element.

Google uses a tree data structure so that our searches can be really fast something like O(log n).

---

## Binary Search Trees

Binary Search Trees are good for searching, great for comparing things. This data structure preserves relationship.

* lookup O(log N)
* insert O(log N)
* delete O(log N)

<image src="./images/Screen Shot 2022-09-05 at 8.42.27 AM.png" height="250px" alt="Unbalanced BST" />

Rules for binary search trees
1) All child nodes in the tree to the right of the root node must be greater than the current node and to the left of the root node must be lesser than the current node.

2) A node can only have upto 2 children because its a binary tree.

Lookup is very fast in binary search tree since, we dont have to iterate over all the data. For example: to find 37, we know 37 is less than 101 so we take left path, now 37 is greater than 33 so we take right path, and hence we find it easily.

For insertion, BST has to figure out where to place the value i.e. it has to traverse like lookup so, the operation is going to be O(log N) [for average case].

For deletion, also we have to traverse first and then remove it. So, the operation is gonna be O(log N) [for average case]. 

---

## Balanced Vs Unbalanced BST

<figure>
    <image src="./images/Screen Shot 2022-09-05 at 9.18.17 AM.png" height="250px" />
    <figcaption>Unbalanced BST</figcaption>
</figure>

Above image shows unbalanced BST and its a big problem with BST. If we dont even have left children to root node, its gonna turn into linked list. 

Unbalanced BST
* lookup: O(n)
* insert: O(n)
* delete: O(n)

---

## Pros and Cons of BTS
Pros:  
* Better than O(n) assuming BST is balanced
* Ordered
* Flexible Size

Cons:  
* No O(1) operations

---

## Binary Search Tree Implementation

```js
class Node {
  constructor(value){
    this.left = null;
    this.right = null;
    this.value = value;
  }
}

class BinarySearchTree {
  constructor(){
    this.root = null;
  }
  insert(value){
    const newNode = new Node(value);
    if (this.root === null) {
      this.root = newNode;
    } else {
      let currentNode = this.root;
      while(true){
        if(value < currentNode.value){
          //Left
          if(!currentNode.left){
            currentNode.left = newNode;
            return this;
          }
          currentNode = currentNode.left;
        } else {
          //Right
          if(!currentNode.right){
            currentNode.right = newNode;
            return this;
          } 
          currentNode = currentNode.right;
        }
      }
    }
  }
  lookup(value){
    if (!this.root) {
      return false;
    }
    let currentNode = this.root;
    while(currentNode){
      if(value < currentNode.value){
        currentNode = currentNode.left;
      } else if(value > currentNode.value){
        currentNode = currentNode.right;
      } else if (currentNode.value === value) {
        return currentNode;
      }
    }
    return null
  }
  remove(value) {
    if (!this.root) {
      return false;
    }
    let currentNode = this.root;
    let parentNode = null;
    while(currentNode){
      if(value < currentNode.value){
        parentNode = currentNode;
        currentNode = currentNode.left;
      } else if(value > currentNode.value){
        parentNode = currentNode;
        currentNode = currentNode.right;
      } else if (currentNode.value === value) {
        //We have a match, get to work!
        
        //Option 1: No right child: 
        if (currentNode.right === null) {
          if (parentNode === null) {
            this.root = currentNode.left;
          } else {
            
            //if parent > current value, make current left child a child of parent
            if(currentNode.value < parentNode.value) {
              parentNode.left = currentNode.left;
            
            //if parent < current value, make left child a right child of parent
            } else if(currentNode.value > parentNode.value) {
              parentNode.right = currentNode.left;
            }
          }
        
        //Option 2: Right child which doesnt have a left child
        } else if (currentNode.right.left === null) {
          currentNode.right.left = currentNode.left;
          if(parentNode === null) {
            this.root = currentNode.right;
          } else {
            
            //if parent > current, make right child of the left the parent
            if(currentNode.value < parentNode.value) {
              parentNode.left = currentNode.right;
            
            //if parent < current, make right child a right child of the parent
            } else if (currentNode.value > parentNode.value) {
              parentNode.right = currentNode.right;
            }
          }
        
        //Option 3: Right child that has a left child
        } else {

          //find the Right child's left most child
          let leftmost = currentNode.right.left;
          let leftmostParent = currentNode.right;
          while(leftmost.left !== null) {
            leftmostParent = leftmost;
            leftmost = leftmost.left;
          }
          
          //Parent's left subtree is now leftmost's right subtree
          leftmostParent.left = leftmost.right;
          leftmost.left = currentNode.left;
          leftmost.right = currentNode.right;

          if(parentNode === null) {
            this.root = leftmost;
          } else {
            if(currentNode.value < parentNode.value) {
              parentNode.left = leftmost;
            } else if(currentNode.value > parentNode.value) {
              parentNode.right = leftmost;
            }
          }
        }
      return true;
      }
    }
  }
}

const tree = new BinarySearchTree();
tree.insert(9)
tree.insert(4)
tree.insert(6)
tree.insert(20)
tree.insert(170)
tree.insert(15)
tree.insert(1)
tree.remove(170)
JSON.stringify(traverse(tree.root))

//     9
//  4     20
//1  6  15  170

function traverse(node) {
  const tree = { value: node.value };
  tree.left = node.left === null ? null : traverse(node.left);
  tree.right = node.right === null ? null : traverse(node.right);
  return tree;
}
```

---

## AVL Trees and Red Black Trees

These two trees are popular for balancing binary search trees. Usually in production, we wanna have balanced binary search trees. These trees balances itself on insertion and deletion.

## Binary Heaps

lookup: O(n)
insert: O(log N)
delete: O(log N)

In binary heaps we do the insertion from left to right, so we don't have to balance the tree here. 


## Priority Queue

 Binary Heaps are great to implement priority queue. Priority queue is different from normal queue in the sense that some items while insertion gets priority than the other.

### Review of Binary Heaps and Priority Queue

Pros
* Better than O(n)
* Priority 
* Flexible Size
* Fast insert

Cons
* Slow lookup

 ## Trie

A trie is a specialized tree used in searching most often with texts.
 
<image src='./images/Screen Shot 2022-09-10 at 9.54.54 AM.png' alt="Trie" height="250" />

In most cases, trie can out perform binary search tree, hash tables, and most other data structures depending on the search we are doing.

In trie, the root is empty and from there letters are added. In image trie, we can have 26 childrens because we have 26 letters in the alphabet. When we search for 'N' in the image, there we can find two words associated with the letter 'N'. 

Another word for Trie is Prefix tree. Its a tree like data structure which proves to be quiet efficient when solving problems specific to strings such as autocompletion on search engines, implementing dictionaries, IP routing. The benifit of this data structure is speed and space. We don't have to through each node in the tree.

The space complexity is: O(length of the word)

Because of prefexes we dont have to save the prefex node multiple times. For e.g. A in word are and as, here we have to save A only one time. 

### Tree Review

Although there are a lot of trees, there is only small variations between them and they are easy to pick up. We can implement easily as needed.  