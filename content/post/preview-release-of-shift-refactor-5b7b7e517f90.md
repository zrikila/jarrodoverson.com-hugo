+++
showonlyimage = false
draft = false
image = "https://cdn-images-1.medium.com/max/1920/1*9Q5fjqKluA2hEClylp4QPg.jpeg"
date = "2019-08-09T22:51:27.056Z"
title = "Preview release of shift-refactor"
categories = [ ]
+++




<span class=subtitle>Transform, manipulate, and deobfuscate JavaScript with shift-refactor</span>


<!--more-->

For the last few weeks I have live streamed several reverse engineering and deobfuscation sessions. In these sessions I’ve been using an up-til-now unpublished library.

<iframe width="560" height="315" src="https://www.youtube.com/embed/YqmmFXVAEkA" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Today I am publishing a preview version of shift-refactor that you can install via npm:

```
$ npm install shift-refactor
```

## What does shift-refactor do?


shift-refactor is a general purpose JavaScript manipulation and refactoring tool. It provides many common methods you’d want to use when dealing with source code. Methods that allow you do things like rename variables, delete statements, or insert helper code before a line. Transforming JavaScript source is nothing new but it’s never been something many would call quick and easy. Existing methods often rely on tree traversals, tree folds or reducers, and other code-or-configuration-heavy ways of finding and modifying an AST, an abstract syntax tree. An AST is just a big data structure that represents parsed source code. shift-refactor abstracts all the work of traversing an AST away via by leveraging shift-query, a library that queries the tree via CSS-style selectors like IdentifierExpression[name=”program”]. This, combined with utility methods like rename, allow you to write complex manipulations in single lines of code, e.g.

```
refactor.rename(`IdentifierExpression[name=”oldName”]`, "newName")
```

I built shift-refactor to help with reverse engineering JavaScript. Reverse engineering means walking through source and identifying its purpose all while navigating traps, pitfalls, and dead ends. What this means in practice is a lot of backtracking and, by hand, that means a lot of CTRL-Z-ing. Codifying reverse engineering operations means that you have a breadcrumb trail to share, fork, and comment.


## Who is shift-refactor for?


You can think of shift-refactor as a very specialized regex replacement library for JavaScript source code. The queries are your patterns and you operate on the matches. If you ever wanted to crawl through and modify JS source with a regular expression then shift-refactor is the tool you didn’t know you needed.


## How can I use it?


Install shift-refactor via npm. You’ll want to install shift-parser as well to parse the target JavaScript.

```
$ npm install shift-refactor shift-parser
```

Parse the target JavaScript and pass it as an argument to create a new RefactorSession. A RefactorSession is a way to store transformations for an AST. All transformations happen off a RefactorSession instance and you generate new source anytime via .print().

```
const { RefactorSession } = require('shift-refactor');
const { parseScript } = require('shift-parser');

const fs = require('fs');

const fileContents = fs.readFileSync('./source.js', 'utf8');

const tree = parseScript(fileContents);

const refactor = new RefactorSession(tree);

refactor.rename('IdentifierExpression[name="oldName"]', 'newName');

refactor.insertBefore(
  `ExpressionStatement[expression.type="CallExpression"]`,
  node => `console.log("Calling ${node.expression.callee.name}()")`
);

console.log(refactor.print());
```

The above code will turn

```
oldName();
otherFunction();
```

Into

```
console.log("Calling newName()");
newName();
console.log("Calling otherFunction()");
otherFunction();
```

The README has many more examples, check them out!


I don’t expect many changes between the preview and release. shift-refactor will sit in preview for a few more weeks while I tune the API. This library is a cleaned up version of code that I’ve been using separately for months. The livestream helps me test the API on real world scenarios. Now that it is released you can play around with the concepts yourself!


[Share this on Medium](https://medium.com/@jsoverson/preview-release-of-shift-refactor-5b7b7e517f90)
