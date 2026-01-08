---
title: Lab 06
subtitle: More List Operations
---

## Objectives

In this exercise, you will:

1. Build more List operations.
2. Practice using pointers.

## Introduction

In this week's lab you will add more functionality to the List class we built in class.

[Here is the invite](https://classroom.github.com/a/5XSzmw4g).

Use git clone to get your copy of the assignment, as we have been doing. You should have these files: **List.cpp**, **List.h**, **tests.cpp**, plus a **makefile**, etc.

If you are working with a partner, make sure you join the same Team when creating your repos. Also, put both your names in the _README.md_ file now.

## Step 1. Append

The `append()` method is easy to understand: given a new `Item`, add it to the end of the linked list. The **tests.cpp** file contains tests already for `append()`.

Now, implement the code for `append()`. You might find looking at the implementation of `prepend()` to be helpful -- although `append()` is a bit more complicated. DRAW PICTURES! (Or, don't draw pictures, if you want to make this step of the lab take much longer...)

## Step 2. Searching

Let's implement a method that searches the linked list for a given `Item`, and returns the index of where the item is found, or -1 if it is not found. Name the method `getIndexOf()`. Here is the prototype:

```cpp
int getIndexOf(const Item &it) const;
```

First implement tests of `getIndexOf()` in **tests.cpp**, and then implement the method. You must call the `TEST_CASE` "lookfor". I.e., put this in the **tests.cpp** file:

```cpp
TEST_CASE("lookfor") {
     // add your tests here -- either inside SECTION()s or not.
}
```

## Step 3. Copy constructor

You knew it was coming...

**tests.cpp** does not contain any test cases for this, so you'll have to implement them yourself. My solution has 1 `TEST_CASE` with 3 `SECTIONS`: copying a 0-element List, copying a 1-element List, and copying a $>1$-element list. The name of the TEST_CASE must be "copy":

```cpp
TEST_CASE("copy") {
     // add your tests here -- either inside SECTION()s or not.
}
```

The prototype of the copy constructor will be:

```cpp
List(const List & original);
```

Here is the algorithm to implement the copy constructor:

- Set all the instance variables (`myFirst`, `myLast`, `mySize`) to default values.
- Walk the list of nodes in original, calling `append()` on the value in each node. (You are calling `append()` on "this" node, thus adding a new node each time to the `List` being constructed.)

## Step 4. Equality

Implement the equality method, so that you can test if two `List` objects have the same number of nodes and the items in the nodes are the same. The equality operator returns **true** or **false**.

E.g.,

if `list1` contains 3 values: 11, 22, 33 and `list2` contains four values: 11, 22, 33, 44, then `list1 == list2` should return **false**.

To test this you have to use `==` (not `!=`), so your test might look like this:

```cpp
REQUIRE(! (list1 == list2) );
```

Create your tests first in a test case called "equality":

```cpp
TEST_CASE("equality") {
     // add your tests here -- either inside SECTION()s or not.
}
```

```{tip}
Use a "curr" pointer to each list's `myFirst` node, then in a loop, check if the items are the same for the two nodes, then move each `curr` pointer to its next node.
```

## Step 5. Templatize

Now, convert your `List` class to a `List<Item>` template and modify the tests in **tests.cpp** to test your new template. Remember to edit the **makefile** to remove **List.cpp** from the `SOURCES` line near the top of the file. You should also delete the **List.cpp** file completely from your tree.

## Submit

A part of your grade will be based on the thoroughness of your tests; you may want to model your tests after those provided for you in previous projects.

Don't forget to **Commit** and **Push** your changes to your repo.

Verify you have synced your code to github by going to your online repo webpage and looking to see that the files are correct.

Verify that the autograding tests have passed in github.com.

## Grading Rubric

You will be graded this way: 19 pts total

- 4 pts each for `append()`, `getIndexOf()`, copy constructor, and equality operator (16 pts)
- 3 pts for correctness,
- 1 pt for thorough tests (you get this point free for `append()` for which I've provided tests).
- 3 pts for correctly converting to a class template.

Ways students lost points in the past:

- -3: Incorrect class template conversion, code does not compile;
- -3: Missing tests for `getIndexOf()`, copy constructor, and equality operator
- -1: Incomplete equality tests, no tests for when equality is true
- -1: Append implementation needs to adjust the `myNext` of the current last element
- -1: Copy constructor: `myFirst` is not initialized to **nullptr**, causing tests to fail;
- -1: Missing test for equality operator;
- -1: Incomplete test for copy constructor;
