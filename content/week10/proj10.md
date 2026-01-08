---
title: Project 10
subtitle: Using Queues to Implement the Snake Game
---

## Objectives

1. Use a Queue to implement the snake game.
2. Gain experience using more complex data structures.

```{figure} ../../figures/snake-game.gif
:width: 30%
From Giphy by \@hmd_global
```

## Step 0: Set Up

[Accept the assignment](https://classroom.github.com/a/qjNZ6tpS) and use `git clone` to create your copy of the code.

## Step 1. Try it out

If you are not familiar with "the snake game", then you can try it out on google. Just type "snake game" into google and it will give you a pop-up game you can try. Use the arrow keys to move the head of the snake and go after the apple in order to make the snake longer and gain points. Don't run into the edges or the snake itself!

In our version of the game, we will allow the snake to wrap round from top to bottom (and vice versa) and left to right (and vice versa). The only way to die is to run into yourself.

We will use the [Bridges library](http://bridges-cs.herokuapp.com/signup) to visualize the game online. We'll use the "Game mode" which requires you to start your program then open the browser and connect to your game. You'll see a button on the web page that looks like this:

```{figure} proj10-button.png
---
name: proj10-button
---
Button to connect to game
```

For our implementation, we'll use a queue to represent the body of the snake. As the snake moves a new block is added to the end of the queue — which is the front of the snake — and the last block of the body is removed from the tail — which is the head of the queue. Each item in the queue will be a Pair of integers, representing the $(x, y)$ location of the block ($x$ is vertical and $y$ is horizontal). So, the snake's queue will be defined as

```cpp
Queue<Pair<int>> snake; // (see line 58 of Snake.h)
```

The only other kinda tricky part of the code is how we grow the snake. The screen is redrawn each frame. A variable, `skipDeletingTailNodesCount`, exists which keeps track of how many subsequent frames should _not_ delete the tail of the snake. So, if the variable has the value 2, the snake will grow by two new segments, because for the next 2 frames the snake's tail will not be deleted.

## Step 2. Your task

There are TODOs littered throughout **Snake.cpp**. Your task is to replace the TODOs with code. Each TODO contains a description of what your code should do.

````{note} A Note about Iterators

You will have to write some code to use the *iterator* class defined inside the Queue class. An *iterator* is an abstract *pointer* — meaning that it can be used like a pointer, but isn't actually a pointer. So, you can get an iterator, `it`, that "points" to an item in the queue and then get the item itself by doing `*it`.

You can use iterators to walk through the snake object, like this:

``` cpp
for (Queue<Pair<int>>::iterator it = snake.begin(); it != snake.end(); it++) {
      // use it here -- remember it points to an item in the queue, and those items are Pair objects.
}
```
````

To run your program you have to provide two _command-line arguments_: your Bridges UserName and your Bridges Id. E.g., I run the program this way:

```bash
./snake EricAraujo 123456789
```

Recall that you can get your username and id from the bridges website: <http://bridges-cs.herokuapp.com/>

## Step 3. Plan of Attack

I recommend you replace the TODOs in this order:

1. do `drawSnake()`
2. Fix `updateSnake()`. After this, you should be able to run your program and see the snake move around.
3. do `plantTarget()`
4. do `detectTarget()`
5. do `detectDeath()`

```{note}
For some of these there are easy ways and hard ways to implement them. Study the Queue class to see what methods exist on a Queue object. I've created some of those methods to help you implement the functions above more easily.
```

## Submission

Don't forget to commit your code to your online repo on [github.com](https://github.com/) so that the grader can grade it.

If, after you submit your code, you want to enhance the game, you could:

- make the game run faster as the snake gets longer.
- make the target be a number between 1 and 9 inclusive, and the snake grows that much longer each time the target is eaten.

(If you make these enhancements, don't submit them. The grader will just grade the basic implementation.)

## Grading Rubric

The assignment will be graded as follows:

Total points: 25 pts total:

- 4 pts: `drawSnake()` correct
- 5 pts: `updateSnake()` correct
- 3 pts: `plantTarget()` correct
- 4 pts: `detectTarget()` correct
- 7 pts: `detectDeath()` correct
- 2 pts: code is clean and neat.

Ways students lost points in the past:

- -2: Can't make file. Error occurs
- -2: Does not allow me to play the game.
- -4: program does not detect collisions correctly.
- -3: program does not "eat" the target correctly.
- -12.5: code is identical with one other person.
- -18: code is identical with 2 other people.
