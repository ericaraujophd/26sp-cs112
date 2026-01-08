---
title: Project 00
subtitle: Exploring types, addresses, and more
---

:::{figure} imgs/xkcd-99.png
:alt: XKCD Comic #99 - Binary Heart: A binary representation forming a heart shape
:width: 400px
:align: center

XKCD Comic #99 - Binary Heart ([source: xkcd.com/99/](https://xkcd.com/99/))
:::

## Objectives

Practice creating variables, printing values, printing locations of variables, and so on.

## 1. Setup

1. Click on this assignment invitation and then ["Accept this assignment"](https://classroom.github.com/a/JmVHN27P).
   - Wait a few seconds and refresh the page. Refresh until the page says "You're ready to go!".
   - Click the link to see your new repo on github.com.
   - Click the green <span style="color: green;">Code</span> button, then SSH, and copy the link it shows.
2. In a terminal,
   - `cd` to the directory where you are putting all your CS112 assignments.
   - type: `git clone <paste-the-contents-of-the-link-you-copied>`
   - `cd` to the new directory containing your repo.
   - type `code .` to start up Visual Studio Code in that directory.
3. Inspect the code you got in the assignment.
4. In the terminal, type `make`
   - The code should compile and give you an executable called "**tester**". You can see if it is there by typing `ls`
   - Run the program: type `./tester`
   - You should get some basic output — or at least it should not crash.

## 2. Variables

1. In **functions.cpp**, in `vars()`, create a **constant unsigned integer** called **BIG_NUMBER**, initialized to 10 million.
2. Then, create a variable of type **string** and initialize it to your name. (Note: you will have to `#include <string>` to make this work.)
3. Then, create a variable of type **char** and initialize it to the first letter of your last name.
4. Then, create a variable of type **double** and initialize it to the value 3.1415.
5. Then, create a variable of type **bool** and initialize it to **false**.
6. Then, create a variable of type **long** and initialize it to 0.
7. Compile and run your code by typing `make tester` in the terminal.

```{important}
You'll get warnings about unused variables. Ignore them.
```

```{attention}
At this point in the course, our tester program does not actually test the results in the output. However, when you submit your code to github, an automated testing script will run, which will test if the output is correct. If it isn't, you can then make fixes and resubmit to github.
```

## 3. Hexadecimal addresses

Write code to print out the locations of each of the variables, in hexadecimal, on separate lines.

Compile and then run your program like this:

```bash
./tester step3
```

```{note}
If you get a weird answer for when you print out the location of the char variable, don't worry about it. Just go on.
```

## 4. Number Systems

1. In `ns()`, write code to initialize a variable of type _int_ to the value **37**.
2. Write code to print out the value of that variable in decimal, octal, and hexadecimal, each on its own separate line. You will have to google how to do this in C++.
3. Compile and then test your output by running

```bash
./tester step4
```

## 5. Arrays

1. In `arrays()`, create a variable that will hold an array of 20 floats.
2. Write a line of code to print out the total size of that variable in decimal. Note that you might find `sizeof()` useful.
3. Compile and then test your output by running

```bash
./tester step5
```

## 6. Decrementing Unsigned Integers

1. In `dec()`, create a variable that is an **unsigned integer**, initialized to 0.
2. Write code to decrement the value, and then print it out.
3. Add a comment to your code to explain why you do not see -1 in the output. You may have to ask Google for the answer.
4. Compile and then test your output by running

```bash
./tester step6
```

## Submission

In VS Code, click on the **Source Control** icon on the upper left and type in a commit message, then click the checkmark icon to submit your code.

Go through the various pop-up boxes to commit your changes to your repo.

You should check to see if the automated tests pass. If they do not, then make fixes to your code and commit them and sync them to github, then watch to see if the automated tests pass.

## Grading Rubric

**This lab is worth 12 pts:**

- 2 points for each of steps 3, 4, 5, 6 passing the automated tests.
- 2 points for clean, hospitable code.
- 2 points for following directions correctly.

```{important}
The project is due at **midnight** on Monday. You will receive a 10% per day penalty for lateness.
```

**Examples of how students lost points in the past:**

- -1: Need a comment explaining why the output isn't -1 (Step 6). Output is incorrect for Step 6 because a post-decrement was used.
- -1: unsigned int needs to be const unsigned int (Step 2).
- -1: Code for Step 2 doesn't compile; your string needs to be quoted.
- -1: Hexadecimal output is wrong for Step 4.
- -1: Step 2 doesn't compile. Chars need to be single-quoted.
