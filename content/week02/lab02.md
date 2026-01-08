---
title: Lab 02
subtitle: File I/O, Control Structures, and the Debugger
date: 3 Mar 2026
---

## Objectives

In this exercise, you will:

1. Read in a file and process its contents.
2. Practice creating functions
3. Practice writing `for` loops and `if` statements.
4. Use the debugger to execute a program statement by statement.

## Step 0. Prepare

```{warning}
Find a partner before starting anything!
```

1. Click [this link](https://classroom.github.com/a/nyshxnJo) and then scroll down to choose a Team name. "Accept this assignment".
   - Wait a few seconds and refresh the page. Refresh until the page says "You're ready to go!". The page has a link to a github repo.
   - Click the link to see your new repo on github.com.
   - Click the green <span style="color: green;">Code</span> button and copy the SSH link it shows.
2. In a terminal,
   - `cd` to the directory where you are putting all your CS112 assignments.
   - type `git clone paste-the-contents-of-the-link-you-copied`
3. In VS Code, "Open Folder" and navigate to your newly created repository.
   - Make sure both you and your partner are in the same Team for this assignment. Only one of you will work on the code at a time during the session.
   - Inspect the code you got in the assignment.

## Finding duplicates in an array of integers

In this assignment, you will write a short function, `findDuplicate()`, that searches an array of integers to find the first pair of duplicate values. Please read this entire section before starting to code -- we'll do that in the next section! For our `findDuplicate()` function, if a duplicate value is found, the function returns **true**, and "returns" the duplicate value through an _Out_ parameter. If no duplicate value is found, the function returns **false**.

Think about the algorithm to find a duplicate value in an array. Consider the following array:

```
+----+---+----+---+---+
| 11 | 7 | 31 | 4 | 7 |
+----+---+----+---+---+
```

How would you write code to detect that 7 is in the array twice? Talk to your partner about your algorithm. I highly recommend you write pseudo-code for your algorithm. If you want to finish the lab in an efficient way, you'll take time to write the algorithm and test it on some inputs, revising it until you get it right.

When you have an algorithm, consider this array:

```
+----+---+---+---+----+
| 11 | 7 | 7 | 4 | 71 |
+----+---+---+---+----+
```

And this array:

```
+---+----+----+----+----+
| 7 | 43 | 31 | 12 | 71 |
+---+----+----+----+----+
```

Does your algorithm seem to work on these arrays? Will your algorithm work for arrays with 10,000 values? How about an array with 0 elements or 1 element? Does it work?

## Step 1. Write the function

In **functions.h**, write the **prototype** for your function. The prototype is just the first line of the function, without the actual implementation. Study the table below to understand what parameters the function should take. Then try to write that first line of the function. If you can't get it, I'll give the answer just below the table.

Your function is called `findDuplicate()`, has 3 parameters, and returns **bool**.

| Parameter name | Parameter type | Description                                                              |
| -------------- | -------------- | ------------------------------------------------------------------------ |
| arr            | array of int   | arr of integers to search                                                |
| size           | int            | size of the array                                                        |
| dup_value      | int &          | The out parameter containing the first duplicate value, if one is found. |

The function's prototype should look like this:

```cpp
bool findDuplicate(int arr[], int size, int &dup_value);
```

That's all that you should have in your header (.h) file.

In **functions.cpp**, implement your function. To repeat from above: If a duplicate value is found, the function returns **true**, and "returns" the duplicate value through the _out_ parameter, **dup_value**. If no duplicate value is found, the function returns **false**. Work from your algorithm. Do your best to implement the function correctly, but don't take too much time on this, as the next steps will help you make sure your code is correct.

## Step 2. Unit test your function

Take a look at the file **tests.cpp**. This file uses a unit testing framework called **catch**, implemented in **catch.hpp**.

Notice that the file `#includes "functions.h"` and calls `findDuplicate()` one or more times in each test. The results of the call to `findDuplicate()` are tested by `REQUIRE` statements, which are basically identical to the `assert()` statements we've been using.

When you compile your code using `make tester`, a **tester** executable is created. That executable runs the code in **tests.cpp**, but also allows you to do much more: you can just list the tests, run only some of the tests, configure how the output should look, etc.

Try compiling your code by typing `make tester`. If it builds, try running `./tester -s` to see output from all the tests that are executed.

To run only the first test, you can do:

```bash
./tester "findDuplicate size 0"
```

```{warning}
If your code does not pass this test, try fixing it. Take 5 minutes maximum to try to fix your code. Whether you succeed or not, go on.
```

## Step 3. Using the Debugger

A debugger is a program that allows you to set breakpoints in your code, and then run your code. When a breakpoint is encountered, the debugger stops, and allows you to view variables' values, the call stack, etc.

[This video](https://youtu.be/vfPY7qFnDZI) shows you how to use the debugger with VS Code. You should watch the video now, or as a homework exercise. Then, go down to **Step 3.5** below.

If you cannot watch the video, I'll describe how to use the debugger here:

Open your file that you want to debug. E.g., your **functions.cpp** file. Here is mine:

```{figure} imgs/img1.png
---
name: img1
---
functions.cpp
```

You can see that I have a good start on the function, but it isn't complete. But, I want to make sure I'm passing in my parameters correctly, and a good way to do that is to use the debugger.

**The first thing I have to do** is build the project:

```bash
make tester
```

If you look at **tests.cpp**, you can see a bunch of calls to `findDuplicate()`, from line 10, line 21, etc.

To check if our parameters are being passed in correctly, **let's set a breakpoint** on line 2. To do that, put your pointer to the left of the 2 on line 2, and click. You should see a red dot.

```{figure} imgs/img2.png
---
name: img2
---
Set a breakpoint on line 2
```

You can set multiple breakpoints at the same time. You could, for example, set a breakpoint on line 3 and line 5, so that you can see in what circumstances your code returns **true** or **false**.

Now, we can **start the debugger**. The easiest way is to hit F5. Or you can go to **Run -\> Start Debugging**.

(If you get a weird error, just go on here. You might be trying to debug the wrong executable.)

When you start debugging (successfully), your screen changes quite a bit.

You'll see a menu bar appear at the top of the screen. You'll also see the debugging icon on the left side become bright:

```{figure} imgs/img3.png
---
name: img3
---
Debugging icon
```

You'll see a debugging window on the left side. And, you'll see your code run and the debugger will stop at the first breakpoint:

```{figure} imgs/img4.png
---
name: img4
---
Debugger has stopped at the breakpoint
```

```{caution}
If you saw an error when you started debugging, you might be trying to debug the wrong executable. Look at the image just above. Notice that next to the green arrow is a small menu, with a dropdown arrow. You might be trying to debug the "Debug lab2" program instead of the tester program.
```

You know where your code has stopped because you see the yellow "arrow" overlaying the red dot. This means your code has run to this point and is stopped.

On the lower-left corner you see the call stack. The top frame in the call stack is `findDuplicate()`. Below that you see that `findDuplicate()` was called from **C_A_T_C_H_T_E_S_T_0()** in **tests.cpp** at line 10. Click on that to see **tests.cpp** and where it called `findDuplicate()`.

```{figure} imgs/img5.gif
---
name: img5
---
Click on C_A_T_C_H_T_E_S_T_0() to see where findDuplicate() was called from.
```

Now, to continue from the breakpoint, we can use the menu bar at the top. If you hover your mouse over the items in the menu bar, you'll see: Continue (F5), Step Over (F10), Step Into (F11), Step Out (Shift F11), and Stop (Shift-F5). Step Over really means "go to the next line".

```{figure} imgs/img6.gif
---
name: img6
---
Use the menu bar to control execution of your code.
```

Click on **Step Over** now. You should see your pointer go to line 3, which returns **false**. Step Over a few more times, and you'll get back to **tests.cpp**, line 11. Now, click **Continue**. That will make the debugger run the code again until it encounters the next breakpoint -- which is back at line 2 of **functions.cpp**. You can again inspect the parameter values.

Click **Continue** again. Notice that you are still at line 2, but look closely to see where `findDuplicates()` was called from. Which line of **tests.cpp** called `findDuplicates()`?

Click on **C_A_T_C_H_T_E_S_T_6()** on the lower-left corner of the screen, and look at the values of the Local variables in the upper-right corner. What values are in the numbers array?

This really concludes our introduction to using the debugger.

## Step 3.5 Caveats

📌 **Please note these caveats:**

- If you make changes to your code, you have to recompile before using the debugger again. Starting or restarting the debugger will not first recompile your code! (To recompile, use make tester .)

## Step 4. Get your code working against all tests

Using the debugger and your brain 🧠, fix your code such that it passes all the tests when you run

```bash
./tester
```

## Step 5. Implement your application

Now that you have a good function that finds duplicates, use it to implement a simple application.

Look in **main.cpp**, where you will find the steps to implement, as comments.

Compile your code with

```bash
make lab2
```

Implement steps 1 - 6 of the algorithm. Step 4 is implemented for you already (assuming you read in the number of lines in the file into a variable named size).

I **HIGHLY RECOMMEND YOU IMPLEMENT** your code in small iterations: just write the code for Step 1., compile it and make sure it is correct. Then go on to Step 2. Repeat...

Step 7. says to "print appropriate output". This means your application should either print out that there are no duplicates, or should print out that a duplicate was found, and should print what that duplicate value is. E.g., here are a few runs of my solution:

```bash
% ./lab2
Enter a filename: input_files/in0.txt
Enter the number of lines in the file: 0
No duplicate number was found.
```

and another run:

```bash
% ./lab2
Enter a filename: input_files/in5.txt
Enter the number of lines in the file: 5
A duplicate number, 91, has been found.
```

```{note}
Your output must match the output above EXACTLY. You should try your solution against all the files in the `input_files/` directory. These files will be used in the autograding tests run when you submit.
```

## Submit

In VS Code, click on the **Source Control** icon on the upper left and type in a commit message, then click the checkmark icon to submit your code. Go through the various pop-up boxes to commit and SYNC your changes to your repo.

Verify you have synced your code to github by going to your online repo webpage and looking to see that the files are correct.

Also, check to see that the automated tests pass.

## Grading Rubric

Your submission will be graded this way: 19 pts total

- 10 pts for a correct function implementation
- 8 pts for correct code in main().
- 1 pts for style: good variable names, perfect indentation, etc.

Ways students have lost points in the past:

- -1: For loop in main.cpp has no body (or no semicolon, either way the code did not compile).
- -1: No assert statement for when the file is not opened; missing body or semicolon causes the "numbers" variable not to be recognized by the compiler.
- -10% (-1.8) for 1 day late.
- -1: Improper indentation in main.cpp.
- -1: Poor formatting.
- -1: Array not dynamically allocated with "new" (Step 4).

<!-- [^1]: how to add footnotes. -->
