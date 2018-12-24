---
layout: post
title: DS&A Textbooks
excerpt_separator:  "<!--more-->"
categories:
  - coursework
tags:
  - DS&A
  - Study Notes
image: clrs.jpg
---

a compilation of study notes of CLRS and DSA in Python

- TOC
{:toc}

<!--more-->
<img src="{{site.baseurl}}/assets/image/clrs.jpg" style="float: left; width: 10rem; height: auto;">


## module

array, collections, copy, heapq, math, os, random, re, sys, time

## OOP

#### Goal

robustness: handle exception adaptivity: evolve over time reusability:
reuse as component

#### abstract data type

the fundamental of any object interface: publicly supported methods

### OOD

#### principles

abstraction modularity encapsulation: hide internal details in python,
done with loose rule of prefix

#### design rule

responsibility: assign work to actor independency: between classes
communication: class methods can be understood by other classes

#### OOD in python

duck typing abstract base class: built-in class that be inherited,
available in collections module

### design patterns

  - algo recursion, amortization, divide\&conquer, prune\&search, brute
    force, dp, greedy
  - dev iterator, adapter, position, composition, template method,
    locator, factory method

### class

class diagram - UML

### iterator

**iter**, **next**, **getitem**

## object design

### base class

low-level class, to maximize code reuse

### concrete class

build on base class(es), can be instantiated

### abstract class

need to be implemented by subclass(es), should raise error when no
subclass python’s abc module is a formal approach for this
\#backtracking a DFS on implicit graph of possible solutions iterate on
all possible solutions, so correctness is secured prune wisely to be
efficient

## MEMORY MANAGEMENT

allocation, deallocation, reclaim

### mem allocation

the storing space in memory is called memory *heap*. storage available
in heap is divided into blocks. free blocks are kept in a linked list
called *free list*. seperation of free blocks is called *fragmentation*.
\* internal frag a portion of an **allocated** block is unused. the
runtime env cannot do much about it \* external frag frag blocks between
allocated blocks, the real frag use heuristics of memalloc: \* best-fit:
find closest sized hole \* first-fit: search from the beginning of the
free list \* next-fit: search from where previous search left \*
worst-fit: find larlgest hole, faster if the free list is a pqueue. and
works the best since it produces least small frags

### garbage collection

  - live item: have direct of indirect reference direct reference:
    identifier in active namespace active namespace: global namespace,
    local namespace for function, etc. indirect reference: reference
    that occurs within the state of some other live objects

  - python strategy reference count: count the number of reference to an
    object when running ref count with 0 is garbage sys.getrefcount(var)
    is available for user, though results is plused one for explicitly
    called by this func

cycle detection: a cyclic reference has reference count, but they may be
out of scope mark-sweep algo: the mark phase: mark all the root objects
do DFS on roots DFS should be done in-place\! use edge switch instead of
recurrsion the sweep phase:clear all unmarked objects (optional)
organize all objects to one mem block to eliminate external frag

### python intepreter stack / runtime call stack

call, record, frame: one entry of a stack running call: on top of stack,
running suspended calls: rest of stack a call has: a dictionary of
namespace that maps identifiers to values a program counter that
maintain address of the state to recieve return value and continue
excution.

  - another stack: operant stack for arithmatic expression evaluation

## Memory hierarchies and caching

  - Hierarchy CPU, register, cache, internal memory, external memory,
    network storage

### Caching

  - locality of reference temporal: one accessed mem location is likely
    to be accessed again in near future spatial: one accessed mem
    location’s surroundings is likely to be accessed

  - strategy virtual memory: copy unused data in RAM to disk *temporal
    unlikely to use* blocking: when reading from disk, read the
    surrounding block of needed data *spatial likely to use* blocks from
    RAM to CPU is called cache line; from disk to RAM is called page
    when memory full, we need replacing: random, FIFO, Least Recently
    Used

## Disks

disk I/O is slow so data are transfered in *Blocks* number of query
needed is I/O complexity \* B-tree is widely used (b for block) b-tree
of an order d is an (a,b) tree with a=d+1//2 and b=d a b-tree takes
O(n/B) Blocks and I/O complexity O(log\_B(n)) for search and update
query the node: O(log(n)/log(a)) \<- log\_a(n)换底 in the node: a and b
are propotional to B so O(1)

### External memory sorting

k-way merge-sort, on n items, M memory sort: seperately sort M items,
repeat n/M times merge: load k arrays, k = M/B - 1, len(k) = M/(k+1),
one more item for output maintain a k-item pqueue so finding next item
in k arrays in O(logk) whenever output array is full, move to external
and clean; whenever input array is empty, load the next batch internal
merging is O(nlogk) conclusion: time O(nlogn), i/o complexity:
O(nlog\_m(n)), where n = Number/Block, m = Memory/Block \#dynamic
multi-threading \#\#parallel computing \#\#spawn, sync, para-loop

\#matrix special skill on computing matrix

\#linear programming optimization f(x1, x2…xn) based on constraints on
g1(x..), g2, g3 optimization can be max/min constraint g can be
equality(==) and inequality(\<, \>) all f and g are linear \#\# simplex,
duality, graph can convert to linear problems

\#polynomial programming fast fourier transform

\#number theory \#\#divisibility, modular arithmatic, unique
factorization \#\#greatest common divisor, euclid algorithm \#\#a^b mod
n a==b%m: a,b对m同余 a%m == b%m (a-b)%m == 0 \* mod ops: work for +,-,x, (a
op b)%m == (a%m op b%m)%m (a ^ b)%m == (a%m ^ b)%m \* mod inverse: given
a and mod m, a’s mod inverse is b that (axb)%m == 1; a=3, m=7, then b is
5 because 3x5 % 7 == 1 however b exists only if a and m coprime 互质 \*
euclidean algo for greatest common devider given big and small, find
their gcd d **a%d = b%d = (a%b)%d** big, small = small, big%small when
small == 0: return big

\#\#RSA Crypto concerned number always to be large it is convenient to
consider them as polynomial primitive bits, and count calculations as
bit operations, ie. multiplication is O(b^2)

\#string matching included in matching.py

\#computational geometry geometric

\#NP completeness in mit 6006 computation.md \#\#decision
vs. optimization \#\#reduction \#\#TODO

\#approximation algorithm for near optimal solutions to NP problems

\#combinatorial search and heuristic optimization backtracking simulated
annealing
