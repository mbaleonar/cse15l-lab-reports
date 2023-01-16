## CSE 15L Week 1
# Week 1: CSE 15L VScode, Remote Connection and Terminal Command tutorial
---

## Visual Studio Code Installation
(If you have VScode already installed, just kindly ignore this section and go onto the next step for remote connection)
First off, go to the Visual Studio Code website at (https://code.visualstudio.com/) and (at least in the Lord's year of 2023), the download link should be right in the middle of your webpage on a button colored with a stunning navy blue hue.
![image](https://user-images.githubusercontent.com/122484639/211910251-0bf495fe-182e-4448-8e0e-ff1bea9e5963.png)
If your operating system is anything other than Windows, there is a dropdown arrow to the right of the icon where you can select a macOS (for Macs) or Linux installation. (Unless you know you need it, keep with the Stable build of VScode).

After going through the install progress, you should be able to get to a window with this layout (The default settings may very depending on any settings you mess around or any default system settings):
![image](https://user-images.githubusercontent.com/122484639/211909188-ddf3f875-434d-408c-b34f-b2127cfd4197.png)

**Reminder**: If for some reason your install does not go through properly, idk, like, look it up on google or smth.

## Finding Your Course Account and You

Head over to this webpage to look up your course-specific account:

https://sdacs.ucsd.edu/~icc/index.php

Once you submit your username and Student ID number, the course account should be right underneath the welcome message under *Additional Accounts*.

If you need help resetting your password or are looking for a more visual guide, go to this link: [[TUTORIAL] How to Reset your Password](https://docs.google.com/document/d/1hs7CyQeh-MdUfM9uv99i8tqfneos6Y8bDU0uhn1wqho/edit).

There's a lot of steps and parts to this, so make sure to follow every little instruction down to the T.

The password reset process takes a while, so give it a few minutes while you finish these two other parts to get you connected.

## Remote Connection
Courses in CSE utilize course-specific accounts for posterity, and other jobs in the field also similarly setup like in this tutorial. We'll use VScode's terminal function to remotely connect to a computer over the internet to do our work.

First off, for Windows users, install `git` for Windows, which will be necessary for our remote connection:

[Git for Windows](https://gitforwindows.org/)

*There's going to be a LOT of dialogue boxes but just stick to the default settings and mash through the *next* button on the bottom right. (Unless there is a specific function stated by your employer or professor)*

After that's installed, follow this tutorial to get `git bash` working on Visual Studio Code's terminal.

[Using Bash on Windows in VScode](https://stackoverflow.com/a/50527994)

Now with the necessary preparations out of the way, that should be enough time for your password to be reset if you did so, and to move onwards with the rest of the tutorial.

Head over to VisualStudioCode and create a Terminal session (On Windows that's Ctrl + \` and on Mac that is Cmd + \`) and copy this command. Your own command will look similar, but replace the `xx` with your own personal code.

`$ ssh cs15lwi23zz@ieng6.ucsd.edu`


