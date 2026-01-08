---
title: Lab 10
subtitle: Recursion
---

## Learning Objectives

Students will be able to...

- use an AI model to write code to implement recursive algorithms.
- analyze the code from an AI model

## Introduction

In this lab, for most steps, you will use ChatGPT or another AI model to generate recursive solutions to some simple problems. You will then analyze the code to verify it is correct and/or improve it.

To log in to ChatGPT (as if you didn't already know :-), go to [https://chatgpt.com](https://chatgpt.com).

After the AI generates C++ code, copy and paste it into a file, and compile and run it. You will be submitting multiple files each containing a `main()` in it.

[Accept the assignment](https://classroom.github.com/a/EQo-iiMU).

## Part 1: Reverse an array, recursively

Ask ChatGPT for C++ code to reverse an array of integers recursively. When you are happy with the code that has been generated for you, copy and paste it into file **rev_array.cpp**. Compile and run the file by doing `make rev_array` and `./rev_array`.

Describe in a few complete English sentences how the solution works. Put your answers in comments in the file. (Do not use the AI to generate this answer.)

What if the array has an odd number of values? How does the algorithm handle this? (Do not use the AI to generate this answer.)

## Part 2: Binary search, recursively

Ask ChatGPT for C++ code to implement a recursive version of binary search over an array of integers. (doubles?)

When you are happy with the resulting code, place it in **bin_search.cpp**, compile it, and run it (if you can't figure out how to do these steps, inspect the `makefile`). Make sure the code works for arrays of different sizes, including size 0, size 1, size 10, etc.

Your code probably contains this line:

```cpp
int mid = low + (high - low) / 2;
```

Describe in a comment above this line what this line does and why it works when the size of the array is odd (which means you cannot divide the array into two even parts). (Do not use the AI to generate this answer.)

## Part 3: Sum of values in an array, recursively

Place the code from Slide 5 of the lecture slides into file **sum_array.cpp**. Add other code to initialize an array with 6 values. Compile and run the value and verify that the result is correct.

Now, modify the code so that the base case is not when `size == 0` but when `size == 1`.

Describe in a comment in the file why this solution is slightly more efficient.

## Part 4: Fibonacci sequence, recursively

Ask the AI to generate C++ code to compute recursively the _nth_ fibonacci number, where the user provides the value for $n$. Copy and paste the code into file **fib.cpp**. Then, compile and run the code. Verify that the results are correct (you can ask the AI for the correct answer when $n$ is 20).

Ask the AI to modify the C++ code so that it counts how many times the recursive function is called and prints out the results at the end.

Put the code into your file and compile and run it. Add the results for when $n$ is 20 in a comment in the code at the bottom of the file.

Now, ask the AI to modify the code to use memoization. The code should still count and display the number of times the function `fibonacci()` is called.

Add to your comment at the bottom of the file the results for when memoization is used. Also, write a sentence or two (in the comment) to describe how memoization works and how it improves the run time of the algorithm. (Do not use the AI to generate this answer)

```{important} Submit
Don't forget to submit all your code to github.
```

## Grading Rubric

20 points total

- 5 points for each of the 4 parts. Those 5 points consist of:
  - 2 points for code correctness
  - 3 points for your analysis of the code.

Ways students lost points in the past:

- -12: no analysis was given.
- -3: some of the questions were not answered properly.
