---
title: Project 02
subtitle: Falling Sand Simulator
---

## Step 0. Prepare

1. Click [the link](https://classroom.github.com/a/IOEaD8MT) and then "Accept this assignment".
   <!-- 1. Click [the link]() and then "Accept this assignment". -->
   - Wait a few seconds and refresh the page. Refresh until the page says "You're ready to go!". The page has a link to a github repo.
   - Click the link to see your new repo on github.com.
   - Click the green <span style="color: green;">Code</span> button and copy the SSH link it shows.
2. In a terminal,
   - `cd` to the directory where you are putting all your CS112 assignments.
   - type `git clone paste-the-contents-of-the-link-you-copied`
3. `cd` to the new directory containing your repo.
   - type `code .` to start up Visual Studio Code in that directory.
   - Inspect the code you got in the assignment.
   - In the terminal, type `make`
   - The code should compile and give you an executable called **FallingSand**.
4. Run the program: type

```bash
./FallingSand <YourBridgesName> <YourBridgesId>
```

## Step 0.1. Setting Up Your Bridges Account

You will need to make yourself a [Bridges Account here](http://bridges-cs.herokuapp.com/signup).

Please use your Calvin information, and do fill in the optional fields correctly. Use "CS112" as the Course number.

```{warning} NOTE NOTE NOTE
You will not be able to build your program on your own machine unless you [download and install the Bridges libraries](https://bridgesuncc.github.io/bridges_setup.html) and include (header) files correctly. **DO NOT** ask Prof. Wieringa or Prof. Araújo to help you do that. Instead, just use Coder system!
```

To get your username and id, login to the bridges project, and go to the **Profile** page where you will see your "User Name" and "API Sha1 Key". That second thing is your unique id.

## Step 0.2. Instructions

In this simulation, you can move your cursor around a two-dimensional "board" and create or delete one of 3 different "elements" — a square of sand, a drop of water, or a block of metal. Here is what happens when each element is created:

- **Metal:** it sticks to the board where you place it.
- **Sand:** it falls down the board, stacking up on Metal or other Sand, or on the bottom. If Sand encounters water below it, the two switch places, so that it seems the sand is falling through the water.
- **Water:** it falls down the board and fills in any "cups" created by Metal or Sand, or resting on the bottom. If it encounters Metal, Sand, or Water below it, and there is nothing to the left or right of it, it moves sideways left or right, randomly. This makes the water flow around obstacles.

```{figure} imgs/proj02-falling-sand.png
---
name: proj02-falling-sand
---
Falling Sand Simulator.
```

In the image above you can see how **Sand** stacks on top of **Sand** and **Metal**. The **Water** will fill in any area that is a "cup". If one were to move the **Cursor** (the 6-point star) over above the **Water** that is in the cup in the middle and drop a **Sand**, it would slide down the board, falling through the **Water**, leaving a **Water** up above the level of the **Sand**. The **Water** would then randomly move back and forth until falling down to the bottom.

The user interface for the "game" is a little strange, IMO. You use arrow keys to move the cursor around — this should all work. Then, you choose W, A, S, or D to choose whether you are in Water mode, Metal mode, Sand mode, or Delete mode. When you hit the **space bar**, a Water, Metal, or Sand is created, or whatever the cursor on is deleted, if in Delete mode.

Note that if you move the **Cursor** on top of a **Metal** and go into **Sand** mode, you can replace a metal with a sand — a little strange, but don't worry about that — it isn't a bug.

## Step 1. What you need to do

Look at the code in the file **FallingSand.cpp** and search for the word **TODO**. You need to follow the instructions and implement code below each **TODO** comment. There are **5 places** where you have to implement the code.

```{tip} STRONG HINT
Implement one TODO, and then see if you can compile, run, and connect to the online server. If you can and what you implemented seems correct, then repeat these steps. **Do NOT implement too much** before trying your code with the online server. If you do that and something is wrong, you don't know where the problem is.
```

In each place, you'll get practice with looping over a 2-dimensional grid, using the switch statement, using many if statements, and calling functions from the Bridges API. For those API calls, there are other examples in the code already which you should refer to.

## Submit

In VS Code, click on the Source Control icon on the upper left and type in a commit message, then click the checkmark icon to submit your code. Go through the various pop-up boxes to commit and sync your changes to your repo.

```{warning}
Verify you have synced your code to github by going to your online repo webpage and looking to see that the files are correct.
```

## Grading Rubric

This project is worth 20 pts:

- 15 points for generating a correct Falling Sand Simulator.
- 5 points for clean, neat, well-indented code, with good variable names, etc.
- The project is due at midnight next Monday. You will receive a 10% per day penalty for lateness.
