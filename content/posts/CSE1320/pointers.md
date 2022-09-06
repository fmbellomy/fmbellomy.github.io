---
title: "Intro to Pointers"
date: 2022-08-31T18:47:49-05:00
draft: false
toc: false
readingtime: true
images:
tags:
  - "1320"
  - "C"
  - "Resource"
---
(Preface: I am aware that there are already a million explanations of pointers. I'm fine with writing the 1,000,001st one.)

Pointers are famously confusing for new C programmers, and are a common cause for subtle bugs among even the most seasoned C programmers. 

The goal of this post is to hopefully familiarize you with what a pointer *is,* as well as to how and why you might use one. 
## Memory

A pointer is called a pointer because it "points" to a location in your computer's memory.
Memory is where data that your computer needs right away to perform a computation is stored. 
This includes variables as well the binary representation of the actual code you've written.

Memory is organized as a linear collection of individual bytes, and *every byte of memory has an address.*
Imagine the positive number line, and every single tickmark from 0 upwards has a little space to store a byte of data.
```graphic
(an 'int' is generally 4 bytes wide)
      | (chars are only 1 byte)
      V         |
|----------|    V
[1030032003][e][h][f] <- stored data
(0)(1)(2)(3)(4)(5)(6) <- address
 |  |  |  |  |  |  |
 -------------------
```

When you create a variable in C, it allocates some empty space in what's called *Stack Memory* to store the content of your variable.

```C
// Create a variable and assign to it the value of 8.
// In binary representation, this may look something like 
// 0b00000000 00000000 00000000 00001000
int x = 8;

// On most systems, this will print `4` 
// because `int` is typically 32 bits, or 4 bytes long.
printf("%d", sizeof(int));
```
So variables *have* to take up space in memory in order to exist, and memory has addresses. Great. How is any of this useful?

## How is any of this useful?
Imagine you want to store 20 `int`s, but you don't want to go through the trouble of declaring 20 variables.
The simplest way to go about doing this would be to allocate enough space in memory for 20 ints, and then just slap them all right next to each other. Lets try doing just that.

```C
// malloc() is a function in stdlib.h that 
// tries to give you a pointer to a chunk of memory 
// as big as you ask for.

// In this case, we want enough space for 20 ints.
int* pointer_to_list = malloc(sizeof(int)*20);

// Currently our pointer_to_list is pointing to the very 
// beginning of that chunk of memory, so lets try putting something in it.
// To interact with the memory we have the address of, 
// we use the * operator again, 
// but this time it means to "dereference" the pointer.
*pointer_to_list = 404;

// The first "slot" in our list is now holding a value.
// in other words, bytes 1-4 of our 80 available bytes are now taken up.
// Let's start filling up the rest.

*(pointer_to_list + sizeof(int)) = 0x45;
*(pointer_to_list + sizeof(int)*2) = 0b110100100;
*(pointer_to_list + sizeof(int)*3) = 'a';
// Okay, I've had my fun.
```

You may have noticed that this is very similar to how one would use an array in C. This is because arrays are really pointers behind the scenes, but nobody ever told you that. 

A noticeable difference between declaring an array and declaring a pointer assigned to `malloc()` is that an array is placed into *Stack Memory* whereas `malloc()` will always give you memory from the *heap.* If those words mean nothing to you, that's fine, but for now know that they are different parts of memory and there are subtle differences in how arrays and pointers work because of that fact.

So now we've established pointers can be used to create an array. What else?
Unfortunately, arrays are only the tip of the iceberg. To get to the rest of the crazy things you can do with pointers, we'll have to use a struct.

```C
// If structs are unfamiliar, that's okay.
// Just think of this as a custom type that holds other variables in it.
struct Node{
  // Our node contains an int
  int x;
  // Oh look! A pointer to another instance of this very same type.
  // Because all pointers are the same size in memory,
  // this is actually legal.
  struct Node* next;
};
```
This is a struct with two members. A space to hold an int, and a space to hold a pointer to another Node.
By doing this, you could have a chain of Nodes connected to other Nodes, each holding a piece of data. 
It's *like* an array in the sense that we're creating a *list,* but it's not quite the same.

![linked lists be like](/linked_list_limmy.gif)

The key differences between this new list data structure and an array are that an array is of a fixed size. If you have a full array and you need to add an element to it, you're out of luck. You'll just have to make a new larger array, copy the old one into it, and then insert your new element.

With this list structure, we can just set the pointer of the last node to a new node, and we're done!
A downside of this structure, however, is that in order to find say... the fifth element, we now have to follow a trail of pointers until we get there. This is in comparison to an array where we can just dereference the address `beginning + sizeof(int)*4` to get to the fifth element in one easy step.

So... adding elements is faster with this funky pointer list, but *accessing* it is slower.
That's certainly a tradeoff, and sometimes we may care more about convenience than raw speed. In those cases we may use this data structure over an array.

This is the foundation of *Data Structures and Algorithms,* if you've heard of it before.
Pointers are everywhere in DSA, and DSA is a fundamental skill for programmers and computer scientists everywhere.







