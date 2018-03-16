---
layout: post
title: Pycharm / IntelliJ on i3wm - the annoying problem with popup dialogs
---

If you run IntelliJ och Pycharm on the i3wm Window Manager in Linux, the popup dialogs have
an annoying tendency to get closed before you have a chance to actually open the file. They 
close as soon as there's even the most minuscule mouse event, even as small as 
the mouse trembling a bit due to you typing on the keyboard. 

Same thing with the symbol lookup window. You will have to move the mouse into the popup
window before you start typing for it to work.

There's an article [here](https://faq.i3wm.org/question/4071/modal-pop-up-in-idea-loses-focus-while-entering-text.1.html),
which I've seen before. I think I've tried the solutions too, but without success. However,
today it worked! It may be that now the combination of i3wm version and PyCharm/IntelliJ works
better again.

Anyways, two options I've tried which both work are:

* Turn off mouse_follows_mouse in i3wm. You can do this by editing `~/.config/i3/config`,
  adding a line:
  
      focus_follows_mouse no
     
  This of course makes focus not follow mouse in i3wm. This may or may not be desired.
  
* The other option is to modify idea.properties. At first, I tried modifying the 
  file in my snap installation of Pycharm under `/snap/pycharm-community/51/bin`, but
  since it's a snap, it's not possible to modify it. At least not from what I understand.
  
  However, turns out there's a menu option under Help, `"Edit Custom Properties"`. So just
  go in there and add a line:
  
      idea.popup.weight=medium
      
  ..and it actually works! 
  
Wow. If this works on IntelliJ at work as well I'm going to be very happy. This is one 
of those really small details that really matter when you work with programming.  
