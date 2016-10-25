---
layout: post
title: Introducing Myself to React
---

React is something I've wanted to get a better, fuller understanding of for a while now. I figured I needed to take the dive and started to look for the best way to pick it up. I'm definitely somone who needs to dive into the implementation and code before stuff starts to make sense. I was looking for something that allowed me to see React functionality via the development of a small project. I found exactly what I needed in [this article](https://www.airpair.com/reactjs/posts/reactjs-a-guide-for-rails-developers) by [Fernando Villalobos]() - thanks man. 

My first problem was a lack in my working knowledge in CoffeeScript. I always disliked it. I feel like it obfuscates what's actually happening under the hood. Also, what is wrong with JavaScript? Ugh. Whatever. I went to the CoffeeScript site and reread the documentation in an hour or two to understand what would be happening. To me, there are a couple really important things to remember in reading CoffeeScript:

1 - blocks are dilineated via indentation 

2 - the @ symbol means this, as in @say_hello is really this.say_hello

3 - no var! variables declerations are written in when compiled and are scoped to their block.

4 - this is how functions are define (much like fat-arrow notation in ES6): square = (x) -> x * x

5 - the last line is returned by default as in Ruby. 

Integrating React into the Rails app was pretty easy: install the `react-rails` gem and regerence the newly availible JS files in your manifest file. 

Great, now that we're clear on CoffeeScript and we've got React into our tutorial app, the next hurdle came with JSX. The way I understand it, JSX is a templating DSL parsed via JavaScript. It allows you to essentially write HTML, interspersing JS code that gets interpolated later. There are some funny quirks like `className=` must be used instead of 'class=' for HTML elements because class is a reserved keyword. Here's an example of some JSX: 

```JavaScript
function helloWorld() {
  return (
    <div className="hello">Hello World</div>
  )
}
```

I sifted through the JSX docs and figured I'd learn the specifics when I needed to. After that, it wasn't hard following the tutorial. Everything made sense and was super clear. 

I think the most important thing to remember learning new frameworks, libraries, or whatever, is that it's just code. React is just a set of functions and objects written in JavaScript. It's a matter, then, of learning the patterns and paradigms that engineers before me have found to be the best solution for the problems they are facing. In this case, the problem is complex client side code that has a lot to keep track of. 

I don't think this is the best place to start talking about React in depth and I'm still getting into "thinking in React" so I'll kill this post here and gewt back to the topic in a different one. 