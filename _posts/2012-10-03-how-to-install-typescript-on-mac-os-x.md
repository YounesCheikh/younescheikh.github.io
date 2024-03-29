---
title: How to install typescript on mac os x
date: '2012-10-03 00:00:00'
description: Mini-Tutorial explains how to install typeScript on Mac OS X easily
comments: true
categories:
  - How To
tags: [macos, tutorial]
---


![typescript]({{ site.ImagesFolder }}/typescript1.jpg)


This article explains how to install [TypeScript][2] on Mac OS X easily.

The following steps are tested on OS X Mountain Lion 10.8.2

## 1. install [Homebrew][3]:

```shell
$ ruby -e "$(curl -fsSkL raw.github.com/mxcl/homebrew/go)"
```

## 2. Install [nodejs][4] using home-brew:

```shell
$ brew install nodejs
```

## 3. get and install npm:

```shell
$ curl https://npmjs.org/install.sh | sh
```

![]({{ site.ImagesFolder }}/install_npm.png)

## 4. get TypeScript:

```shell
$ npm install -g typescript
```

![]({{ site.ImagesFolder }}/install_typescript.png)

## 5. Test TypeScript:

In your editor, type the following JavaScript code in greeter.ts:

```typescript
function greeter(person) {
  return "Hello, " + person;
}
var user = "Jane User";
document.body.innerHTML = greeter(user);
```


## 6. Compile the code:

At the command line, run the TypeScript compiler:

```shell
$ tsc greeter.ts
```

The result will be a file greeter.js which contains the same JavaScript that you fed in.

 [1]: http://cyounes.com/new/how-to-install-typescript-on-mac-os-x
 [2]: http://www.typescriptlang.org/ "TypeScript"
 [3]: http://mxcl.github.com/homebrew/
 [4]: http://nodejs.org
