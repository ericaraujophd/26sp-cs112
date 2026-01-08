---
title: Lab 04
subtitle: Vec — A First Dynamic Data Structure
---

## Objectives

In this exercise, you will:

1. Build a class that uses dynamic allocation/deallocation.
2. Use pointer variables to access items in a dynamically-allocated array.

## Introduction

You should know how to [get the assignment](https://classroom.github.com/a/jeT134Lz). So, do it.

```{important}
Don't forget to make sure you and your partner are in the same Team! Also edit the README.md file and put both of your names and emails in the file.
```

The Vec class is a simpler version of the `vector<T>` class template available in the C++ standard template library (STL). It will provide the basic functionality, without some of the more advanced "bells and whistles" of the STL version.

The class in **Vec.h** is a mere shell at this point. Filling in this shell is our task this week.

## Step 1. Getting Started

Open each file and take a moment to browse through them, to get a sense of what each one contains. Note that **tests.cpp** contains tests for a variety of Vec operations.

Our approach today will be to use the following steps to build each operation:

- This exercise will provide you with a description of what the operation should do, and a stub for the method that provides that operation;
- You will uncomment the call to the test for that operation in **tests.cpp**
- You will complete the method by adding statements to the stub; and
- You will compile and run the project. (do `make tester && ./tester`)

```{important}
Compile, debug and fix any errors.

If all is well, you can then proceed to the next operation; otherwise you will need to debug your operation to figure out why it is failing the test, recompile, and rerun the test, until it is passed.
```

## Step 2. Instance Variables

If you look in **Vec.h**, you'll see that we are (for now) using a `typedef` to define the identifier `Item` as a synonym for the type `double`.

You'll also see that the `private:` section of class Vec is currently empty. As a minimalist dynamic array, our Vec will need to "remember" two things:

1. How many Items it is currently storing; and,
2. The `Item`s it is currently storing.

To let a Vec "remember" the first of these, add an instance variable named `mySize` of type `unsigned`:

```cpp
private:
    unsigned mySize;
```

To let a Vec "remember" the second of these, add an instance variable named `myArray` capable of storing the address of an `Item`:

```cpp
private:
    unsigned mySize;
    Item   *myArray;
```

With these two variables, a Vec object can "remember" (i) how many items it is storing, and (ii) the address of a dynamically allocated array in which its items are stored.

## Step 3. The Default Constructor

The role of the default constructor is to provide the instance variables with default values. In a data structure, these are usually values that are appropriate for an "empty" structure. In **Vec.cpp**, complete the default constructor for the class, so that it sets `mySize` to zero, and sets `myArray` to `nullptr`. Compile and run the project (`make tester && ./tester`).

The test should pass, but notice that it isn't actually doing anything... To make a useful test, we need to see if `mySize` is 0 and `myArray` is `nullptr`. However, `myArray` and `mySize` are private, so the test cannot "reach into" the innards of the Vec object to check the values. To resolve this, we will create a getter for `mySize`. In the **.h** file, in the `public:` section, add the prototypes:

```cpp
unsigned getSize() const;
```

In the **Vec.cpp** file, add this code:

```cpp
unsigned Vec::getSize() const {
}
```

and finish the code which returns `mySize`.

```{note}
Notice that we are **NOT** going to add a getter method for `myArray`, which would allow a user of the Vec class to get the address where the values are being stored. We do not want to expose this internal detail to the user, as the user could abuse it and start putting values directly into memory. So, because we won't make a getter for `myArray`, we won't be able to make tests to check the value of `myArray`. (Unless we create a method that returns `true` if `myArray` is not `nullptr`, and false otherwise)
```

Uncomment the lines in the first ("default") `SECTION` and compile and run (`make tester && ./tester`). You should get 1 assertion in 9 test cases passed.

```{important} Before you go the next step!
When your definition passes the test, continue; otherwise fix and retest your constructor.
```

## Step 4. The Explicit-Value Constructor

The explicit-value constructor's role is to initialize an object using values provided by the user. In a data structure, the user often wants to specify a non-zero starting size for the structure. (e.g., `Vec v(5);` should construct `v` as a vector capable of storing 5 items.) To store the value the user specifies, our constructor will need a parameter, so we might start by writing this stub for the constructor:

```cpp
Vec::Vec(unsigned size) {
}
```

Put the above code in your **.cpp** file, and add a prototype for this constructor to the Vec class in **Vec.h**. Then in **tests.cpp**, uncomment **ONLY THE FIRST 2 LINES OF CODE** in the "explicit-value" `SECTION` that tests this constructor (if you hadn't changed the **tests.cpp** file, those should be lines 14-15). Save/compile/run the tests. The test should fail. To make it pass, add code to your explicit-value constructor. Here is the algorithm to follow:

1. Set `mySize` to `size`
2. If `size` is positive (greater than zero):
   - Dynamically allocate an array of size values of type `Item`, and store the address of the array in `myArray`; and
   - Set each of the `Items` in that array to zero.
3. Otherwise:
   - Set `myArray` to `nullptr`.

Continue when your class passes all tests (2 assertions in 9 test cases).

## Step 5. Getting the Value of an Item

The rest of the test for the "explicit-value constructor" looks to see if `myArray` was initialized correctly. In order to do this, we need to be able to retrieve the value in each location in `myArray`. To do that, we'll implement a `getItem()` method that lets us retrieve the value of an item at a given index (e.g., `Item it = v.getItem(i);`). Since this method (i) needs the index of the value it is to retrieve, and (ii) does not change its receiver's instance variables, we will start by defining this stub:

```cpp
Item Vec::getItem(unsigned index) const {
}
```

Place a prototype for this method in the Vec class, and in **tests.cpp**, uncomment the rest of the test code in the "explicit-value" constructor `SECTION`. For the sake of time, here is the code for **.cpp** file:

```cpp
Item Vec::getItem(unsigned index) const {
    if (index < 0 || index >= mySize) {
        throw range_error("Bad index");
    }
    return myArray[index];
}
```

When all tests pass, continue (15 assertions in 9 test cases).

```{note}
There is a `TEST_CASE` in **tests.cpp** to fully test `getItem()`, but it relies on `setItem()`, which we have not implemented yet. So, don't uncomment that test case yet.
```

## Step 6. Setting the Value of an Item

Our next operation is to set the value of a particular item in a Vec (e.g., `v.setItem(i, val);`). Since the method needs both the index of the item to change, and the new value for the item, we will start with this stub:

```cpp
void Vec::setItem(unsigned index, const Item& it) {
}
```

Place a prototype for this method in the `Vec` class, and in **tests.cpp**, uncomment the code to test `TEST_CASE("setItem")` (22 assertions in 9 test cases).

Try to build and run the test to see what errors you get; then complete the stub so that it passes the test. Again, for the sake of time, here is the code for **Vec.cpp**.

```cpp
void Vec::setItem(unsigned index, const Item& it) {
    if (index < 0 || index >= mySize) {
      throw range_error("Bad index");
    }
    myArray[index] = it;
}
```

When all tests pass for testing `setItem`, also uncomment the `TEST_CASE("getItem")`. If you have everything working, you should be passing 29 assertions in 9 test cases.

## Step 7. The Copy Constructor

The compiler invokes a special copy constructor any time it needs a copy of an object, for example:

- When a function returns an object; OR
- When an object is passed as an argument to a call-by-value parameter.

The C++ compiler supplies a default copy constructor, but it merely does a bit-by-bit copy of the instance variables of the object being copied. This bit-copy is inadequate for classes with pointer instance variables, because it just copies the address within such variables, rather than making a distinct copy of the dynamically allocated memory to which that address points. Because of this, **every class that contains a pointer instance variable should define its own copy constructor that makes a distinct copy of the object, including its dynamically allocated memory**.

The stub for a Vec copy constructor looks like this:

```cpp
Vec::Vec(const Vec& original) {
}
```

```{important}
If we were to mistakenly make the copy constructor's parameter a **call-by-value** parameter instead of a **call-by-const-reference** parameter, an infinite recursion will occur when the copy constructor is invoked. The reason is that passing a Vec to a call-by-value parameter will invoke the copy constructor, which will take the thing to be copied as a parameter, which will invoke the copy constructor, which will take the thing to be copied as a parameter, which will invoke the copy constructor, which... To avoid this, the parameter of a copy constructor should always be a const-reference parameter, as shown above.
```

Add the code above to the .cpp file. Then, add a prototype to the Vec class, and in **tests.cpp** uncomment the code in the "copy" constructor SECTION (`SECTION("copy")`) to test it. Then add statements to your stub to construct a Vec that is a distinct copy of original, and check to see if the tests pass. Here is the algorithm to follow:

1. Set `mySize` to the `size` of original
2. If `original.mySize` is greater than zero:
   1. Dynamically allocate an array of `mySize` values of type `Item`, and store the address of the array in `myArray`.
   2. Set each item `i` in the new array to item `i` from original.
3. Otherwise, set `myArray` to `nullptr`.

Continue when your constructor passes all tests. (I am now seeing 42 assertions in 9 test cases passing.)

## Step 8. The Destructor

The C++ compiler invokes an object's **destructor** when the object ceases to exist. The role of the destructor is thus to perform any "clean up" actions that are needed to return the system to the same state it was in before the object existed. In a data structure that uses dynamic memory allocation, the main task is usually to return dynamically allocated memory to the system using the **delete** operation.

A destructor cannot have any parameters, and its name is the name of the class preceded by the tilde character (\~), so we can begin with the stub:

```cpp
Vec::~Vec() {
}
```

Skeleton code is already in the .h and .cpp files. Uncomment the code to test the destructor in **tests.cpp**. Then add the statements to the destructor to reclaim the dynamic array whose address is in `myArray`, set `myArray` to **nullptr**, and set `mySize` to zero. Compile and see if your statements pass the test. Here is the algorithm to follow:

1. Use `delete []` to deallocate the array whose address is stored in `myArray` aka `delete [] myArray;`
2. Set `myArray` to `nullptr`
3. Set `mySize` to zero.

Technically, only the first step is strictly necessary. The reason is that the destructor is only invoked at the end of an object's lifetime. Since the object will no longer exist, resetting its instance variables is not necessary (except to pass the test).

Continue when your destructor passes all tests, including the section `TEST_CASE("destructor")`. By now, you should have 43 assertions in 9 test cases.

## Step 9. Setting a Vec's Size

Our next operation is to set a Vec's size via a method (e.g., `v.setSize(8);`). The role of this method is to allow us to change the size of an existing Vec to some new size. Since the user must specify this new size, we need a parameter to store it. We might start by defining this stub:

```cpp
void Vec::setSize(unsigned newSize) {
}
```

Place a prototype for this method in the Vec class, and in **tests.cpp**, uncomment all the code in the `TEST_CASE("setSize")`. Then complete the stub so that it passes the test. Think carefully! This one is deceptively tricky to get right! Algorithm:

<ol>
    <li>If <code>mySize</code> and <code>newSize</code> are different:
        <ol type="a">
            <li>If <code>newSize</code> is zero:
                <ol type="i">
                    <li>Deallocate <code>myArray</code></li>
                    <li>Set <code>myArray</code> to <code>nullptr</code></li>
                    <li>Set <code>mySize</code> to zero.</li>
                </ol>
            </li>
            <li>Otherwise:
                <ol type="i">
                    <li>Declare a local variable <code>newArray</code> of type <code>Item *</code></li>
                    <li>Allocate a new dynamic array of <code>newSize</code> Items, storing its address in <code>newArray</code>.</li>
                    <li>If <code>mySize</code> is less than <code>newSize</code>:
                        <ol type="a">
                            <li>Copy <code>mySize</code> values from <code>myArray</code> into <code>newArray</code>.</li>
                            <li>Set the remaining (<code>newSize - mySize</code>) values to zero.</li>
                        </ol>
                    </li>
                    <li>Otherwise, just copy <code>newSize</code> values from <code>myArray</code> into <code>newArray</code>.</li>
                    <li>Set <code>mySize</code> to <code>newSize</code>.</li>
                    <li>Deallocate <code>myArray</code>.</li>
                    <li>Set <code>myArray</code> to <code>newArray</code>.</li>
                </ol>
            </li>
        </ol>
    </li>
</ol>

<!-- ```
1. If `mySize` and `newSize` are different:
    a. If `newSize` is zero:
        1. Deallocate `myArray`
        2. Set `myArray` to `nullptr`
        3. Set `mySize` to zero.
    b. Otherwise:
        4. Declare a local variable `newArray` of type `Item *`
        5. Allocate a new dynamic array of `newSize` Items, storing its address in `newArray`.
        6. If `mySize` is less than `newSize`:
            1. Copy `mySize` values from `myArray` into `newArray`.
            2. Set the remaining (`newSize - mySize`) values to zero.
        7. Otherwise, just copy `newSize` values from `myArray` into `newArray`.
        8. Set `mySize` to `newSize`.
        9. Deallocate `myArray`.
        10. Set `myArray` to `newArray`.
``` -->

When your method passes all tests (67 assertions in 9 test cases), continue.

## Step 10. Equality

The purpose of the **equality operation** is to let us compare two objects (e.g., `if (v1 == v2) { ... }`), returning **true** if they are equal, and returning **false** if they are not. Since the equality operation returns a bool value, a call:

```cpp
v1 == v2
```

will be treated by the compiler as:

```cpp
v1.operator==(v2)
```

This equality operator should not change either of its operands. We start by defining this stub:

```cpp
bool Vec::operator==(const Vec& v2) const {
}
```

Place a prototype for this method in the Vec class, and in **tests.cpp**, uncomment the code to test "equality" (`TEST_CASE("equality")`). Then add statements to the stub so that it passes the test. Algorithm:

1. Check to see if `mySize` is NOT the same as the size of v2. If the two vectors are not the same size, return false.
2. Compare each item `i` in `myArray` to each item `i` from v2's array: If any are not equal, return **false**.
3. The two arrays are equal in size, and all their values are the same, so return **true**.

Continue when your method passes all tests. By now you should have 74 assertions in 9 test cases.

## Step 11. ostream Output

It is useful to be able to write a vector to an `ostream`, as this allows us to display it on the screen (or write it to a file via an `ofstream`). This method should output the values of the items in the Vec, but not its size; if the user wants that size information displayed, they can do that separately using `getSize()`.

Whereas (i) our method returns nothing to its caller, (ii) it needs to "know" the ostream to which it is to write, (iii) it modifies that ostream by inserting items, and (iv) it should not modify any Vec instance variables, we might begin with this stub:

```cpp
void Vec::writeTo(ostream& out) const {
}
```

Place a prototype for this method in the Vec class, and in **tests.cpp**, uncomment the test "writeToStream" (`TEST_CASE("writeToStream")`). Then add statements to this stub so that it passes the test. Algorithm:

- Send each value in `myArray` to the `out` stream, followed by a single space.
- Use `to_string()` to convert the values to string, otherwise your tests might fail.

Continue when your method passes all the tests (75 assertions in 9 test cases).

## Step 12. istream Input

It is also useful to be able to read a vector from an **istream**, as this lets us enter a vector's values interactively, from a keyboard (or read them from a file via an `ifstream`). This method complements `writeTo()`, and should assume that the user has already constructed the Vec with the appropriate size.

Since (i) our method returns nothing to its caller, (ii) it needs to "know" the istream from which it is to read, (iii) it modifies that istream by extracting items, and (iv) it might modify its instance variables, we might begin with this stub:

```cpp
void Vec::readFrom(istream& in) {
}
```

Place a prototype for this method in the Vec class, and in **tests.cpp**, uncomment the test `TEST_CASE("readFromStream")`. Then add statements to this stub so that it passes the test.

Assuming that `mySize` equals the number of values in in, the Vec `readFrom(istream& in)` method should:

- Extract each value from `in`, storing each in "the next" item of `myArray`.

Continue when your method passes all the tests. (My solution passes with 82 assertions in 9 test cases. If you have less, uncomment `TEST_CASE("getSize")`).

```{tip} Congratulations!
You have just built a class that offers the basic functionality one would expect from a vector!
```

## Submit

Use VSCode (or the command line) to commit and push your changes to your repo.

To verify your submission to github.com, go to a browser and go to the location of your repo in github.com.

Also, verify that your submission passes all the automated tests in github. The automated tests are the same as those in tests.cpp.

## Grading Rubric

24 pts total

- 25 pts for correct code that passes all the tests
- 2 pts for clean, neat code, well-indented, and readable
- 6 pts for correctness (see common mistakes below).

Ways students lost points in the past:

- -1: Be careful about brace indentation <!-- + -1: Assignment operator leaks memory if the old `mySize > 0` and `original.mySize == 0` (remove Vec.cpp line <redacted>, check instructions carefully) --> <!-- + -1: Tester crashes at line <redacted>, should be < newSize in case newSize is smaller than mySize (otherwise you index past the end of the array) -->
- -1: Memory leak in `setSize()` when mySize \< newSize. You need to delete\[\] myArray in both cases; move it outside the else statement.
- -2: Make sure you are using `delete[]` and not `delete`, which leaks memory
- -33: No submission, or partner forgot to include you in README.
