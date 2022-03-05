---
title: Basicmenu Library
comments: true
description: An open source library coded in C, allows the programmer to create and display a menu easily in his/her console application on linux and mac os x, works with C/C++ programs.
categories:
  - Development
  - C Programming
tags: [c]
fullview: true
---


[Basicmenu](http://cyounes.com/projects/basicmenu) is a an open source library coded in C, allows the programmer to create and display a menu easily in his/her console application on linux and mac os x, works with C/C++ programs.


## Screenshoot example
![BasicMenu Library]({{ site.ImagesFolder }}/basicmenu.png)


## Installation

There is no installation required, you need just to download the basicmenu.h file, include it in your code then start use the libray :)

```c
#include "basicmenu.h"
```

## Essential functions
To use this library , you have just to learn about some basic functions

### 1. Start the basic menu library
First you need to tell the program that uses the library
to do this, invoke `startBasicMenu()` function in the beginning of the main.


### 2. Create and initialize a new menu

To create a new menu you need to declare it with its type:
```c
custom_Menu* mymenu;
```
To initialize it with the `init_new_menu()` function:
```c
init_new_menu (&mymenu);
```

### 3. Add a new item to the menu

Any menu, needs to have at least tow items, to add a new item to the menu use the `addNewItem()` function:
```c
addNewItem (&mymenu , "Choice number one!");
addNewItem (&mymenu , "Choice number tow!");
```
You can add unlimited number of items, but be careful to don't exceed the console size :)
`see the TODO list.`

### 4. Put and display a menu into the program

To display the menu you need to invoke the <code>put_menu()</code> function.
example: <a href="https://raw.githubusercontent.com/YounesCheikh/old_younescheikh.github.io/master/Content/Docs/basicmenu/example1_8c-example.html">Link</a>

## TODO

- Allow the programmer to add unlimited items to the menu.
- Add a scroll menu option.
- Add the maximum of items to shown on the menu.

for more functions and examples please visit <a href="https://raw.githubusercontent.com/YounesCheikh/old_younescheikh.github.io/master/Content/Docs/basicmenu/examples.html">the documentation</a>

> Are you a developer? Fork me on GitHub, I'll be very happy to take pull requests from others, Go ahead and fork me.
{: .prompt-info }



## Documentation

for code documentation please visit  <a href="https://raw.githubusercontent.com/YounesCheikh/old_younescheikh.github.io/master/Content/Docs/basicmenu/examples.html" >Documentation page</a>
