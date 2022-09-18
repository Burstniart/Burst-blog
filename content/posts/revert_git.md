---
title: "I've made a huge mistake"
date: 2022-09-18
description: 'Life doesn't always give you second chances, GIT does...'
---
# The fastest way to learn is to make mistakes 
****
At least that's what they told me, but they never said sometimes I'd need to fix those mistakes, else I wouldn't be able to continue.
 
As I'm writing this post the blog is decorated by a blue theme for goHugo, which looks nice, but I wanted to change it to something more purple.
So naturally I searched for some themes to switch, found one that I liked and proceeded to do as the repo indicated. Or so I thought...
 
Imagine my face after pushing the changes that were supposed to switch colors in my blog, not only giving me the same colors even after refreshing the cache and checking that Github Actions has successfully deployed my update, but also showing a crooked and yanked version of my site. Things began to get fishy around here.
Rereading the instructions, double checking routes, making sure the files were replaced correctly took me nowhere; *Just one of those times where things are wrong and I was clueless.*
 
I wanted to rollback since I couldn't figure out what was not working with the blog and the themes and luckily I was able to to do because I use Git, and by that I mean I actually use it, not just push my work whenever I want to see any changes; So it was quite easy: check when was the last time the code worked, get that code and replace it.
 
1. Checkin when was the last time the code worked:
 
    Not a very difficult task, just did a good old `git log` and voila! just two commits ahead of a working copy of my project, now what?

        git log

    ![Git log screenshot](/static/images/revert_01.png "Screenshot_revert")

    
1. Get that code:

Here comes the hero

    git revert 
 
This command lets us record new commits to reverse the effects of commits pushed before; Since I didn't mind what happened to the faulty code I simply went with this.
    But there was the detail that I couldn't just reverse to the HEAD of my commits list, this was the case because like the Readme file of this repository says this blog was created by someone else and the way it works is that Github Actions pushes new changes after each push I do, thus putting me two positions away from my ideal scenario, such a chess moment.
 
    git revert HEAD
 
`HEAD` simply had to be replaced with my desired commit from which I simply took the first 6 characters of the string that identifies it and voila!
 
    git revert 4654f37

![Git revert screenchot](/static/images/revert_02.png "Screenshot_revert_2")

 
3. Replace it:
 
Not just push it, we want to force it, we want to take back those mistakes and make things right and we can do it!
 
    git push origin -f
 
This command is telling git to push our changes even if the remote branch is ahead, and that's because we have rolled back in time and now have files without changes that the remote branch does have, or maybe files that existed in the future now don't??? This is getting confusing.
Essentially we have things the way we want them and our branch should hold these ones instead.
 
After running those commands the files that were affected in those commits should be back to their working stages.
 
An important note here is that if you revert a commit that affected one file or set of files your not modifying the entire project project structure, only those files; This is useful to know because if your building a project and have adequately separated features, modules and such you could rollback on them without losing progress on the others.
 
So there you have it! Now we can feel safer knowing how to undo our mistakes. I wish I could do that in real life haha...
 
****
*Intrusive thought of the day:*
*Have to work for food, and I don't even like food that much. Why is food even so expensive? Wish I could live off Pepsi (not sponsored)*.
 
 