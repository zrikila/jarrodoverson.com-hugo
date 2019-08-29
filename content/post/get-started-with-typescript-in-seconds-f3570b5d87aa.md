+++
showonlyimage = false
draft = false
image = "https://cdn-images-1.medium.com/max/2500/1*EBJc26L-QRsHI3NcjscsOA.jpeg"
date = "2019-04-01T14:45:24.420Z"
title = "Get started with TypeScript in seconds"
categories = [ ]
+++




<span class=subtitle>No config. No hassles.</span>


<!--more-->

JavaScript fatigue is real. It’s what happens when you try to get into the next hot thing but the next-next hot thing gets added to your plate before you’ve figured out the first hot thing and then, when you’re figuring out which hot thing to focus on, the developers of the first hot thing release version 2 with breaking changes but it’s ok because the changes are also the next hot thing.


It’s easy to see something like TypeScript and think “whoa now, that’s a whole new language, I can’t bother with that right now” and, to be fair, a few years ago I was on your side. I tried to like it but the effort of getting it up and running and sticking with it was too much for the value. Now, though, it’s a totally different game. TypeScript is better, the tools that support it are better, and Visual Studio Code is the killer app that makes at least exploring TypeScript a no-brainer.


Here’s how to give TypeScript a shot with virtually no effort whatsoever.


### 1. Set up a new project folder

```
$ kickstart my-project
```

What? You don’t have a kickstart command? If you’re a developer then you probably have loads of little projects lying around — half-made libraries, scratch directories for experiments, modules for a larger project, whatever. If you’re anything like me then you start all of them the exact same way each time. Put those common commands in a kickstart script or function and use it to get started faster. Mine is below — the function makes a directory, moves into it, initializes git, initializes npm, and opens VS Code. It also adds a bit of motivational support at the end because, hey, who can’t use a little digital hug? Just add the following to your .bashrc (or .bash_profile or whatever you use) and you’re good to go. Or start a project whichever way you want, you do you.

```
kickstart () {
  mkdir $1 && cd $1 && git init && npm init -y && code .
  echo "You're awesome 🤘"
}
```

### 2. Create an index.html

```
<!doctype html>
<html lang=en>
  <head>
  </head>
  <body>
    <script src='./src/index.ts'></script>
  </body>
</html>
```

### 3. Create your TypeScript file


Add a new file in a src directory (or wherever you want) but make sure it has a .ts file, not a .js extension. Here’s an example if you want something to copy and paste.

```
window.addEventListener('load', () => {
  const body = document.body;
  const p = document.createElement('p');
  p.innerHTML = 'Hello world';
  body.appendChild(p);
})
```

“But wait, that looks like JavaScript” — that’s true, it is 100% normal JavaScript but that’s half the point of TypeScript. TypeScript is all on top of JavaScript so you can just use plain JavaScript and absorb the parts of TypeScript you want when you want them. If you really want some types in now to prove you are actually in type-land, use the script below which adds a function with typed parameters.

```
window.addEventListener('load', () => {
  appendMessage(document.body, 'Hello world');
})
```
```
function appendMessage(element: HTMLElement, msg: string) {
  const p = document.createElement('p');
  p.innerHTML = msg;
  element.appendChild(p);
}
```

### 4. Run parcel

```
$ npx parcel-bundler index.html
```

Not familiar with npx or parcel? Lucky you! There’s a rundown video for npx and another one for parcel. Npx is just a way to run npm-installable commands without thinking about how they are installed and parcel is a configurationless web bundler. In this case npx will download, install, and run parcel-bundler from npm. You can also install parcel-bundler via npm install -D parcel-bundler and then npx will run the locally installed version. If you don’t want to use npx, you can also install and run parcel globally, directly from node_modules, or by adding an npm script to your package.json.


### 5. That’s it.


Your project is set up with typescript now. Just visit the URL that parcel shows you (http://127.0.0.1:1234 by default) and explore the wonders of TypeScript. From here you can proceed as normal.


## Ok cool, but how do I use React?


If you’ve read other “Get started with [x]” tutorials, you may have experienced the bait-and-switch emotional rollercoaster where you experience a premature sense of enthusiastic optimism and then get left in a lurch as soon as you try to do anything useful. I’ve been there, I get it. So you use React and JSX and you’re wondering how to wire it up now? Well getting started is as easy as changing your file extension to .tsx instead of .ts.


That’s it. I’m serious.


Try it out with the following TypeScript snippet (after installing dependencies with npm install -D react-dom react of course).

```
import * as React from 'react';
import { render } from 'react-dom';
```
```
class MyElement extends React.Component {
  render() {
    return <div>{"Hello World"}</div> 
  }
}
```
```
render(<MyElement/>, document.body)
```

If Visual Studio Code gives you any red squigglies, then the popup help’s “quick fix” options should be able to handle it for you.


Hope this helps you get started with TypeScript. You will inevitably come across something that isn’t quite so plug-and-play and, if you do, please let me know and I’ll write up another post so others can get the help they need.


[Share this on Medium](https://medium.com/@jsoverson/get-started-with-typescript-in-seconds-f3570b5d87aa)
