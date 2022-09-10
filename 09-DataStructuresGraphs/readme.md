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