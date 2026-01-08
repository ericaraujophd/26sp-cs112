---
title: Project 09
subtitle: Navigate a Maze Using a Stack
---

## Prepare

[Accept the assignment](https://classroom.github.com/a/dp6oZBYK) and use git clone to create your copy of the code.

## Introduction

A stack can be used to find a path through a maze from a starting point to a finish point (the "goal"). The idea is that at each location (starting from the starting point), you record in the stack where you are in the maze and which direction you are facing. If there is a hallway in front of you, you move to that new point and push a new "record" on the stack. Each time you go to a new location, you always look north first, then west, then south, then east. If you get to a location that is a dead end, you pop the stack, thus moving back to a previous location. A dead-end is when you've looked all 4 directions and found no opportunity to move forward. Also, as you work your way through the maze, you record which locations you have already visited — and you never visit a location twice.

When you reach the goal, the stack will contain the path from the goal back to the starting point. Each location on the path will also record which direction you moved to get to the next location on the path.

### Example

Consider this example:

Pictorially the maze looks like this, with S being the starting point (at 0, 0) and G being the goal (at 2, 3).

```default
-------
|SX  X|
|   X |
|X XG |
|     |
-------
```

After the code solves the maze, the stack and pictorial representation look like this:

```default
FINAL PATH: (2, 3, X) (3, 3, N) (3, 2, E) (3, 1, E) (2, 1, S) (1, 1, S) (1, 0, E) (0, 0, S)
-------
|SX  X|
|pp X |
|XpXG |
| ppp |
-------
```

This maze was read from a file that looks like this:

```default
4 5
SX__X
___X_
X_XG_
_____
```

The first row contains the number of rows and columns. The subsequent rows use \_ for an empty space, X for a barrier, S for the start, and G for the goal.

Your task is to implement the code to

1. Read in a maze from a file.
2. Implement the algorithm given below to solve the maze.
3. Print out the stack as you solve the maze.

```{important} Extra credit
**For extra credit**, you may implement code to print out the maze pictorially, as seen above.
```

The code you have includes the file `main.cpp`, and two sample mazes, `maze1.txt` and `maze2.txt`.

### Details

Your implementation should use the STL stack.

The `main.cpp` code contains a definition of a `Location` class, which stores an `x` and `y` location, and a `dir`, which is the direction you are facing.

Your main task is to implement the `readMazeFromFile()` and `isReachable()` function. The algorithm for the latter is below.

**Algorithm:**

1. Define a stack of Location objects this way: `stack<Location> st;`
2. Push a location object with values (0, 0, -1) on stack (-1 = haven't tried any direction yet)
3. while the stack is not empty:
   1. current_loc = top of stack
   2. pop the stack;
   3. if `current_loc` is the goal,
      1. push the `current_loc` back on the stack
      2. return!
   4. mark the current location as true in the "visited" array.
   5. increment `current_loc`'s direction
   6. if `direction` is north:
      1. if there is not a wall to the north and we haven't visited the location to the north:
         1. push the current_location on the stack
         2. push this new hallway on the stack
         3. continue (to the top while loop)
      2. else: increment `current_loc`'s direction
   7. Repeat step f. for west, then for south, then for east.
   8. // We must be at a dead end: nothing to do -- we already popped this dead-end node off the stack.

### Sample output

Here is sample output from running against file `maze1.txt`.

```default
$ ./main
Enter the name of the file containing the maze: maze1.txt
push on stack. stack is now (0, 0, S)
push on stack. stack is now (1, 0, E) (0, 0, S)
push on stack. stack is now (1, 1, S) (1, 0, E) (0, 0, S)
push on stack. stack is now (2, 1, S) (1, 1, S) (1, 0, E) (0, 0, S)
push on stack. stack is now (3, 1, W) (2, 1, S) (1, 1, S) (1, 0, E) (0, 0, S)
dead end: going back to (3, 1, W) (2, 1, S) (1, 1, S) (1, 0, E) (0, 0, S)
push on stack. stack is now (3, 1, E) (2, 1, S) (1, 1, S) (1, 0, E) (0, 0, S)
push on stack. stack is now (3, 2, E) (3, 1, E) (2, 1, S) (1, 1, S) (1, 0, E) (0, 0, S)
push on stack. stack is now (3, 3, N) (3, 2, E) (3, 1, E) (2, 1, S) (1, 1, S) (1, 0, E) (0, 0, S)
FINAL PATH: (2, 3, X) (3, 3, N) (3, 2, E) (3, 1, E) (2, 1, S) (1, 1, S) (1, 0, E) (0, 0, S)
Path Found!
```

```{important} Extra credit
**For extra credit**, you may implement code to print out the maze pictorially, as shown above in the Example section.
```

## Submission

Don't forget to check in your code to github.

## Grading Rubric

The assignment will be graded as follows:

Total points: 20 (23 with extra credit)

- 4 pts for `readMazeFromFile()`
- 10 pts for `isReachable()`
- 3 pts for correct output
- 3 pts for style / documentation
- +3 pts for pictorial displays as the maze is solved.

Ways students lost points in the past:

- -8: `isReachable` does not follow algorithm in instructions and does not compile or work
- -1: `readMazeFromFile` creates a new local "maze" variable instead of reading into the global one
- -3: Missing text output for path tracing
- -2: Text output for path tracing is not detailed enough, see assignment
- -2: Missing continue step
- -2: Need to push the current location back onto the stack before pushing the next one
- -1: Missing dead end output
- -1: Mistake in north check
- -4: The entire `readFromFile()` function does not work. Please test run your code!
