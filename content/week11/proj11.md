---
title: Project 11
subtitle: Binary Search Trees
---

## Objectives

1. Practice building BST operations.
2. Practice building recursive operations.
3. Learn more about binary search trees.

## Introduction

[Accept the assignment](https://classroom.github.com/a/0K0eddFV) and use `git clone` to create your copy of the code.

The tasks for this project are:

1. Add a `getHeight()` to your BST class.
2. Use your `BST<Item>` to conduct an experiment.

As usual, you should use test-driven development to accomplish these tasks. Note that part of your grade is based on the thoroughness of your new tests for `getHeight()`.

```{important}
Copy your **Exception.h**, **catch.hpp**, **BST.h**, **makefile**, and **tests.cpp** files from your previous lab, into your repo.
```

## Adding `getHeight()`

The height of a tree with a root node is defined as the height of the node's taller sub-tree, plus 1. As you can see, this is a **recursive** definition, which needs a **base case**. The base case is that if a node has no children, its height is 1.

Let's give some examples to clarify:

- If a tree has no nodes, its height is 0. If a tree has 1 node — the root node — its height is 1.
- If a tree has a root node and that node has either a left child or a right child, or both, its height is 2. Suppose the tree has a root node and that node has a single right child node. The right child node has height 1. The root node's height is 1 + (the greater of the height of its left subtree — which is 0 — and the right subtree — which is 1). Thus, the root node's height is 2.

Implement `getHeight()` now. Its implementation is similar to `insert()` or a traversal algorithm in that it uses recursion. The difference here is that each function returns an integer — the node's height.

### The Experiment

The height of a BST determines the speed of operations like `insert()` and `contains()`. If we build a "large" BST of N items (e.g., \~$2^{20}$), and that tree is balanced, then its height should be the minimal $O(lg(N))$ (e.g., 20).

This week's problem is to conduct a simple experiment to see how "tall" BSTs get, given random values. Our objective is to see how close we come to lg(N) height if we build large trees of N randomly ordered values.

Your repo contains two directories that each contain ten data files (**randomInts01.txt**, **randomInts02.txt**, ..., **randomInts10.txt**), each containing $2^{20}-1 = 1,048,575$ randomly generated integer values. If these values were ordered in exactly the right way, we could build trees of height 20. (On the other hand, if they were ordered in exactly the wrong way, we could build trees of height 1,048,575!)

Your task is to write a simple program that prompts the user for the name of an input file, reads each value from that file, and inserts it into a BST. Your program should then display the height of the resulting BST.

There are minor details to keep in mind:

- There may be duplicate values within an input file, and inserting a duplicate value into our BST will throw an exception. Your program should count and output the number of duplicate values in a given file by catching and handling this exception.
- There are two directories — one for Linux/MacOS, and one for Windows.
- These files were generated in the Maroon lab (whose workstations are 64-bit machines), and so the integers in these files are 64-bit integers. However, the C++ int and unsigned types only store integers in 32 bits; the long type stores integers in 64 bits, so use it to store these 64-bit integers.

Since there are ten input files, you will need to run your program ten times. (Or find a clever way to automate this.) For each file, record the corresponding tree-height in a spreadsheet, and the number of duplicate values that were found. Given all ten heights, use the spreadsheet to calculate the minimum height, the maximum height, the average height, the median height, and the standard deviation of the ten heights. (Your spreadsheet will make each of these computations easy.) Finally, use your spreadsheet to create a bar-chart showing each of the ten heights, as a visualization of your data. Finally

Answer the following questions in your spreadsheet, below the chart:

1. Is $lg(N)$ or $N$ a better approximation for your measured heights? Why?
2. How much variance is there in the height of these trees? Is this surprising? Why or why not?
3. How many duplicate values were there (on average)? Is this surprising? Why or why not?
4. The "big Oh" notation $O(f(n))$ implies that there are constants $a$ and $b$, such that $a \times f(n) + b$ describes the reality for which $O(f(n))$ is an approximation. A balanced BST of $N$ items has height $O(lg(N))$. Theoretically, there should be values $a$ and $b$ such that $a \times lg(N) + b$ describes the actual height of a BST built using random data. Using your experimental results, what is a reasonable value for $a$?

## Submission

```{important}
👉👉👉 Download/export a PDF version of your chart and store it in your repo for submission. Call the file **analysis.pdf**.
```

Don't forget to commit your code to your online repo on [github.com](https://github.com/) so that the grader can grade it.

## Grading Rubric

Total: 24 pts

- `getHeight()`: 5 pts
- New tests in **tests.cpp** for `getHeight()`: 3 pts
- program: 10 pts
- spreadsheet / analysis: 6 pts

Ways students have lost points in the past:

- -3: Missing chart, spreadsheet
- -6: Missing spreadsheet/analysis
- -3: Missing tests for `getHeight()`
- -1: Big-Oh of height was wrong.
- -1: Error in `getHeight()`: a tree with two items could either have a height of 1 or 2
