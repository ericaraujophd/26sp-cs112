---
title: Lab 05
subtitle: Generic Containers (Templates)
---

## Objectives

In this exercise, you will:

1. Learn about generic containers.
2. Convert a container class into a class template.

## Set up

1. Click [this link](https://classroom.github.com/a/0pyt0v8A) and then "Accept this assignment".

- Wait a few seconds and refresh the page. Refresh until the page says "You're ready to go!". The page has a link to a github repo.
- Click the link to see your new repo on github.com.
- Click the green <span style="color: green;">Code</span> button and copy the SSH link it shows.

2. In a terminal,
   - `cd` to the directory where you are putting all your CS112 assignments.
   - type `git clone paste-the-contents-of-the-link-you-copied`
   - `cd` to the new directory containing your repo.
   - type `code .` to start up Visual Studio Code in that directory.
3. Inspect the code you got in the assignment.

```{warning}
Make sure you and your partner are in the same Team. Edit `README.md` and put your name and your programming partner's name in the file.
```

## Part I

In last week's exercise, we built a simple but useful vector class named `Vec`, that stored real (i.e., double) values. To make it easy to change the type of items stored in our Vec, we used a typedef of the form:

```cpp
typedef double Item;
```

We then meticulously used the name `Item` everywhere we would have used the type double. By doing so, a user wanting to use a vector of integers could just modify the typedef:

```cpp
typedef int Item;
```

recompile, and our Vec would be a vector of integers!

This approach works fine for simple problems where all of the vectors store the same types of values. However suppose you need vectors of both integer and real items (or some other type of item) in the same program? In this situation, the typedef approach cannot help us -- we need a different approach.

Part I of today's exercise is to convert our Vec class into a **generic container** -- a container capable of storing any type of item. To do so in C++, we convert the Vec class into a **class template**. Because we have used the typedef-Item approach to define our Vec class, this conversion is fairly simple.

The tests in the provided **tests.cpp** have **not** been revised to use a **Vec template**. You will be changing **Vec.h**, **Vec.cpp**, and **tests.cpp** in today's exercise.

As its name suggests, a **class template** is a plan or blueprint from which the compiler can build a class. Once we have converted our Vec class into a `Vec<Item>` template, a user of the class will be able to write:

```cpp
Vec<int> v1;
Vec<double> v2;
Vec<string> v3;
```

Given these declarations, the C++ compiler will use the `Vec<Item>` template to build three classes:

1. A class that is a vector for storing integer values.
2. Another class that is a vector for storing double values.
3. Another class that is a vector for storing string values.

The compiler will use these behind-the-scenes classes as the types of `v1`, `v2`, and `v3`. For every declaration in which we pass a new type into the template, the compiler will build a new class, and then use that class as the declaration's type.

With that as our introduction, let's get on with turning our Vec class into a `Vec<Item>` class template.

### Step 1. Converting the Class Declaration

The first step in converting a class into a class template is to **delete the typedef declaration** we used previously -- so remove the line defining `Item` as a double. In its place, we place the phrase `template<class Item>` immediately before the class declaration:

```cpp
template <class Item>
class Vec {
       ...
};
```

Do this now.

This revised declaration tells the C++ compiler that

1. What's coming is a class template, not a class.
2. This template has a single parameter, whose name is `Item`.
3. The word class before `Item` indicates that `Item` represents a type, not a variable or object.

It is worth mentioning that the name `Item` is an identifier we have chosen, since it is what we used for our typedef. The words template and class are C++ keywords, they cannot be changed.

Once this declaration has been processed, the name of the template is `Vec<Item>`.

### Step 2. Eliminating the Implementation File

Because the C++ compiler uses a template as a blueprint from which it builds a class, the compiler needs to be able to see the entire class — class declaration plus method definitions — when a program using the template is compiled. This means that the entire class template — template declaration plus method definitions — must appear in the header file, in order for a program that `#include`s the header file to compile, or linking errors will occur. So our next step is to select the method definitions in the implementation file, cut them, and paste them into the header file, between the template declaration and the `#endif`.

In **Vec.cpp**, select all of the method definitions, cut them (Ctrl-X or Cmd-X) from the .cpp file. Switch to the **Vec.h**, move the cursor to a point between the end of the template declaration and the `#endif`, and paste them in (using Ctrl-v).

If there are `#include` directives in the **Vec.cpp** file that are **not** in **Vec.h** (except for **Vec.h** itself), they will also need to be cut-and-pasted into **Vec.h**. (It is often necessary to cut-and-paste `#include <iostream>`.)

Now that the method definitions have been moved from **Vec.cpp** to **Vec.h**, you should delete **Vec.cpp** from your project.

```{note}
Note that you will need to update your **Makefile**! Find the **Vec.cpp** reference in the SOURCES line and <span style="color: red;">remove</span> it.
```

### Step 3. Converting the Class-Methods to method-templates

We now have a class template, but our methods are still class methods. Our next step is to convert each class method into a template method. Test-driven development gives us a systematic, method-by-method means of doing this conversion, without getting overwhelmed by a zillion compiler errors.

You should see the message indicating there are no tests if you **comment out all of the Vec prototypes**, and **all of the method definitions you just pasted into the header file**. If you want to, and compile (`make tester`) and run your project(`./tester`). Just remember that your code was drastically changed, and might not function anymore if you don't comment certain parts. **You should see the message indicating there are no tests.**

Our test-driven procedure will be to: (don't do this yet — just read the steps below)

1. In **tests.cpp**, uncomment the `TEST_CASE`. Convert all uses of Vec to be `Vec<sometype>`. You may choose what type to put in between the `<` and `>`, but the type should be an integer type -- int, unsigned, short, char, unsigned char, long, etc.
2. In **Vec.h**, uncomment the corresponding method (i.e., its prototype within the class and its definition outside the class.)
3. Convert the method's definition into a method-template.
4. Compile and run the tester.
5. If any errors are reported, find and fix them;

   Otherwise, return to step 1.

Converting a method definition (step 3) to a method-template is fairly simple:

1. Place `template <class Item>` before the beginning of the method's definition.
2. In the method definition, find each place where the name of the class (e.g., Vec) **is being used as a type** — each use except when it is being used as the name of an operation like the name of a constructor or destructor — and replace it with the parameterized name of the template (e.g., `Vec<Item>`).

So the rest of Part I is to use these steps to convert each of the Vec methods to method-templates.

To illustrate this conversion process, let's run through these steps using some of the Vec constructors.

#### Step 3a. The Default Constructor

In **tests.cpp**, uncomment the test that tests the default constructor and convert it to use `Vec<sometype>`. (Make sure to uncomment the matching curly brackets (}) at the end of the test case section.) Then switch to **Vec.h** and find the definition of the default constructor. We can perform step 1 by placing `template<class Item>` before the constructor definition:

```cpp
template<class Item>
Vec::Vec() {
  ...
}
```

That completes step 1.

For step 2, we replace each use of the name of the class (Vec) that is not the name of an operation with the name of the template (`Vec<Item>`), as follows:

```cpp
template<class Item>
Vec<Item>::Vec() {
  ...
}
```

That's it! Save all changes, and compile and run your tests. If you find errors, find and fix them before continuing.

```{hint}
You may need to make some additional changes before things build. More than likely, compilation of the tester will not succeed until you have converted several other methods that are used in the default constructor tests, including the destructor.
```

Congratulations! You have just converted your first class-method into a method-template!

#### Step 3b. The Explicit-Value Constructor

Using what we just did to the default constructor as a model, uncomment the explicit constructor's test, fix the types, then convert the explicit constructor into a method-template. Compile and run your project. If errors occur, fix them. When it passes all tests continue.

Note that within this constructor, the allocation of the dynamic array uses `Item`. Previously, this `Item` was determined by the `typedef` declaration; but now, `Item` refers to the name of our template's parameter. If the user declares:

```cpp
Vec<double> v1;
Vec<int> v2;
```

then in `v1`, all of the occurrences of `Item` will be replaced by double, while in `v2`, all the occurrences of `Item` will be replaced by **int**.

Congratulations! You've just done another method-to-method-template conversion!

#### Step 3c. The Copy Constructor

Uncomment and fix the copy constructor's test. In **Vec.h**, find the copy constructor's definition. As before, we place `template<class Item>` before the definition, and replace each occurrence of the name of the class that is not the name of an operation with the name of the template:

```cpp
template<class Item>
Vec<Item>::Vec(const Vec<Item>& original) {
  ...
}
```

Note that the type of any Vec parameter or local variable must be replaced by `Vec<Item>`. This is consistent with our "conversion rule" — any use of the name of the class that is not the name of an operation (i.e., a constructor or destructor) must be replaced.

Compile and run your project. Continue when it passes all tests.

#### Step 3d. The Destructor

If you have not already done so, convert the destructor to a method-template. Continue when your conversion passes all tests.

#### Step 3e. The Remaining Operations

Now that you know how to do the conversion, we can speed up this mechanical process a bit.

At the destructor definition, comment out the line `template<class Item>`. Then copy the line `//template<class Item>`. With the remaining operations still commented out, use Ctrl-v to paste that line at the beginning of each of the remaining operations in the header file.

Return to the destructor's definition and uncomment the line `template<class Item>` in the destructor. Then copy the "phrase" `<Item>`. With the remaining operations still commented out, paste this after each use of the name of the class that is not the name of an operation, throughout the rest of the header file.

Then, one untested method at a time:

1. Uncomment the converted method.
2. Uncomment its corresponding test.
3. Uncomment the call to that test.
4. Compile and run the test. When it passes the test, continue to the next untested method.

By using this _methodical_ approach (Ha, ha! Get it?!?), any compilation errors that occur should be confined to the newly uncommented method-template. This will make it easier and faster for you to find and fix the errors.

Use this approach to complete the conversion of class `Vec` to the `template Vec<Item>`.

Congratulations! You have just built your first class template!

### Discussion - Part I

As you can see, the C++ syntax to build class templates is a bit complicated, and it is quite easy to make syntax errors if you try to build a template container from the outset. For this reason, we recommend this 2-step approach to building containers:

1. Use the typedef-Item mechanism to build a container class and thoroughly test its operations.
2. Convert the Item container class into a template that receives its type via a parameter.

By doing so, you can build and test the container in step 1, and debug the logic of its operations. Then (as we have seen today), converting it to a template in step 2 is a mechanical process.

Because **any** type can be passed via the template's parameter, a container built as a template can store any kind of value. Because they are defined to store "generic" items, container templates are often called generic containers. The template is the C++ mechanism for building generic containers; other languages (e.g., Ada, Java) provide other (simpler) mechanisms.

## Part II. Add support for Python-like indexing to PyList

Before proceeding, comment out all code in the **tests.cpp** file that runs the tests for Part I — including the `#include “Vec.h”` statement.

```{note}
**Make sure that *catch.hpp* stays included!** And uncomment PyList testing code (i.e., toggle the comments that are there).
```

The makefile is currently not compiling **PyList.cpp**, so you need to change it. Change the SOURCES line, adding **PyList.cpp**.

```{important}
If **Vec.cpp** is still there, it should be removed at this time.
```

Look at the **PyList.cpp** and **PyList.h** files.

Build and run. The execution should succeed, testing the existing PyList functionality.

In Python, you can index a list using negative numbers. The last item in the list is at index -1, the second-to-last at -2, etc. The first item in the list, e.g., `lst[0]`, is the same as `lst[-10]`, if there are 10 items in the list. Here are some examples of how python behaves:

```python
>>> lst = list(range(10))
>>> lst
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]  # in this example, the values are the same as the indices
>>> lst[-1]                # last item
9
>>> lst[-8]                # penultimate item
2
>>> lst[-10]               # same as lst[0]
0
>>> lst[-11]               # cannot index off the "front" of the array
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: list index out of range
>>> lst[10]                # cannot index off the end of the array
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: list index out of range
```

In the **tests.cpp** file, there are already tests for this feature, but they are still commented out. Uncomment them, and run the test. You'll see failures. In fact, you might see a **Segmentation Fault**.

Now, implement the feature. You'll have to alter `getValue()`, `setValue()`, and `operator[]`, so that the Python-like index is converted to a legal C++ index before accessing `myArray`. Because the code to check for a legal index is the same in those three methods, I put the common code into a new private method called `validate_index(index)`, described in the table below. Then, my whole implementation of `getValue()` becomes very short: `return myArray[validate_index(index)];`

Here is a summary of `validate_index()`:

| **Method**       | **Parameters** | **Notes**                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ---------------- | -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| validate_index() | int index      | The purpose of this function is to convert what would be a legal python index into a legal C++ index.<br><br>Make note, does this method change anything in our class? If it doesn’t, should we make this a const function?<br><br>**Algorithm:** <br><br>- If the index is \>= n, throw a range_error exception. <br>- If the index is \< -n, throw a range_error exception. <br><br>Convert the index to be between 0 and n-1 if necessary. Return the index back. |

Finally, implement a `find()` method as described below:

| **Method** | **Parameters**          | **Notes**                                                                  |
| ---------- | ----------------------- | -------------------------------------------------------------------------- |
| find()     | an `Item` to search for | If the item is found in the array, return the index. Otherwise, return -1. |

First, add a `SECTION("find")` to the "PyLists" TEST_CASE in **tests.cpp** to test the find command. You'll want to make sure you try to find items that are in a PyList and items that are not in the list. You should also make sure that if an `Item` is in a list more than one time, the index of the first item is returned.

After you are satisfied with your tests, and you prove that your tests fail, then implement the `find()` method.

After you do this and have all your tests passing, then **Uncomment all the Vec tests** in **tests.cpp**, so that ALL tests are now available, both for Vec and for PyList. Then, of course, recompile and run `./tester` to make sure it tests both Vec and PyList.

## Submit

Don't forget to commit AND sync your code to your repo for grading.

```{important}
Verify you have synced your code to github by going to your online repo webpage and looking to see that the files are correct.
```

```{warning}
Verify that the automated tests have passed in github.com.
```

## Grading Rubric: 24 pts total

This lab will be graded the following way: 24 pts total

- Part I: 10 pts
  - All code has been converted to a class template correctly: 5 pts
  - All tests pass: 5 pts.
- Part II: 10 pts.
  - Negative indexing works correctly, as indicated by thorough tests: 5pt
  - `find()` works correctly: 5 pts.
- Code is clean, perfectly indented, hospitable: 2pts
- Code builds correctly: 2 pts

Ways students lost points in the past:

- -2: Can't make tester. Error occurs.
- -2: Late submission
- -4: Grader had to edit the makefile to build.
- -2: Tests fail
