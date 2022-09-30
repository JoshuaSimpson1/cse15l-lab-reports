# Lab Report 1: Remote Access and The File System
---
## Installing VS Code
To start working on the file system and acessing the UCSD ieng6 server, you first need visual studio code,
an IDE that will help us use it's terminal for SSH and SCP commands, but also let us edit our Java program
that we will upload to the server.

[Download Visual Studio Code](https://code.visualstudio.com/download)

After you are finished installing VSCode, we can get starting with remoting connecting.

## SSH into ieng6 server
To log into an ssh server the command `ssh [server]` is used. The interaction looks like this:

![Image](https://raw.githubusercontent.com/JoshuaSimpson1/cse15l-lab-reports/main/Week1LabScreenshots/loggingssh.png)

The interaction between server and client starts as `ssh cs15lfa22kk@ieng.ucsd.edu`, which will tell your computer to connect to the server cs15lfa22kk@ieng.ucsd.edu. Since in this example I have conenected to the server for the first time it asks if I wish to continue after seeing it's fingerprint. Since I do, I type yes and the server asks for my password, after putting it in it tells me information about the server such as: when my account was last connected to, if there were failed attempts to log in before, servers available, and other information

## Trying some commands out on the server
Now that we are logged into the server, we can ensure that any commands we execute are actually running on the computer we want.

![CommandsImage](https://raw.githubusercontent.com/JoshuaSimpson1/cse15l-lab-reports/main/Week1LabScreenshots/randomcommands.png)

Here I used two commands `echo` and `whoami`, `echo` will print out what a type after the command, and `whoami` will print out the user currently on the temrinal.
This image shows the echo command printing back what I type, which is a good response, and the whoami command replies back with cs15lfa22kk, which is my user on the server. This means that I am running commands not on my local computer but instead on the server.

## Moving files with the `scp` command
The command `scp` will move files remotely from your computer to the server. This is useful for running programs or moving various files that you need on the server.
![scpimage](https://raw.githubusercontent.com/JoshuaSimpson1/cse15l-lab-reports/main/Week1LabScreenshots/scp.png)

In this I start out on my local machine, compiling the WhereAmI.java and running the program. The output of the java program is that of my local machine showing Windows 10 and my home and root directories.

Using `scp WhereAmI.java cs15lfa22jp@ieng6.ucsd.edu:~/` I will move the file WhereAmI.java to the home directory (~) to the server. When it has completed, I log back into the server with `ssh` and compile and run the same program onto the server machine. The output of this program is different than that of my local machine, instead now showing linux and other directories on the server account. This means the program has ran on the server successfully, and that the output was not from my machine, but instead the server.

## Setting up SSH key
At this point, every login to the server will need a password to be put in. However there is a way to correct this by generating an SSH key and sending it to the server for use.

To do this we need to use ssh-keygen, which will create a public key and private key.

![sshkeygen](https://raw.githubusercontent.com/JoshuaSimpson1/cse15l-lab-reports/main/Week1LabScreenshots/sshkeygen.png)

Here we start the key generation process with ssh-keygen which will ask which file to save this in and for a passphrase, in this image I entered just the default setting. After it generates it shows an image and tells you where it is saved.

Now we need to move this key to the server, so it too has a copy of the key we made. We do this with `scp` but first we need to make a directory too. After logging back into the sever with ssh use the `mkdir` command in the home directory to create the .ssh directory. The command would look like this: `mkdir .ssh`.

Going back to the client we now need to move the key into the directory we just created.

![scpsshkey](https://raw.githubusercontent.com/JoshuaSimpson1/cse15l-lab-reports/main/Week1LabScreenshots/scpsshkey.png)

We have done this before in the lab so, this should be pretty simple by this point.

![nopasswordlogin](https://raw.githubusercontent.com/JoshuaSimpson1/cse15l-lab-reports/main/Week1LabScreenshots/nopasswordlogin.png)

And the next time you log in on the same computer, Viola! You do not need to type your password again, as shown above.

## Making remoting running more pleasant
Since students and programmers alike want to make their lives easier, we would like to reduce the amount of work needed to do things.

In the last step we made a lot of progress on this goal, as we don't need to type in our password every single time we want to login. 

Let say instead of logging in to the server then running the command, we do both at the same time. Lets use our WhereAmI.java file as an example.

![runningmultiplecommands](https://raw.githubusercontent.com/JoshuaSimpson1/cse15l-lab-reports/main/Week1LabScreenshots/runningmultiplecommands.png)

Here, instead of doing everything in multiple steps of logging in then compiling then running java, we do this on login. This is done with `ssh "(commands seperated by semicolon)"` in the example we do `ssh cs15lfa22k@ieng6.ucsd.edu "javac WhereAmI.java; java WhereAmI"`

This saves some time, maybe not much, but if you do this a hundred times in a day it will add up to more and more time saved.