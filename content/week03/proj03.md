---
title: Project 03
subtitle: A High Scores Class
---

## Introduction

You will build a `HighScores` class that keeps track of the top-10 scores for a game. The class will store the scores from highest-to-lowest, and only store at most 10 scores. It will keep track of how many high scores are being stored. The class must store the scores in an array.

The methods that must be defined for the class are: `addScore(int score)`, `getScore(i)`, and `getNumScores()`, plus, of course, the default constructor. <!-- These methods need better explanation -->

## Step 0. Prepare

1. Click [this link](https://classroom.github.com/a/dizN1gff) and then "Accept this assignment".
   - Wait a few seconds and refresh the page. Refresh until the page says "You're ready to go!". The page has a link to a github repo.
   - Click the link to see your new repo on github.com.
   - Click the green <span style="color: green;">Code</span> button and copy the link it shows.
2. In a terminal,
   - `cd` to the directory where you are putting all your CS112 assignments.
   - type `git clone paste-the-contents-of-the-link-you-copied`
   - `cd` to the new directory containing your repo.
   - type `code .` to start up Visual Studio Code in that directory.
3. Inspect the code you got in the assignment.
   - In the terminal, type `make tester`
   - The code should compile and give you an executable called **tester**
   - Run the program: type `./tester`
4. You should get some basic output — or at least it should not crash.

## Step 1. Starting slow...

1. Create a `TEST_CASE` that creates a HighScores object, and a `SECTION("getNumScores")` that calls `getNumScores()` on that object, and then REQUIREs that the result is 0. Compile (`make tester`) and see errors.
2. Now, in **HighScores.h**, create the HighScores class and in the class's **private:** section, create an array of size 10 of integers called `myScores`. And, create a variable called `myNumScores` that stores how many scores are being stored. Don't forget to create the prototypes for the constructor and the other methods.
3. In **HighScores.cpp** implement the constructor, initializing both variables. You will have to write a loop to initialize every entry of `myScores` to 0.
4. Create the getter `getNumScores()`. Then, compile and run: your test should now pass.

## Step 2. Adding a first score

In **tests.cpp**, add another test in a `SECTION("addScore")` to call `addScore(30)` and then `getNumScores()` and REQUIRE that the value is 1. Compile and see the errors. Fix them by doing the following:

- Create the `addScore(int aScore)` method in the .h and .cpp files (the function returns **void**).
- Implement it by just adding the score to the array at index `myNumScores`. Then increment `myNumScores`.
- Now, your test should pass. (However, if we call `addScore()` multiple times, the scores may not be sorted properly. But we'll deal with that later.)

## Step 3. Adding many scores

In **tests.cpp**, create a loop to add 10 more scores to your **HighScores** object; thus, there should be 11 calls to `addScore()` made. Then, REQUIRE that the number of scores being stored is 10 — the maximum the object should store. This test should fail because our code does not check for a full array.

Fix the problem by adding code to make sure you only ever store at most 10 scores. Add the code to `addScore()`: if the array is full — i.e., `myNumScores == 10`, just return — do not try to add the new score.

```{note}
This is not a correct solution, but for the time being, it is good enough.
```

Also, at this time, implement the method `getScore(i)`. The parameter is an index of the score to return. For example, if the array has the value 42 at index 7 and the code calls `getScore(7)`, the value 42 should be returned. You should write multiple tests to make sure the results you get are correct.

If the user passes in an invalid index — i.e., an index that is $>= myNumScores$, throw an **invalid_argument** exception. (include `<stdexcept>` and add the `using namespace std;` stuff). Use `REQUIRE_THROWS_AS()` to test if the exception is thrown.

```{tip}
Look at **tests.cpp** in Lab 03 to see an example.
```

## Step 4. Keep the scores sorted

Now, the fun part: when we insert a score into the array, we don't want to just add it to the "end" of the array. Instead, we want to keep the array sorted **from highest score to lowest**. So it should be inserted into the array **after** all the scores that are **higher** than it and **before** all scores that are **less than or equal** to it. In order to do this, we'll have to shift over any lower scores before inserting the new score into the array.

For example, suppose the array looks like this:

```{list-table}
:header-rows: 0

* - 100
  - 95
  - 93
  - 89
  - 87
  - 70
  - 49
  - 22
  - 19
  - 17
```

and `myNumScores = 10`.

If the main code now calls `addScore(77)`, the array should look like this:

```{list-table}
:header-rows: 0

* - 100
  - 95
  - 93
  - 89
  - 87
  - **77**
  - 70
  - 49
  - 22
  - 19
```

Notice that every number $<= 77$ has been shifted up in the array, and the last number has been "lost". Even though we have called `addScore()` 11 times, `myNumScores` is still 10.

To implement this, your code has to first iterate through the array and find the location where the new high score should be inserted — in this case, that location is index 5. Then, your code needs to copy values up in the array — starting at index 8, where the value 19 is in the example. You move the value at index 8 to index 9, then the value at index 7 to index 8, etc. Finally, the code needs to insert the new value into the place it should go.

To summarize, the algorithm for `addScore(score)` is:

1. find the location to insert the new score — checking if the result is -1. If so, return;
2. shift every other value up;
3. add the new score to the array at the found location.
4. increment the number of scores stored — but only if the array was not full before adding the new value.

(When the array was full, then the lowest high score was "lost".)

To implement this, you must create two **private** methods in the class:

```{list-table}
:header-rows: 1

* - Method name
  - Parameters
  - Return type
* - `findLocationToInsert()`
  - `int newScore`
  - `int`: the index of where to insert the newScore, or -1 if the score is not a new high score.
* - `shiftUp()`
  - `int fromIndex`
  - `void`
```

```{important}
If the new score is **lower** than all stored high scores, `findLocationToInsert` should return -1. Your code in `addScore()` should handle this situation, as shown in the algorithm above.
```

```{note} NOTE 1
About `findLocationToInsert()`: loop from 0 to 9 so that your code can discover if the `newScore` should go at the end of the array. This will work because we've initialized the array to all 0s and we assume all scores are $>= 0$.
```

Add the prototypes to your .h file and add empty "skeleton" implementations in your .cpp file. Implement the algorithm above in your `addScore()` method. That implementation should be something like 7 lines of code.

**Before** you implement the code, change your tests in **tests.cpp**. Your tests will have to assume that when `addScore()` is called, the value is inserted into the correct place, thus keeping the array sorted. So, some of your tests that assumed a value would always be added at the end will have to be replaced/fixed.

```{note} NOTE 2

Getting these tests correct is crucial. I added a comment after most of my calls to `addScore()` to state what the array should be holding at that point. That helped me keep track of how the code should be behaving and what my tests should test for.
```

Now, implement the **two private** methods. Both must use for loops.

```{note} NOTE 3

You might find it really useful to create a function to print out the high scores in the object (check the Pair class example). Then, you can call that function from various places to see what the array really holds.
```

Once you get things working, take another look at your tests. Do you need to add more tests to cover every situation? If so, add them. You'll be graded on how good your tests are.

## Submission

Take another look at the Grading Rubric below and make changes to maximize your score.

**Commit and Sync** your code to your online repo.

```{important}
Verify you have synced your code to github by going to your online repo webpage and looking to see that the files are correct.

**Also**, verify that the automated test passes. The test is the same as **tests.cpp**.
```

### Grading Rubric

This project is worth 22 pts:

- 15 pts for correctness
- 2 pt for perfect indentation and good variable names, function names, and comments (i.e., hospitable code). You should write a comment in your code only when the following block of code is not obvious to the trained reader. You should not write a comment for each line of code. Writing a comment above the non-obvious methods can be very useful.
- 5 pts for sufficient test cases to prove that the code is correct.

Ways students have lost points in the past:

- -3: can't make tester
- -2: Tests don't pass
- -22: No submission
