---
layout: post
title:  "Bash Functions for Creating Jekyll Posts"
date:   2016-10-23 12:00:)) -0400
categories: bash, software engineering, automation
---

As I have decided to proceed with Jekyll atop Github Pages for my blog, I wanted a quick way to create posts. In Jekyll, the file structure include a directory called _posts. Creating a post is as simple as creating a file in the _posts directory in the following format: YYYY-MM-DD-title.md

As such, an example title could be: 2000-1-1-we-are-still-alive.md

The idea is that one command should create the file in the directoy in the appropriate format given a title. So, at it's most basic level, given "we-are-still-alive", the bash script should create the needed file.

I started with the following: 

```
# Go to blog
alias gtb="cd /Users/mac/Workspace/static_blog/myblog"
# New Blog Post
alias nbp="_post=$1 && _now=$(date +"%Y-%m-%d") && gtb && touch _posts/$_now-$_post.md"
```

This wasn't working when i ran `nbp we-are-still-alive`.

It took far longer than I'd care to admit to realize that aliases essentially just replace text with other text. That meant I wasn't passing in an argument to the commands in nbp like I thought I could, I was essentially doing: 

```
_post=$1 && _now=$(date +"%Y-%m-%d") && gtb && touch _posts/$_now-$_post.md nbp we-are-still-alive
```

What I needed was a function to pass the argument into. The alias then would reference that function. I came to: 

```
alias onbp="__nbp() { _post=$1; _now=$(date +"%Y-%m-%d"); _filename=$_now-$_post; gtb; touch _posts/$_filename.md; };__nbp"
```

This wasn't working either. It was baffling at first because copy/pasting this directly into the console worked just fine! I fumbled around some more and then finally found [this post on StackOverflow](http://unix.stackexchange.com/a/180708/196618). I had figured that it was something to do with how aliases were being parsed, but I did not realize that the function was inaccessible to the command ultimately. The explanation is put rather succintly in bash documentation, is quoted in the SO answer, and I'll include it here: 

>Bash always reads at least one complete line of input before executing any of the com‐ mands on that line. Aliases are expanded when a command is read, not when it is executed. Therefore, an alias definition appearing on the same line as another command does not take effect until the next line of input is read. The commands following the alias definition on that line are not affected by the new alias.

Cool beans. Fair enough. Alright. Here's my new alias/function combo:

```
  alias gtb="cd /Users/mac/Workspace/static_blog/lewaabahmad"
  function __nbp() { _post=$1; _now=$(date +"%Y-%m-%d"); _filename=$_now-$_post; gtb; touch _posts/$_filename.md; }
  alias nbp="__nbp"
```

Great! Now I have a working function and alias! I realize though, that there are a number of ways this command could be made more useful. For example, it should create the YAML on the top of the markdown document (how Jekyll stores information about the post or page as it is serving static .md files) automatically and I shouldn't need to enter the dashes between the words. It'd take more time than I'm willing to put in though to get evertyhing just perfect. Figuring that someone had to have had this problem and stumbled upon [Jekyll Compose](https://github.com/jekyll/jekyll-compose). Definitely seems promising! 

tl;dr
1 - Aliases are just a way to replace a string in a bash command with another string. 
2 - Declerations need to be made before the alias in order to be availible to the alias command. 