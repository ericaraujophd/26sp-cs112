---
title: Project 01
subtitle: More Control Structures
---

## Objectives

1. Practice using `for` loops, `while` loops, and `if` statements.
2. Practice creating functions and passing parameters.
3. Practice writing unit tests.

## Step 0. Prepare

1. Click [this link](https://classroom.github.com/a/jzY3a4_d) and then "Accept this assignment".
   - Wait a few seconds and refresh the page. Refresh until the page says "You're ready to go!". The page has a link to a github repo.
   - Click the link to see your new repo on github.com.
   - Click the green <span style="color: green;">Code</span> button and copy the SSH link it shows.
2. In a terminal,
   - `cd` to the directory where you are putting all your CS112 assignments.
   - type `git clone paste-the-contents-of-the-link-you-copied`
3. `cd` to the new directory containing your repo.
   - type `code .` to start up Visual Studio Code in that directory.
   - Inspect the code you got in the assignment.

## Step 1. function practice, 1

In **utils.h**, create a function **prototype** called `constrain()` that has 3 parameters:

- value, a `double`
- low, a `double`
- high, a `double`

`constrain()` returns a `double`, which is the value constrained by low and high. I.e., if the value is greater than high then, return high. If it is less than low, return low. Else, return the value itself unchanged. Remember, in **utils.h** you are writing just the prototype.

Now, in **utils.cpp**, implement the function.

In **tests.cpp**, in the `TEST_CASE("step1")`, add more `REQUIRES()` function calls to test that your function is correct in all cases. We have provided one test there already.

Compile using `make`. Then, run like this:

```bash
./tester step1
```

When you pass the test, **Commit and Sync** your code to github (use a Message like "step 1 done") and check that the autograding test for step1 passes. (It should, as all it does is run `./tester step1`.) (Tests for the other steps will pass, because the test cases are currently empty.)

## Step 2. function practice, 2

Now, make a second function in **utils.h** and **utils.cpp**, `constrain2()`, which is the same as `constrain()`, but has the default value of $0.0$ for the low parameter, and the default of $100.0$ for the high parameter. Uncomment the test case in step2 and then add more `REQUIRE` tests to make sure these default arguments work correctly.

When you have your code completed (and perfectly indented!), compile and run:

```bash
./tester step2
```

**Commit and Sync** your code to github.

```{note}
The autograding tests should now pass "step1" and "step2". (Tests for the other steps will pass, because the test cases are currently empty.)
```

## Step 3. Compute prime numbers

Write a function prototype `isPrime()` in the **primes.h** file. The function takes an **unsigned integer** and returns a **boolean**.

For the implementation in the .cpp file, `isPrime()` returns **true** if the value is a prime number (and **false** otherwise). Here is the pseudo-code:

```
A prime number is a number that is evenly divisible by only itself and 1. That is,
  for each integer "divisor" value from 2 through n / 2,
    if you divide the number by that divisor, and the remainder is 0,
          that number is not prime -- return false.
  if you get through all possible divisors, the number is prime: return true.
```

Note that 1 is not a prime (for some reason). 2 is the first prime. Your code may have to handle this case specially (my code does).

Add code to the "step3" `TEST_CASE` in the **tests.cpp** file to test `isPrime()`.

Make sure you test if 4 is a prime (it isn't). Write other `REQUIRE()` calls to test other values.

When you are satisfied that your code is complete, **Commit and Sync** it to github and check that the "step3" test succeeds.

## Step 4. Collecting prime numbers

In your **primes.h** and **primes.cpp** files, create a function that:

- is called `findNPrimes()` that returns **void**
- takes as a parameter an array of **unsigned** called primes
- takes as a parameter an **unsigned** called size that is the size of the array
- computes the first size prime numbers, putting them into the array (of course, the code calls `isPrime()` to do the hard work)

```{note}
Note that this is a little tricky -- if the size of the array is 100, do you loop up to 1000 to find the first 100 primes? Or 2000? You don't know... So, use a while loop that keeps looping as long as the array is not full.
```

In **tests.cpp** in the "step4" TEST_CASE, write code to define an array of a certain size, call the function, and then `REQUIRE` that various correct values are in the array at the correct indices. You might find it useful to know that the 100th prime is 541.

When you are satisfied that your code is complete, **Commit and Sync** it to github and check that the "step4" test succeeds.

At this point, all autograding tests should pass. You are done!

````{important} OPTIONAL

For fun, create an array of 100000 and fill it with primes. See how long it takes to compute and print out the last prime.

You can get the exact run time by running your project this way:

```bash
time ./tester "step4"
```
````

## Grading Rubric

This project is worth 20 pts:

- 3 points for each of steps 1 and 2 (6 pts total)
- 2 pts for correctness
- 1 pt for thorough tests
- 5 points for step 3
- 6 points for step 4
- 3 pts for code beauty and hospitality.

Here are some ways students lost points in the past:

- -6: Missing step 4
- -1: poor indentation
- -1: low and high are supposed to be parameters
- -3: Missing step 2
- -1: tests in step1 are insufficient.
- -1: tests in step2 do not test all cases.
