---
title : "Linked List Basics"
author : pu71n
layout : post
category : C
---
### Why Linked Lists ?
Linked lists and arrays are similar since both store collections of data. The terminology is that arrays and linked lists store "elements" on behalf of "client "code". The specific type of element is not important since essentially the same structure works to store elements of any type. 
Linked lists have their own strenghs and weaknesses, but they happen to be strong where arrays are weak. The array's features all follow from its strategy of allocating the memory for all its elements in one block of memory. Linked lists use an entirely different strategy. As we will see, linked lists allocate memory for each element separately and only when necessary. 

### Pointer Refresher 
Here is a quick review of the terminology and rules for pointers. The linked list code to follow will depend on these rules.

* **Pointer/Pointee** : A "pointer" stores a reference to another variable sometimes know as its "pointee". Alternately, a pointer may be set to the value NULL which encodes that it does not currently refer to a pointee.
* **Dereference** : The dereference operation on a pointer accesses its pointee. A pointer may only be dereferenced after it has been set to refer to a specific pointee. A pointer which does not have a pointee is "bad" and should not be dereferenced. 
* **Bad Pointer** : A pointer which does not have an assigned a pointee is "bad" and should not be dereferenced. In C and C++, a dereference on a bad sometimes crashed immediately at the dereference and sometimes randomly corrupts the memory of the running program, causing a crash or incorrect computation later. That sort of random bug is difficult to track down. In C and C++, all pointers start out with bad values, so it is easy to use bad pointer accidentally. Correct code sets each pointer to have a good value before using it. Accidentally using a pointer when it is bad is the most common bug in pointer code. In Java and other runtime oriented, pointers automatically start out with the NULL value, so dereferencing one is detected immediately. Java programs are much easier to debug for this reason.
* **Pointer assignment** : An assignment operation between two pointers like p=q; makes the two pointers point to the same pointee. It does not copy the pointee memory. After the assignment both pointers will point to the same pointee memory which is know as a "sharing" situation.
* **malloc()** : malloc() is a system function which allocates a block of memory in the "heap" and returns a pointer to the new block. The prototype for malloc() and other heap functions are in *stdlib.h*. The argument to malloc() is the integer size of the block in bytes. *Unlike local "stack" variables*, heap memory is not automatically *deallocated* when the creating function exits. malloc() returns NULL if it cannot fulfull the request. You may *check* for the NULL case with **assert()** if you wish just to be safe. Most modern programming systems will throw an exception or do some other automatic error handling in their memory allocator, so it is becoming less common that source code needs to explicitly check for allocation failures.
* **free()** : free() is the opposite of malloc(). Call free() on a block of heap memory to indicate to the system that you are done with it. The argument to free() is a pointer to a block of memory in the heap 


### What Linked Lists Look LikeA "pointer" stores a reference to another variable sometimes know as its "pointee". Alternately, a pointer may be set to the value NULL which encodes that it does not currently refer to a pointee.
* **Dereference** : The dereference operation on a pointer accesses its pointee. A pointer may only be dereferenced after it has been set to refer to a specific pointee. A pointer which does not have a pointee is "bad" and should not be dereferenced. 
* **Bad Pointer** : A pointer which does not have an assigned a pointee is "bad" and should not be dereferenced. In C and C++, a dereference on a bad sometimes crashed immediately at the dereference and sometimes randomly corrupts the memory of the running program, causing a crash or incorrect computation later. That sort of random bug is difficult to track down. In C and C++, all pointers start out with bad values, so it is easy to use bad pointer accidentally. Correct code sets each pointer to have a good value before using it. Accidentally using a pointer when it is bad is the most common bug in pointer code. In Java and other runtime oriented, pointers automatically start out with the NULL value, so dereferencing one is detected immediately. Java programs are much easier to debug for this reason.
* **Pointer assignment** : An assignment operation between two pointers like p=q; makes the two pointers point to the same pointee. It does not copy the pointee memory. After the assignment both pointers will point to the same pointee memory which is know as a "sharing" situation.
* **malloc()** : malloc() is a system function which allocates a block of memory in the "heap" and returns a pointer to the new block. The prototype for malloc() and other heap functions are in *stdlib.h*. The argument to malloc() is the integer size of the block in bytes. *Unlike local "stack" variables*, heap memory is not automatically *deallocated* when the creating function exits. malloc() returns NULL if it cannot fulfull the request. You may *check* for the NULL case with **assert()** if you wish just to be safe. Most modern programming systems will throw an exception or do some other automatic error handling in their memory allocator, so it is becoming less common that source code needs to explicitly check for allocation failures.
* **free()** : free() is the opposite of malloc(). Call free() on a block of heap memory to indicate to the system that you are done with it. The argument to free() is a pointer to a block of memory in the heap 


### What Linked Lists Look Like ?
An array allocates memory for all its elements lumped together as one block of memory. In contrast, a linked list allocates space for each element separately in its own block of memory called a "linked list element" or "node". The list gets is overall structure by using pointers to connect all its nodes together like the links in a chain.
Each node contains two fields: a *data* field to store whatever element type the list holds for its client, and a *next* field which is a pointer used to link one node to the next node. Each node is allocated in the heap with a call to malloc(), so the node memory continues to exist until it is explicitly deallocated with a call to free(). The front of the list is a pointer to the first node.
<br>

<pre>
struct list_float          /*     ---------    ---------           */
{                          /*     | Value |    | Value |           */
  float             value; /*     |  ---  |    |  ---  |           */
  struct list_float *next; /*     |  next-|--> |  next-|--> NULL   */
}                          /*     ---------    ---------           */
</pre>

### The Empty List - NULL
The above is a list pointed to by head is described as being of "length two" since it's made of two nodes with the .next field of the last node set to NULL. There needs to be some representation of the empty list - the list with zero nodes. The most common representation chosen for the empty list is a NULL head pointer.

### Linked List Types: Nodes and Pointer
Before writing the code to build the above list, we need two data types:
1. **Node** : The type for the nodes which will make up the body of the list. These are allocated in the heap. Each node contains a single client data element and a pointer to the next node in the list.
<pre>
struct node {
	int data; 
	struct node* next; 
};
</pre>
2. **Node Pointer** : The type for pointers to nodes. This will be the type of the head pointer and the .next fields inside each node.

<div>
<iframe src="https://drive.google.com/drive/folders/1dvzwPt_Qs1TqWQXTEr2AlqjocTfU-6Gb?usp=sharing#list" style="width:100%; height:600px; border:0;"></iframe>
</div>
