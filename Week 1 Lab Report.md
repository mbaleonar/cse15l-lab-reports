## CSE 15L Week 1
#VScode, Remote Connection and Terminal Command tutorial
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

`$ ssh cs15lwi23xx@ieng6.ucsd.edu`

(Keep in mind that is a lowercase "L", as in lab, and not a "1" digit. Also, don't actually put in the `$` symbol, as that is simply a coding convention)

If this is the first time connecting to the server, a message should show up like this in your dialogue box:

`⤇ ssh cs15lwi23xx@ieng6.ucsd.edu
The authenticity of host 'ieng6.ucsd.edu (128.54.70.227)' can't be established.
RSA key fingerprint is SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec.
Are you sure you want to continue connecting (yes/no/[fingerprint])? `

When it comes to connecting to a server for the first time, saying yes to this question is a given and shouldn't come as a surprise. If this message shows up on a server you connect to frequently, however, this could show that someone is trying to listen into or take control of your connection. This is a good answer to what is going on when this message shows up [Ben Voigt’s answer](https://superuser.com/questions/421074/ssh-the-authenticity-of-host-host-cant-be-established/421084#421084).

So go ahead and type 'yes' into terminal, and a prompt to  enter your password will show up. The terminal should look like this:
`# On your client
⤇ ssh cs15lwi23xx@ieng6.ucsd.edu
The authenticity of host 'ieng6-202.ucsd.edu (128.54.70.227)' can't be established.
RSA key fingerprint is SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec.
Are you sure you want to continue connecting (yes/no/[fingerprint])? 
Password:`

Keep in mind that your password input will be censored while being entered for security reasons, so make sure to carefully type it in!

After you (hopefully the first time) successfully entered your password, there terminal should spit this word vomit out:
`# Now on remote server
Last login: Sun Jan  2 14:03:05 2022 from 107-217-10-235.lightspeed.sndgca.sbcglobal.net
quota: No filesystem specified.
Hello cs15lwi23zz, you are currently logged into ieng6-203.ucsd.edu

You are using 0% CPU on this system

Cluster Status 
Hostname     Time    #Users  Load  Averages  
ieng6-201   23:25:01   0  0.08,  0.17,  0.11
ieng6-202   23:25:01   1  0.09,  0.15,  0.11
ieng6-203   23:25:01   1  0.08,  0.15,  0.11

Sun Jan 02, 2022 11:28pm - Prepping cs15lwi23`

When that shows up, that means you're connected to a computer in the CSE basement and subsequently any commands you run on your device will also run on that remote computer! As an added note, *client* refers to your personal computer and the *server* is the remote computer hooked up in the CSE building.

If you ever run into any issues during the process, remember to take a step back and go through every process properly and if all else fails, ask google or ask for help from someone else, especially when working with a group.

## Run Some Commands
Now go ahead and try some commands like `cd`, `ls`, `pwd`, `mkdir` and `cp` on both your personal computer and the remote computer to get a feel of properly inputting commands in terminal.

Try out these commands:
* `cd ~`
* `cd`
* `ls -lat`
* `ls -a`
* `ls <directory>` where `<directory>` is `/home/linux/ieng6/cs15lwi23/cs15lwi23xxx`where `xxx` is your own login info or someone else's
* `cp /home/linux/ieng6/cs15lwi23/public/hello.txt ~/`
* `cat /home/linux/ieng6/cs15lwi23/public/hello.txt`

If you're working with a group, reach out and compare your commands to see if they're working properly. Have fun with it and just mess around to see what happens with the commands.

Last Tip: When you're finished with your `ssh` session, use:

* Ctrl + D
* Run the command `exit`
