---
title: Project 04
subtitle: More Vec Operations
---

## Objectives

1. Build more vector operations.
2. Practice using the debugger (if necessary).

## Step 0. Prepare

```{important} **READ THIS:** IT IS DIFFERENT THAN NORMAL!

```

1. [Click the link](FIX THIS!!!) and then "Accept this assignment".
   - Wait a few seconds and refresh the page. Refresh until the page says "You're ready to go!". The page has a link to a github repo.
   - Click the link to see your new repo on github.com.
   - Click the green <span style="color: green;">Code</span> button and copy the link it shows.
2. In a terminal,
   - `cd` to the directory where you are putting all your CS112 assignments.
   - type `git clone paste-the-contents-of-the-link-you-copied`
   - `cd` to the new directory containing your repo.

```{important}
BECAUSE your project depends on your lab code, you need to copy your lab code over to this repo. That is, you have to copy **Vec.h** and **Vec.cpp** you've implemented during Lab 04 to this repo after cloning it.

In a terminal:

- `cd` to your **lab04** directory (use `pwd` to make sure you are in the right directory)
- `cp Vec.h Vec.cpp your-project-4-directory` (the full path to your project 4 directory)
- `cd` to your project 4 directory (`your-project-4-directory`)
```

In the video below I've copied the files from my **lab04** folder to the **proj04** folder as requested. Can you follow up with the steps?

```{figure} cpVec.gif
---
name: cpVec
---
Copying Vec.h and Vec.cpp from lab04 to proj04.
```

```{warning}
If, at this moment in the course, you are still not able to handle directories and files using the terminal, spend some time searching more about it and learning. This is an essential skill for anyone who handles computational systems nowadays. [This might be a good place to start](https://www.youtube.com/watch?v=42iQKuQodW4).
```

- Open your project in VS Code, and open **Vec.h**
- Add this prototype for the assignment operator to **Vec.h**, in the public area:

```cpp
Vec& operator=(const Vec& original);
```

- Add this code to **Vec.cpp**:

```cpp
Vec& Vec::operator=(const Vec& original) {
    if (this != &original) {
        if (mySize != original.mySize) {
            if (mySize > 0) {
                delete[] myArray;
                myArray = nullptr;
            }
            if (original.mySize > 0) {
                myArray = new Item[original.mySize];
            }
            mySize = original.mySize;
        }
        for (int i = 0; i < mySize; ++i) {
            myArray[i] = original.myArray[i];
        }
    }
    return *this;
}
```

- In the terminal, type `make tester`
- The code should compile and give you an executable called "tester"
- Run the tester file: `./tester`
- Your tests should all pass.

## Step 1. Introduction

This week's project adds more functionality to the Vec class we built in the lab. To illustrate, suppose that `v1`, `v2`, and `v3` are Vec objects containing the following values:

```cpp
v1 == {1, 2, 3}
v2 == {2, 4, 6}
v3 == {1, 2, 3}
```

### 1.0 Subscript

The subscript operator (`[i]`) can be implemented such that using subscripting on the left-hand-side of an assignment (i.e., setting a value in the array) and using subscripting on the right-hand-side (i.e., getting a value in the array) both work. Thus, the method will be similar to both `setItem(i)` and `getItem(i)`.

- Normally, the subscript operation on an array **does not** perform bounds checking on the index value i, but yours should perform bounds checking. More precisely, your subscript operator should throw a `range_error` if it is passed a "bad" index value.
- The method should return a **reference** to the item in the array.

Here is the algorithm:

```cpp
Item &operator[](unsigned index)
    check if index is legal. If not, throw a range_error
    return myArray[index];
```

Because the method is returning a reference to the item in the array, subscripting works for both sides of an assignment.

### 1.1 Const subscript

If a Vec object is defined as constant then indexing the array in the Vec must also be constant — i.e., it cannot allow code to change the array. In **tests.cpp**, see a function called `testConstSubscript()`. This function takes a const-ref parameter. The subscripting of that Vec parameter will require us to implement the const subscripting method. The code in the method is identical to the code you wrote in the previous step above, but it returns `const Item &`, and is a const method — i.e., has `const` on the end of the line. Implement that method now so that all subscripting tests pass.

```{note}
The function `testConstSubscript()` can be found on line 315 in **tests.cpp**. Make sure you uncomment the function and the following `TEST_CASE("subscript")` and run `make tester && ./tester` before proceeding. You should have 131 assertions in 11 test cases passed at this point.
```

### 1.2 Vector Addition

The expression:

```cpp
v3 = v1 + v2;
```

should set `v3 == {3, 6, 9}`, without leaking memory.

When C++ compiles `v1 + v2`, it looks at the types of the values that surround the `+`. It sees that `v1` is a Vec object, so it actually will call `operator+()` on the `v1` object, passing `v2` as the parameter. Thus, the prototype is

```cpp
Vec Vec::operator+(const Vec &rhs) const
```

`v1` is the "this" object that `operator+` is being called on. `v2` is being passed in as the **rhs** (right-hand-side) parameter.

Implement it. The implementation is quite simple: make sure the sizes of the two Vecs are the same. If not, throw an error of type `invalid_argument`. If they are the same, create a new Vec object (of the correct size) and loop, repeated adding the values from `myArray[i]` and `rhs[i]` together and putting the result into the new Vec object.

```{note}
Uncomment the `TEST_CASE("addition")` in line 344 to test if your code works. Do not move foward if you get errors. You should have 139 assertions in 12 test cases passed at this moment.
```

### 1.3 Vector Subtraction

The expression:

```cpp
v3 = v1 - v2;
```

should set `v3 == {-1, -2, -3}`, without leaking memory.

```{note}
To make life easier for you, **tests.cpp** contains tests for each this operation also (`TEST_CASE("subtraction")`). Use these tests and test-driven development to build your operations. If you get your program to compile, but it fails a test and you cannot figure out what is wrong, **use the debugger**! If necessary, draw a memory diagram and trace through the execution of the problematic function one statement at a time, until you identify the logic error. At this point, you should have (all going well) 147 assertions in 13 test cases passed.
```

## Step 2. Application

Congratulations! 🎉🎉🎉🎉 You have been named the navigation officer on the starship **U.S.S. Boobyprize**, whose hyper-spatial engines allow the ship and its crew to explore the universe. Current theories suggest that reality consists of 11 or more dimensions, so you need a program to help you navigate through an N-dimensional space.

Vectors can be used to store positions (and/or directional forces) in a coordinate system. Vectors of length 2 can be used to store 2-dimensional (x, y) information; vectors of length 3 can be used to store 3-dimensional (x, y, z) information; and so on. Your task is to write a program that:

1. Prompts for and has the user enter the number of dimensions in their space, storing this number in a variable N, which it can then use to define vector objects.
2. Prompts for and has the user enter a starting position in that space, and stores that position in a vector object sum.
3. Uses a loop that:
   1. prompts for and has the user enter a position (relative to their current position), and stores that position in a vector,
   2. adds that vector to the sum vector.
4. This loop should let the user enter an arbitrary number of positions.
5. Outputs the starting position plus the final position (i.e., the sum of the positions from the accumulator-vector).

For example, if the user is in a 3-dimensional system, enters the starting point {0, 0, 0}, and then enters the following four 3-dimensional relative-positions:

```bash
{1, 0, 0}
{0, 1, 0}
{0, 0, 1}
{1, 2, 3}
```

the program should then display the starting position (`{0,0,0}`) and the sum from the accumulator (`{2, 3, 4}`), which is the user's final position within the 3-dimensional system.

As another example, if the user is navigating through a 5-dimensional space, enters `{1, 0, 1, 0, 1}` as the starting point, and enters three 5-dimensional relative-positions:

```bash
{0, 1, 0, 1, 0}
{2, 2, 2, 2, 2}
{-3, -3, -3, -3, -3}
```

the program should then display the starting position and the final position (`{0, 0, 0, 0, 0}`).

```{note}
You may (if you wish) have your program display the starship's new position each time it is updated, rather than just displaying the final position at the end.
```

Your application should have the user enter the vectors in the format expected by your `readFrom(istream&)` method: numbers separated by whitespace. (It does not have to parse through curly-brace and comma characters.) Likewise, your application can display the starship's position using the format provided by your `writeTo(ostream&)` method—numbers separated by spaces.

To get you well on your way, your repo contains **App.cpp** and **App.h**. These files provide most of what you have to implement to finish this project. Just implement the missing TODO parts.

Now that you have addition implemented, you'll need to uncomment the line in **App.cpp** that reads

```cpp
res = res + v;
```

You will have to edit `main()` in **main.cpp** to:

1. call the `App()` constructor, and then
2. on the resulting object, call `run()`.

Compile the program with `make proj4` and execute the program by doing `./proj4`.

## Submit

Submit your changes using git, either from the command line or using VSCode. Push your changes up to github.

Verify you have synced your code to github by going to your online repo webpage and looking to see that the files are correct.

```{tip}
Verify that the autograding tests have successfully passed in github.
```

## Grading Rubric

30 pts Total:

- Passes all tests: 8 pts.
- `operator[]`: 3 pts
- `operator+`: 3 pts
- `operator-`: 3 pts
- USS Boobyprize application: 10 pts
- Code is clean and neat. Comments where appropriate, good spacing, etc: 3 pts.

Ways students lost points in the past:

- -1: Const-qualified subscript operator \[\] should return `const Item&`, not `Item&`;
- -3: Your `readFrom()` implementation never stops reading from input, so the app doesn't work
- -2: Missing call into `App::run()` from `main()`. <!-- + -15 (50%) for 5 days late. -->
- -2: Dynamically allocate the new vectors in addition and subtraction causes memory to leak
- -2: Did not uncomment the line that adds each vector to the result in `App.cpp`, so it doesn't work
- -2: Needs two versions of the subscript operator for const and non-const
- -2: `setSize()` was not fixed from the lab, tests do not pass
