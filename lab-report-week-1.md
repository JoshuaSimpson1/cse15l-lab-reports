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