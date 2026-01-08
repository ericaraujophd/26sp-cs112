---
title: Project 05
subtitle: Processing Video Game Data
---

## Introduction

In this project, you will use the C++ Standard Template Library (STL) vector class to store and analyze video game data retrieved using the Bridges Library.

You can see an example application that pulls the [video game data here](http://bridgesuncc.github.io/tutorials/Data_IGN_Games.html). (Click on the C++ tab.)

Each Game is stored in a Game object. Information about the [Game class is here](http://bridgesuncc.github.io/doc/cxx-api/current/html/classbridges_1_1dataset_1_1_game.html).

Inspect that web page now to see what information you can retrieve about a Game.

The database contains 17,534 games in 33 genres. When you retrieve the games, they are not in any sorted order.

This assignment is to process the games to

1. Discover all the unique genres and print them out.
2. Ask the user to select a genre and print out all the games in that genre.
3. Do one more task of your own choosing.

## Setup

Make your **proj5** repo as normal, using [this link](https://classroom.github.com/a/UlvbgSvg).

You will need to make yourself a [Bridges Account here](http://bridges-cs.herokuapp.com/signup).

Please use your Calvin information, and do fill in the optional fields correctly. Use "CS112" as the Course number.

To build your program use `make`. It produces an executable called **games**.

```{note} NOTE NOTE NOTE
You will not be able to build your program on your own machine unless you download and install the Bridges libraries and include (header) files correctly. DO NOT ask Prof. Wieringa or Prof. Araújo to help you do that. Instead, just use the machines in the lab or access your virtual machine through [Coder](https://coder.cs.calvin.edu/)!
```

To run your program you have to provide **two command-line arguments**: your Bridges _UserName_ and your Bridges _Id_. E.g., I run the program this way:

```bash
./games ericaraujo 1313148564
```

To get your username and id, login to the [bridges project](http://bridges-cs.herokuapp.com/login), and go to the Profile page where you will see your "User Name" and "API Sha1 Key". That second thing is your unique id.

## Information about using vector

You will use the STL's vector class template multiple times. The functions I used from the vector class were:

- `size()`
- `operator[]` to index into the vector.
- `push_back(value)`

In addition, you'll need to use the `find()` function which is outside of the vector class. Here is an example of how to use it to search a `vector<string>` called `genre_vec`:

```cpp
if (find(genre_vec.begin(), genre_vec.end(), "Pinball") == genre_vec.end()) {
    // "Pinball" was not found in genre_vec.
}
```

The `find()` function takes three parameters: where to start looking, where to stop looking, and what to look for. If the target string ("Pinball") is not found at all, then the function returns `yourvector.end()`. In all uses of your code, you will always search the entire vector, so always use `yourvector.begin()` and `yourvector.end()` as the first two parameters.

To sort a `vector<string>` you can just do this:

```cpp
sort(yourvector.begin(), yourvector.end());
```

## Step 1: Implement collecting all the genres for the games

In the starting code you received in your repo, you'll see that **main.cpp** implements a simple menu system to allow the user to choose what action to take. Your job is to fill in the code to implement those actions, and at the end, add your own option.

Start by implementing the "_Show all genres_" option by creating the function `collectAllGenres()`. This function takes one parameter — the vector of Game objects — and returns a vector of strings containing all the discovered genres, in sorted order. Make sure you pass in the parameter _efficiently_ (**do not** use pass-by-value).

The function should first create a variable— I called it `all_genres` — that is a vector of strings. It will hold all the genres seen. Then, the function should loop through all the Game objects in the vector, and for each Game, loop through all genres the game belongs to. For each genre, it should search `all_genres`. If the new genre has not been seen before, add it to the end of the `all_genres` vector using `push_back()`.

After getting all genres from all games, you should sort the vector and then return that vector of strings.

Your main code should print out the genres in a nice list with numbers in front, like this:

```
All genres:
1. Action
2. Adult
3. Adventure
4. Baseball
5. Battle
6. Board
7. Card
8. Casino
9. Compilation
... etc ...
```

## Step 2. Print all games in a selected genre

In the case statement in the main code, ask the user for a number of a genre: (the user enters 32 below)

```
Enter a number of a game genre to see how many games are in that genre: 32
```

From that number, index into your vector of game genres to get the name of that genre. Then, call a function, described below to get all titles in that genre. After you get the titles, print each one out.

Your function needs to iterate through all games, looking for the games that belong to a given genre. I called my function `getTitlesInGenre()`. The function should return the `vector<string>` containing those games' titles, in sorted order. My implementation of `getTitlesInGenre()` takes two parameters — the vector of all Games, and a string that holds the genre to search for. Make sure you pass both parameters in **efficiently**.

Remember that a game can belong to multiple genres, so you'll have to get the genres for each game, and go through each genre to look to see if the game belongs to the "target" genre.

````{note}
Your code should only add a game's title to the results if the game's title is not already in the results. If your `vector<string>` results variable is called `results`, then use this code to detect if the game's title is already in the `results`, and add it only if it isn't:

``` cpp
// if not already found in the vector, add it.
if (find(results.begin(), results.end(), game.getTitle()) == results.end()) {
    results.push_back(game.getTitle());
}
```
````

Don't forget to sort the results before returning it from the function.

The main code should then print out the result from the function.

## Step 3. Implement something else interesting

In this step, you get to implement something of your own choosing.

Add comments to your code to describe what your option does (if it isn't obvious). Put your code in its own function.

Here are some ideas, but I'd prefer if you came up with your own:

- Ask the user for a game title and find all matches in the list and print all information about each match.
- Ask the user for a game genre and print out the top 10 games according to their rating.
- Create a line graph or bar graph showing how many games of each genre are in the data. Bridges has a LineGraph class you could use. If you want to create a Bar Graph, you could perhaps use the Color Grid class.
- Create a line graph showing how many games were released in each year. Use Bridges's LineGraph class.

## Testing

The graders will test your code by running the pexpect script, **test.exp**, you see in your repo. They will do this by just running

```bash
python test.exp
```

That script runs your game's executable and sends it menu items, looking for the correct output. You could try this against your code too. This should work on lab machines, but won't work on your machine unless you install the python **pexpect** library.

## Submission

Take a look at the Grading Rubric below and make changes to maximize your score.

Don't forget to **Commit** and **SYNC** your changes to your repo.

```{warning}
Verify you have synced your code to github by going to your online repo webpage and looking to see that the files are correct.
```

## Grading Rubric

This project is worth 20 points:

- 15 pts for correctness
- `collectAllGenres()`: 5 pts.
- `getTitlesInGenre()`: 5 pts.
- your own option: 5 pts.
- 1 pt for efficient passing of parameters.
- 2 pts for perfect indentation and good variable names, function names, and comments (i.e., hospitable code). You should write a comment in your code only when the following block of code is not obvious to the trained reader. You should not write a comment for each line of code. Writing a comment above the non-obvious methods can be very useful.

Ways students lost points in the past:

- -3: `collectAllGenres()` does not print all results
- -3: `getTitlesInGenre()` does not work for a specific genre
- -4: Option 2 and 3 does not work properly
- -5: Late submission
- -5: missing a step
