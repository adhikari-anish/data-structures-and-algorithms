# Data Structures

## Introduction

A data structure is a collection of values. Algorithms are the steps we put into place to manipulate these collection of values.  
```
Data Structures + Algorithms = Programs
```

## What is a Data Structure?

A data structure is a collection of values. Each data structure is different in what it can do and what it is best used for. Each data structure is good and is specialized for its own thing.

Lets think data structure as a place where we put things such as bag, fridge, drawer, paper bag, toy box etc. Each place has its own purpose. For example, we dont put yoghurt in a drawer, we dont put paper in a fridge. Similar with data structure each data structure has its own purpose.

There are tons of data structure but we only need some of them like 5 or 6 in daily basis. Bitcoin uses block chain which is also a data structure. 

Data structure models a real life scenario, and more advanced developer you become the more time you spent talking and thinking about data structures. This is why interviewers love talking about data structure. 

As there is always trade off. Every programming question has a trade off. Like our 3 pillars of readability, memory and speed has a trade off, data structure also has a trade off. One is better than the other in some aspects, and other better than the other. That why each one is used in a specific case.

Two parts to understand data structure: 
1. How to build one
1. How to use it

First one deals with how to build data structure with code and second deals with how to use built data structure to solve problem. Second one is more important than first one. Because, most of the time, data structure is already pre built in a programming langugage. *The goal is to be able to pick which data structure for which scenario* like we picked object instead of array before in how to solve problem section.

---
## How computers store data
 
In order to truly unders the value of data structures, we have to know how the computer works. In order for computer to run code, it needs to keep track of things like variables like number, strings, arrays. These variables are stored in RAM. Computer also has storage where we store video files, music files, documents. Storage can be a disk drive, flask drive, or SSD. Data on storage is persistent, so when you turn of your laptop or computer, it still gonna be there when you turned it back on. In RAM, you lose the memory when the computer turns off. So, why dont we always store the data in storage if it is persistent? Because, the problem with storage is it is slow. 

## Why do we need to know how the computer works for Data Structure?

Data structure are ways for us to store the information.
In modern computers we represent the intergers in 32 bit
In the below picture, we store number 1 in first 4 block snd number 7 in next 4 blocks.

![Ram blocks](./images/Screen%20Shot%202022-08-27%20at%201.22.44%20PM.png)

Now, we can think how systems that are 8 bit can hold 255 bits of information. 

* 8-bit (11111111) - 255
* 16 bit - 65,536
* 32-bit - 2,147,483,647

A data structure is an arrangement of data. We can define the way we interact with data and how it is arranged in RAM. Some are organized right next to each other and some are organized apart from each other and they have pros and cons in access and write. Our goal is to minimize the operation we need to do for the CPU to get and write the information. And that is why data structures are so powerful. We are thinking of the low level.  

## Data Structures in Different Languages

Each language has its own data types. Every language may not have every data structure from builtin, but we can built it on our own and most of the langauges has enough data strucutures and data types to build on our data strucutures. 

## Operations On Data Structures

Data structures are ways to organize our data on our computers, and there are different variations on how we store data according to differnt data structures. And each data structures has their trade offs. Some are good at certain operation, and others are good at other operation. One operation we can perform with data structures is:

* Insertion: Add a new item in a given collection of items.

* Deletion: Delete data from our list.

* Traversal: Traversal means access each data item exactly once so that it can be processed.

* Searching: We want to find out the location of data item if it exists in a given collection. 

* Sorting: Having data that is sorted.

The most important one is access. How do we access the data that we have on our computer? 