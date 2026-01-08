---
title: Project 08
subtitle: Conga!
---

## Objectives

1. Practice building List operations.
2. Practice using pointers.
3. Practice test-driven development.

## Introduction

This week's project is to complete a program that simulates a Conga Line dance:

## Simulation Trace

When run, the `CongaLine` simulation should behave like the trace shown below:

```
Ann and Bob have started a Conga Line!

 =Ann=Bob

Conga, Conga, Con-GA!  Conga, Conga, Con-GA!

Please enter:
 1 to join the Conga line at the end
 2 to join the Conga line after a particular person
 3 to join the Conga line before a particular person
 4 to quit
--> 1

What is your name? Chris

 =Ann=Bob=Chris

Conga, Conga, Con-GA!  Conga, Conga, Con-GA!

Please enter:
 1 to join the Conga line at the end
 2 to join the Conga line after a particular person
 3 to join the Conga line before a particular person
 4 to quit
--> 2

What is your name? Don
Who do you want to follow? Ann

 =Ann=Don=Bob=Chris

Conga, Conga, Con-GA!  Conga, Conga, Con-GA!

Please enter:
 1 to join the Conga line at the end
 2 to join the Conga line after a particular person
 3 to join the Conga line before a particular person
 4 to quit
--> 2

What is your name? Eve
Who do you want to follow? Bob

 =Ann=Don=Bob=Eve=Chris

Conga, Conga, Con-GA!  Conga, Conga, Con-GA!

Please enter:
 1 to join the Conga line at the end
 2 to join the Conga line after a particular person
 3 to join the Conga line before a particular person
 4 to quit
--> 2

What is your name? Fred
Who do you want to follow? Chris

 =Ann=Don=Bob=Eve=Chris=Fred

Conga, Conga, Con-GA!  Conga, Conga, Con-GA!

Please enter:
 1 to join the Conga line at the end
 2 to join the Conga line after a particular person
 3 to join the Conga line before a particular person
 4 to quit
--> 3

What is your name? Gwen
Who do you want to precede? Ann

 =Gwen=Ann=Don=Bob=Eve=Chris=Fred

Conga, Conga, Con-GA!  Conga, Conga, Con-GA!

Please enter:
 1 to join the Conga line at the end
 2 to join the Conga line after a particular person
 3 to join the Conga line before a particular person
 4 to quit
--> 3

What is your name? Hal9000
Who do you want to precede? Eve

 =Gwen=Ann=Don=Bob=Hal9000=Eve=Chris=Fred

Conga, Conga, Con-GA!  Conga, Conga, Con-GA!

Please enter:
 1 to join the Conga line at the end
 2 to join the Conga line after a particular person
 3 to join the Conga line before a particular person
 4 to quit
--> 3

What is your name? Ivy
Who do you want to precede? Fred

 =Gwen=Ann=Don=Bob=Hal9000=Eve=Chris=Ivy=Fred

Conga, Conga, Con-GA!  Conga, Conga, Con-GA!

Please enter:
 1 to join the Conga line at the end
 2 to join the Conga line after a particular person
 3 to join the Conga line before a particular person
 4 to quit
--> 2

What is your name? Joe
Who do you want to follow? Bilbo

*** Bilbo is not dancing!

 =Gwen=Ann=Don=Bob=Hal9000=Eve=Chris=Ivy=Fred

Conga, Conga, Con-GA!  Conga, Conga, Con-GA!

Please enter:
 1 to join the Conga line at the end
 2 to join the Conga line after a particular person
 3 to join the Conga line before a particular person
 4 to quit
--> 3

What is your name? Jon
Who do you want to precede? Frodo

*** Frodo is not dancing!

 =Gwen=Ann=Don=Bob=Hal9000=Eve=Chris=Ivy=Fred

Conga, Conga, Con-GA!  Conga, Conga, Con-GA!

Please enter:
 1 to join the Conga line at the end
 2 to join the Conga line after a particular person
 3 to join the Conga line before a particular person
 4 to quit
--> 0

*** 0 is not a valid choice!


 =Gwen=Ann=Don=Bob=Hal9000=Eve=Chris=Ivy=Fred

Conga, Conga, Con-GA!  Conga, Conga, Con-GA!

Please enter:
 1 to join the Conga line at the end
 2 to join the Conga line after a particular person
 3 to join the Conga line before a particular person
 4 to quit
--> 5

*** 5 is not a valid choice!


 =Gwen=Ann=Don=Bob=Hal9000=Eve=Chris=Ivy=Fred

Conga, Conga, Con-GA!  Conga, Conga, Con-GA!

Please enter:
 1 to join the Conga line at the end
 2 to join the Conga line after a particular person
 3 to join the Conga line before a particular person
 4 to quit
--> 4
```

## Details

[Accept the project assignment](FIX THIS) and use git clone to get the files.

The `CongaLine` class in **CongaLine.h** has a `List` member named `myLine`, in which it stores the names of the people currently in the dance line. Since a Conga Line needs to have at least two people, the `CongaLine` constructor has two string parameters to which we can pass two people's names, and our simulation uses this constructor to create an initial line containing "Ann" and "Bob".

Assuming your List template is correct, these files should build (`make tester` and `make proj8`) and run correctly as they are. However, some of the lines in the file **CongaLine.cpp** are "commented out", including:

```cpp
//  if (!myLine.insertAfter(otherPersonsName, yourName)) {
//      cout << "\n***" << otherPersonsName
//           << " is not dancing!\n" << endl;
//  }
```

and

```cpp
//  if (!myLine.insertBefore(otherPersonsName, yourName)) {
//      cout << "\n***" << otherPersonsName
//           << " is not dancing!\n" << endl;
//  }
```

and

```cpp
//  cout << "\n " << myLine << "\n\n";
```

Before you can uncomment these lines, you will need to implement the corresponding List operations in **List.h**.

```{warning}
Aside from uncommenting these lines, you should not make any other changes to **main.cpp**, **CongaLine.h**, or **CongaLine.cpp**.
```

### The insertBefore/After Methods

The semantics of the first two operations are as follows:

- `myLine.insertAfter(otherPersonsName, yourName);` Assuming that `otherPersonsName` is present in `myLine`, this operation should insert `yourName` into `myLine` immediately after `otherPersonsName`.
- `myLine.insertBefore(otherPersonsName, yourName);` Assuming that `otherPersonsName` is present in `myLine`, this operation should insert `yourName` into `myLine` immediately before `otherPersonsName`.

Each operation should work correctly regardless of the position of `otherPersonsName` within `myLine`. If `otherPersonsName` is present within `myLine`, your operation should return **true**; otherwise it should return **false**, so that `CongaLine::run()` can display an error message.

```{important}
To receive full credit for these operations, you should implement them in a time-efficient manner. In particular, you should avoid approaches that use multiple passes through the List, such as (a) first finding the index of the other person (one pass) and then (b) inserting before/after that index (a second pass). Implement each of these methods using a single pass through the List.
```

### The Output operation

The semantics of the third operation are as follows:

```cpp
anyOstream << myLine << ...
```

This `<<` operation should insert the items in `myLine` into the `ostream` that is its left operand, with each item preceded by an "=" separator-string. (The lines in the = character represent a person's arms.)

This operation should return a reference to its left operand, so that these operators can be chained.

```{tip}
This operation should use one of the `writeTo()` methods you implemented last week.
```

### Miscellaneous

You should use test-driven development to implement these operations. A part of your grade will be based on the thoroughness of your tests. Add your tests to the provided **tests.cpp**.

For the insert operations, I strongly encourage you to "design" your method by drawing a diagram of what you want to have happen to the structure in each case. Once you have a diagram to go by, you are more likely to write code that actually does the right thing. (Trial and error is not a good debugging technique.)

If you get to the point where you cannot figure out what is wrong, use the debugger! **The debugger is the best way to debug problems with pointers!**

And finally, here is a [silly video](https://www.youtube.com/watch?v=GvQcA24k3-8), in case you need some inspiration.

## Submit

Make sure you commit your changes and push them to the online repository.

## Grading Rubric

The project is worth 25 pts:

- satisfies all requirements: 3 pts
- `insertAfter()` test: 3 pts
- `insertAfter()` method: 3 pts
- `insertAfter()` efficiency: 1 pt
- `insertBefore()` test: 3 pts
- `insertBefore()` method: 3 pts
- `insertBefore()` efficiency: 1 pt
- `operator<<()` test: 3 pts
- `operator<<` function: 3 pts
- Style/Documentation: 2 pts

Ways students lost points in the past:

- -2: `insertAfter` and `insertBefore` goes through entire list, even after finding `targetNode`
- -4: `insertAfter` and `insertBefore` tests are not sufficient: did not test inserting that fails, explicitly checking node values, etc
- -18: <person1>'s, <person2>'s, <person3>'s, and <person4>'s **List.h** differs only in indentation
- -25: does not compile. Nothing seems to have been implemented
- -3: program crashes when try to insert before a person that is not in the list.
- -1: crashes when insert before first person
- -1: poor indentation! So easy to fix...
- -5: tests do not pass -- cause crash
- -1: insert function(s) do not increment size
- -5: program does not display the Conga Line after changes: impossible to test
- -2: insert functions go through the list twice each
- -2: no tests for \<\< operator
- -2: tests do not test failed insertions
- -3: New people are inserted twice each time
- -1: failed insertions are not communicated to the user
- -9: no tests
- -2: test cases are insufficient: 1 (or 2) successful call to each function is enough to test all cases?
- -3: infinite loop when insert in beginning of list.
