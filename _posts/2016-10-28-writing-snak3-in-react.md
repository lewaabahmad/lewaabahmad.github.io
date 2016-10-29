---
layout: post
title: Writing Snak3 in React
---

Wrote it up today. Wanted to write about the process but didn't. In hindight, I would've put a lot of detail for nothing.

[This is what I ended up writing.](https://github.com/lewaabahmad/snak3/blob/react-2d-v1/react-2D/components/board.js)

You can navigate to the index.html file to see the environment in which this React component gets injected (it's not too interesting). This is done on this line:

[```ReactDOM.render(<Board />, document.getElementById('game'))```](https://github.com/lewaabahmad/snak3/blob/react-2d/react-2D/components/board.js#L171).

I ended up essentially only writing ONE big component. I don't know. It made a lot of sense to me when I was building it. I figured that the snake wasn't any different than the board. Afterall, I was using CSS to style the different tiles. 

But therein lies my error. I didn't realize that the tiles had states themselves. They were either occupied by a part of the snake, occupied by an apple, or empty. 

It's funny because it's a little wonky to think about - especially if you're used to seperating out code/functionality into modules already. In this case for example, the snake stretches across our component verticals - it is rendered by a board and its tiles and represented by the state of tiles. Cool, haha. 

I guess it makes sense if you consider that React is a UI centric framework. It's meant to manipulate visual elements. It doesn't care what they are, per se. 

Speaking of thinking in React, [this is something I ought to read.](https://facebook.github.io/react/docs/thinking-in-react.html) 

I can definitely refactor this code, but for right now, I'm fairly satisfied with it. 