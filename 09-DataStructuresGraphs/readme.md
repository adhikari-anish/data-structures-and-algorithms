# Graphs

Graphs are one of the most useful and most used data structures when it comes to modeling life. A graph is a simply a set of values that are related in pair wise fashion.

<img src="./images/Screen Shot 2022-09-10 at 10.53.54 AM.png" height="200px" />

<figure>
<img src="./images/Screen Shot 2022-09-10 at 10.52.19 AM.png" alt="Graphs" height="200px" />
<figcaption>Graphs</figcaption>
</figure>

---

## Types of Graphs

### Directed or Undirected

- Directed 

We can go to only one direction specified. Example: One way street where we can only go one way. Twitter is more of a directed since if I follow people, they don't have to essentially follow me.


- Undirected

We can go to both directions. Examples: highways where we can go to both cities back and forth. Facebook, when I am connected to a friend that friend is connected to me as well.

<img src="./images/Screen Shot 2022-09-10 at 12.58.30 PM.png" height="250px" />

### Weighted Graph

- Unweighted

- Weighted

Vertices have some weight. These graphs are used to calculate shortest path. 

<img src="./images/Screen Shot 2022-09-10 at 1.04.54 PM.png" height="250px" />

### Cyclic and Uncyclic Graph

- Cyclic

When you have vertices connected in cycle, it's cyclic graph. Common in weighted graphs such as Google maps.

- Acyclic

Graph which doesn't have cycle.

<img src="./images/Screen Shot 2022-09-10 at 1.07.50 PM.png" height="250px" />

---

## Implementing Graphs

<img src='./images/Screen Shot 2022-09-10 at 1.44.16 PM.png' height="250px" />

<u>Edge List</u>

const graph = [[0, 2], [2, 3], [2, 1], [1, 3]]

<u>Adjacent List</u>

The index of the array is the value of the actual graph node.  
const graph = [[2], [2, 3], [1, 3, 0], [2, 1]]

<u>Adjacent Matrix</u>

const graph = [
  [0, 0, 1, 0],
  [0, 0, 1, 1],
  [1, 1, 0, 1],
  [0, 1, 1, 0]
]

### Implementation
Let's implement the below graph using adjacency list. For the adjacency list, we are gonna use the hash table.

<img src="./images/Screen Shot 2022-09-10 at 3.01.07 PM.png" height="300px" />

We wanna use the object instead arrays for adjacency list because if we start removing things from the graph or placing things in the graph thats out of order it's gonna cost a lot because arrays  shifting, unshifting is expensive. But with objects we can quickly find the items and see their connections. 

```js
class Graph {
  constructor () {
    this.numberOfNodes = 0;
    this.adjacentList = {};
  }

  addVertex (node) {
    this.adjacentList[node] = [];
    this.numberOfNodes++;
  }

  addEdge (node1, node2) {
    // undirected Graph
    this.adjacentList[node1].push(node2);
    this.adjacentList[node2].push(node1);
  }

  showConnections () {
    const allNodes = Object.keys(this.adjacentList);
    for (let node of allNodes) {
      let nodeConnections = this.adjacentList[node];
      let connections = "";
      let vertex;
      for (vertex of nodeConnections) {
        connections += vertex + " ";
      }
      console.log(node + "-->" + connections);
    }
  }
}

const myGraph = new Graph();
myGraph.addVertex('0');
myGraph.addVertex('1');
myGraph.addVertex('2');
myGraph.addVertex('3');
myGraph.addVertex('4');
myGraph.addVertex('5');
myGraph.addVertex('6');
myGraph.addEdge('3', '1');
myGraph.addEdge('3', '4');
myGraph.addEdge('4', '2');
myGraph.addEdge('4', '5');
myGraph.addEdge('1', '2');
myGraph.addEdge('1', '0');
myGraph.addEdge('0', '2');
myGraph.addEdge('6', '5');

myGraph.showConnections();
// Answer: 
// 0 --> 1 2
// 1 --> 3 2 0
// 3 --> 1 4
// 4 --> 3 2 5
// 5 --> 4 6
// 6 --> 5
```

---

## Graphs Review

Big O's are complicated with graphs as there are many different kinds of graphs.

Pros: 
* Relationships: Graphs are useful for relationships because some data needs to be in a graph form, there is no other way around it. 

Cons: 
* Scaling is hard: You need a big company and resources to make sure graph scale well.