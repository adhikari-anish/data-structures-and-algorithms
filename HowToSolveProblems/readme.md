# HOW TO SOLVE PROBLEMS

What are companies looking for?  
1. Analytic Skills
2. Coding Skills
3. Technical Skills
4. Communication Skills   

---

1. Analytic Skills - How can you think through the problem and analyze things, and when you are coding in an interview, they wanna hear your though process and how you go from not knowing an answer to solving the problem. 

2. Coding Skills - Interview also look at coding skills i.e. Do you code well? Is you code clean, simple, organized well, readable? 

3. Technical Skills - They also wanna know your technical skills like do you know fundamentals, do you understand pros and cons of different solutions.

4. Communication Skills - Do your personality match to their company's culture? Can you communicate well with the team?

---

## What we need for coding interview?

### Data Structures

* Arrays 
* Stacks
* Queues
* Linked Lists
* Trees
* Tries
* Graphs
* Hash Tables

### Algorithms

* Sorting
* Dynamic Programming
* BFS + DFS (Searching)
* Recursion

There are more data structures and algorithms than mentioned above but we these are the main and we only need to know these for interview. Once we get the job, we learn the rest as per our need.

---

*Exercise:*

Given 2 arrays, create a function that lets a user know (true/false) whether these two arrays contain any common items.  

For example:  
const array1 = ['a', 'b', 'c', 'x'];  
const array2 = ['z', 'y', 'i'];  
=> should return false.

const array1 = ['a', 'b', 'c', 'x'];  
const array2 = ['z', 'y', 'x'];  
=> should return true.

**Step 1: Write the key points at the top. Make sure you have all the details. Show how organized you are.**

=> We need to have a function that has two parameters and it should return true or false. Also, step 1 is already done in the question above by defining two examples which have arrays as input and true or false as output.

**Step 2: Make sure you double check: What are the inputs and what are the outputs?**

=> This is already done in the question above. We have two array as input and a boolean as output.

**Step 3: What is the most important value of the problem? Do you have time, and space and memory, etc.. What is the main goal?**

=> Since this is a simple question, we might wanna ask the interviewer how large the input array is gonna get. If the interviewer says the array is never gonna be more than 5 items, well then maybe we don't have to worry about big O or time complexity, or space complexity as much. After that we can ask interviewer is our goal here is to be as efficient as possible with our function? What's more important to us? Is it time complexity or space complexity more important? Maybe the interviewer tells us we just want the most efficient function that you can come up with assuming that the array can get very very large. In that case, we have to worry about time or space complexity.

**Step 4: Don't be annoying and ask too many questions.**

=> At this point we have almost everything to solve the problem. We may have already asked too many questions to the interview. We should only ask important questions and omit small question, and keep time limit in mind.

**Step 5: Start with the naive/brute force approach. First thing that comes into mind. It shows that you're able to think well and critically (you don't need to write this code, just speak about it).**

=> There usually have an easy solution to the problem that we call the brute force which is not the most efficient but usually is the most easiet one.  
If we look at the above problem, we usually think of comparing each element of first array with each element of second array which results in nested loop and has big O of O(n^2). And, we wanna avoid nested loops in interview questions. But, even though this is not an optimal solution, we wanna start with this which shows interviewer that we are thinking clearly about the problem and give us a point from where to improve from. We usually don't wanna code this part and is enough we describe this is a brute force approach to the interviewer.

**Step 6: Tell them why this approach is not the best (i.e. O(n^2) or higher, not readable, etc...)**

=> In our case, we said that the code might be not efficient or we might have not readable code.

```js
const array1 = ['a', 'b', 'c', 'x'];  
const array2 = ['z', 'y', 'x'];  

function containsCommonItem(arr1, arr2) {
  for (let i=0; i < arr1.length; i++) {
    for (let j=0; j < arr2.length; j++) {
      if (arr1[i] === arr2[j]) {
        return true;
      }
    }
  }
  return false;
}

containsCommonItem(array1, array2);
```

=> The above function has time complexity of O(a*b) or if two arrays are of same sizes O(n^2) which is slow.


**Step 7: Walk through your approach, comment things and see where you may be able to break things. Any repeatation, bottlenecks like O(n^2), or unnecessary work? Did you use all the information the interviewer gave you? Bottleneck is the park of the code with the biggest Big O. Focus on that. Sometimes this occurs with repeated work as well.**

=> We are doing unnecessary loop in the above solution. Let's try to optimize it.

```js
const array1 = ['a', 'b', 'c', 'x'];
const array2 = ['z', 'y', 'a'];

// array1 ==> obj {
//   a: true,
//   b: true,
//   c: true,
//   x: true
// }

// array2[index] === obj.properties
```

**Step 8: Before you start coding, walk through your code and write down the steps you are going to follow.**

* loop through first array and create object where properties === items in the array
* loop through second array and check if item in second array exists on created object. 

Now instead of nested loop, we have two loops one after another. So, the big O turns from O(n^2) to O(a+b);

*\* Step 9 comes after Step 10*

**Step 10: Start actually writing your code now. Keep in mind that the more you prepare and understand what you need to code, the better the whiteboard will go. So never start a whiteboard interview not being sure of how things are going to work out. That is a recipe for disaster. Keep in mind: A lot of interviews ask questions that you won’t be able to fully answer on time. So think: What can I show in order to show that I can do this and I am better than other coders. Break things up in Functions (if you can’t remember a method, just make up a function and you will at least have it there. Write something, and start with the easy part.**

```js
const array1 = ['a', 'b', 'c', 'x'];
const array2 = ['z', 'y', 'a'];

function containsCommonItem2(arr1, arr2) {
  // loop through first array and create object where properties === items in the array
  let map = {};
  for (let i = 0; i < arr1.length; i++) {
    if (!map[arr1[i]]) {
      const item = arr1[i];
      map[item] = true;
    }
  }

  // loop through second array and check if item in second array exists on created object. 
  for (let j = 0; j < arr2.length; j++) {
    if (map[arr2[j]]) {
      return true;
    }
  }
  return false;
}

containsCommonItem2(array1, array2);
```

**Step 11: Think about error checks and how you can break this code. Never make assumptions about the input. Assume people are trying to break your code and that Darth Vader is using your function. How will you safeguard it? Always check for false inputs that you don’t want. Here is a trick: Comment in the code, the checks that you want to do... write the function, then tell the interviewer that you would write tests now to make your function fail (but you won't need to actually write the tests).**

