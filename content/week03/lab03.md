---
title: Lab 03
subtitle: Classes
---

## Part 0. Prepare

1. Click this [link](https://classroom.github.com/a/8Ag1LlMI) and then "Accept this assignment". Make sure you and your partner are in the **same Team**. Pick a name for your team different from previous labs. I recommend you keep the name and add a -lab03 to it.
   - Wait a few seconds and refresh the page. Refresh until the page says "You're ready to go!". The page has a link to a github repo.
   - Click the link to see your new repo on github.com.
   - Click the green <span style="color: green;">Code</span> button and copy the SSH link it shows.
2. In a terminal,
   - `cd` to the directory where you are putting all your CS112 assignments.
   - type `git clone paste-the-contents-of-the-link-you-copied`
   - `cd` to the new directory containing your repo.
   - type `code .` to start up Visual Studio Code in that directory.
3. Inspect the code you got in the assignment.

## Part 1: A Student Class

### Step 1. Create the class

We will create a class to represent a Student. You probably have not created a class in C++ before, so here are the [Pair.h](code/Pair.h) and [Pair.cpp](code/Pair.cpp) classes I created as an example in class. Use this code as an example/template.

The instance variables for a Student will be:

| Instance Variable Name | Type         | Default value | Notes                                                                                                                              |
| ---------------------- | ------------ | ------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| myName                 | string       | ""            | Immutable (NOTE: this **is not** a const in our class, but we will **not** be making setter functions for these immutable values.) |
| myId                   | unsigned int | 0             | Immutable (NOTE: this **is not** a const in our class, but we will **not** be making setter functions for these immutable values.) |
| myGpa                  | float        | 0.0           |                                                                                                                                    |
| myMajor                | string       | "Undecided"   |                                                                                                                                    |

In **Student.h**, you should see the definition of the `Student` class. In that class, create the **private:** section, and in there define the 4 instance variables, shown in the table above. You'll have to `#include <string>` and do the using `namespace` business...

Compile (type: `make tester`) and fix any errors. (You may see warnings -- you can ignore those for now.)

In **Student.h** define the default constructor (in the **public:** section). In **Student.cpp**, create the default constructor implementation, initializing the instance variables to their default values, as shown in the table above.

```{important}
Compile and fix any errors!
```

### Step 2. Create _getters_

In your **tests.cpp**, you'll find the first `SECTION` of unit tests called "student getters", within the `TEST_CASE` "Student class". Uncomment the first `SECTION`, so that the code to construct a Student object and then test `getMajor()` runs.

```{caution} Compile
The compilation should fail because we haven't defined `getMajor()` yet. There should be no other problems.
```

So, create a getter function (in both the **Student.h** and **Student.cpp** files) called `getMajor()`.

Compile and run (in a terminal, run `./tester "Student class"`) — this should work now.

Now, repeat the above steps for the other tests and instance variables.

```{important}
That is, create tests for the getters and then implement them according to the instructions at the table above. Start with a test in **tests.cpp** first, then implement the prototype and code.
```

```{note}
Don't delete any old tests -- just keep adding more. Put each test in its own `SECTION` within the "Student class" TEST_CASE.
```

### Step 3. Create _setters_

For the instance variables that are mutable (see the table above), create setter methods. But first, for each, create a test. Put all of these tests in a new `SECTION` within the "Student class" `TEST_CASE`.

```{tip} Example
For the `setGpa` test, set the student's gpa to 3.25, then in a REQUIRE statement, call `getGpa()` and make sure the value is 3.25. Make sure the return type for your setters are `void`.
```

### Step 4. Create an explicit-value constructor

Now, create a second constructor -- the explicit-value constructor. This constructor should take the two immutable fields as parameters, and store their values in the instance variables. Initialize all the other variables to their default values. BUT FIRST, create tests. I called my SECTION `"student explicit-value constructor"`, and in it I create a `Student` with the explicit-value constructor and then use the getters on all instance variables to make sure the object has the correct values in it.

```{important}
Compile and test the result. Fix any errors.
```

You are now done with this simple class. We could add tons of other functionality to it, but not now...

Before you go on, **Commit and Sync** your changes to your github repo. You can easily do this from VSCode. After you do this, you should be able to see that the automated tests fail — but the one test that tests the `"Student class"` passes. If it does not pass, fix your code (or your tests), and resubmit until it does pass.

## Part 2: Fraction class

A Fraction class is a useful class to create. It stores a numerator and denominator and can do things like represent itself nicely (e.g., "3/4"), simplify itself, multiply itself with another fraction, etc.

### Step 1. Test the Fraction class

We'll continue to use **tests.cpp** — **don't remove any code from there**. But, now we'll also use it to create and test Fraction class instances. However, our **makefile** does not compile the Fraction stuff yet.

Edit the **makefile**, adding **Fraction.cpp** to the `SOURCES` line.

```{tip}
Space separated! **Do not** remove *Students.cpp*.
```

In **tests.cpp**, below all your tests for the Student class, add the tests shown below:

```cpp
TEST_CASE("Fraction class") {
    SECTION("fraction constructors") {
        SECTION("default") {
            Fraction fr;
            REQUIRE(fr.getNumerator() == 0);
            REQUIRE(fr.getDenominator() == 1);
        }
        SECTION("explicit value") {
            Fraction fr(2, 4);
            REQUIRE(fr.getNumerator() == 2);
            REQUIRE(fr.getDenominator() == 4);
        }
    }
}
```

```{important}
You'll have to `#include "Fraction.h"` at the top of the file.
```

### Step 2. Add the instance variables and constructors

1. Add the two instance variables — `myNumerator` and `myDenominator` (both integers) — to the class definition in the .h file.
2. Update the default constructor, to initialize `myNumerator` to 0 and `myDenominator` to 1.
3. Now, implement the explicit-value constructor, which takes both the numerator and denominator as parameters, and stores them in `myNumerator` and `myDenominator`. Don't forget to put the declaration in the .h file and implementation in the .cpp file.

```{note}
We will compile our tester after the next section.
```

### Step 3. getters

Add a new `SECTION` (within the "Fraction class" TEST_CASE) called "fraction getters" and SECTIONs to call the getter functions and test their results. Compilation should fail, as expected.

```{warning}
Yes, this is repetitive as we already used them for the default constructors. Just to make sure we cover all our bases, and this can easily be seen in our tests, make another SECTION to quickly check the getter functions again.
```

Now, create getter functions for each.

Now the compilation and execution should succeed with all tests passing.

````{note}
You can run only some tests by putting the name of the test on the command line. E.g., you can run only the Fraction tests by running:

``` bash
./tester "Fraction class"
```
````

### Step 4. setters

1. Create tests to test setters, using the return type of void.
2. Then, create the methods and the code so it will compile and run successfully.

### Step 5. Fanciness

Now, in `setDenominator()`, check if the parameter is 0 — an illegal value. If so, throw an **invalid_argument exception** (remember to `#include <stdexcept>` first). You can do this by using the line:

```cpp
throw invalid_argument("Your error message here!"); // (Change the error message please!)
```

Here is a test for that, assuming you have a fraction called f1:

```cpp
SECTION("setDenominator") {
    REQUIRE_THROWS_AS(f1.setDenominator(0), invalid_argument);
}
```

### Step 6. Display as a _string_

Create a test to call `asString()` on a Fraction object: If you create a new Fraction object `newFrac` and call `newFrac.asString()`, you can `REQUIRE` that the result should be "0/1". Initially, this test will fail, so create the method, which returns a string. This function will be a const function - it will not change any of our private variables. Make sure to define it as `string asString() const`.

```{note}
In `asString()` you can use `to_string(anInt)` to convert an integer into a string. And, you can concatenate strings with +. `to_string()` is defined in `<string>` so you'll have to `#include` that.
```

When that works, use the setters to change the numerator and denominator for a fraction, and then write a test to ensure that `asString()` still produces the correct results.

## Submission

Commit your changes to your github repo. After you do this, verify that the automated tests pass. The automated tests just run the **tests.cpp** file you have been editing.

Don't forget to look at the Grading Rubric at the top to make sure you get as many points as possible.

## Grading Rubric

This lab is worth 20 pts:

- 10 points for each of Part 1 and Part 2: 20 pts
  - 6 pts for correctness
  - 1 pt for perfect indentation and good variable names, function names, and comments (i.e., hospitable code). You should write a comment in your code only when the following block of code is not _obvious_ to the trained reader. You should not write a comment for each line of code.
  - 3 pts for sufficient test cases to prove that the code is correct.

Ways students have lost points in the past:

- -2: Test doesn't pass.
- -1: Missing name and id.
- -3: Missing steps. Next time speak to professor.

<!-- [^1]: how to add footnotes. -->
