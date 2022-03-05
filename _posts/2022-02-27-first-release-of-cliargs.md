---
published: true
date: 2022-02-27 15:19:00 +0100
last_modified_at: 2022-02-27 18:19:00 +0100
title: First release of Cliargs.NET
description: >-
  A short introduction to Cliargs.NET library and a quick description about its first release
comments: true
categories:
  - Development
  - .NET
tags:
  - dotnet
  - csharp
  - cliargs
  - open-source
fullview: true
toc: true
---

For those following me on Twitter, I was sharing some notes about Cliargs.NET during the last weeks, so I ended up by publishing the first release on Nuget last days.

# Background
Since I've started programming with C#, I had always to manage the CLI arguments manually, parsing, validating the input, handling the different scenarios... All this takes a lot of time, especially when you upgrade the software and you have to deal with new arguments, then you have to pass through the same steps again...
I decided to develop Cliargs.NET to reduce all the time I have to spend in programming the user input management.

## What is `Cliargs.NET`?
Cliargs.NET is a .NET library helping to parse the Command Line Interface arguments in easy way and all in C# without having to play with keys strings and argument values parsing.

## Why `Cliargs.NET`?
For sure there may be [other libraries on Nuget][3] doing the same thing, but once starting managing advanced options, you'll face a lot of limitations. The goal from creating Cliargs.NET is to go from basic usage till very advanced usage, such as pre-defined rules validation and so on.
So at the end, the developer has nothing to do except calling the right methods on the correct time to make all working as expected.

# How to get `Cliargs.NET`?

`Cliargs.NET` is an open source library, where the code is hosted on Github, so you can get the code directly from the [Github Repository][1].

Also, the package is available on [Nuget][2], to install it on your project, just execute the following command from Nuget Package Manager on Visual Studio or from dotnet CLI:

## From Pacakge Manager
```shell
Install-Package Cliargs.NET
```

## From .NET CLI
```shell
dotnet add package Cliargs.NET
```
# How to use it?
Ok, if you're interessted to take a look on how it works, I invite you to check the [Quick Startup example][4] in the [Wiki][5].



[1]: https://github.com/YounesCheikh/Cliargs.NET "Cliargs.NET Repository on Github"
[2]: https://www.nuget.org/packages/Cliargs.NET/ "Cliargs.NET Package on Nuget"
[3]: https://www.nuget.org/packages?q=command+line+interface "Other packages for CLI"
[4]: https://github.com/YounesCheikh/Cliargs.NET/wiki/Quick-Startup "Quick Startup Example"
[5]: https://github.com/YounesCheikh/Cliargs.NET/wiki/ "Cliargs.NET Wiki"
