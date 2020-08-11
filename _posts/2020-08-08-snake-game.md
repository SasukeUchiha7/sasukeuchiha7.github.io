---
title: ":snake: A classical Snake Game in C++"
layout: post
date: 2020-08-08 20:10
tag:
    - c++
    - game
projects: true
hidden: true
description: "A classical Snake Game using C++"
category: project
permalink: snake-cpp
author: sasuke
---

## A snake game

We all used to play a very famous classical game in our old end devices way back when we were kids.

<p> And just to give tribute to that nostalgic feeling we are gonna build a similar game using nothing but simple c++ code.</p>
<p>So, let's get stared.</p>
Our program will look like this:
    
<img src="./assets/images/oss.jpg"/>
<figcaption class ="caption"> Output terminal of our program</figcaption>

## Building

The code is very much simple. We will be using iostream and conio.h header.

<p>You may ask why conio.h, but we will understand that when we will go through codes.<br>
So, your include section look like this.</p>
{% highlight cpp %}
#include <bits/stdc++.h>
#include <conio.h> // for function like khbit() and getch()
using namespace std;
{% endhighlight %}

After that we will initialize some varibles globally which we will need throughout the program.
{% highlight cpp %}
// global variables
bool gameover;
const int width = 20;
const int height = 20;
int x, y, fruitX, fruitY, score;
int tailX[100], tailY[100]; //snake coordinates
int snakeLen;

// Controls
enum movements
{
STOP = 0,
LEFT,
RIGHT,
UP,
DOWN
};
movements mov;
{% endhighlight %}

<p>After this we will define some funciton to setup your game.</p>
The setup function look like this which initialise the parameter of the game.
{% highlight cpp %}
void Setup()
{
    gameover = false;

    mov = STOP;

    x = width / 2;

    y = height / 2;

    fruitX = rand() % width; //placing fruit in a random place

    fruitY = rand() % height;
    score = 0;

}
{% endhighlight %}

The display function will look like this which will display the game.
{% highlight cpp %}
void Display()
{
system("cls");
for (int i = 0; i < width + 2; i++)
cout << "#";
cout << endl;
//Inside of game
for (int i = 0; i < height; i++)
{
for (int j = 0; j < width; j++)
{
if (j == 0)
cout << "#";
if (i == y && j == x)
cout << "^"; // snake's head
else if (i == fruitY && j == fruitX)
cout << "O"; // fruit
else
{
bool print = false;
for (int k = 0; k < snakeLen; k++)
{
if (tailX[k] == j && tailY[k] == i)
{
cout << "_"; // adding snake _ in snake's lenght
print = true;
}
}
if (!print)
cout << " ";
}
if (j == width - 1)
cout << "#";
}
cout << endl;
}
for (int i = 0; i < width + 2; i++)
cout << "#";
cout << endl;
cout << "\tScore:" << score << endl;
}
{% endhighlight %}

<p>Now we need a function which will record our movements.</p>
