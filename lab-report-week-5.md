# Looking at the `grep` command

Suppose we have a group of files that we want to search through, it would be a massive pain to just open all of them and search through these manually.

In this example we have 3 files: animals.txt, fruits.txt, fruitsbutcapslock.txt

We are working with these files, with fruitsbutcapslock.txt being in all uppercase.

![Files.txt](Week5LabScreenShots/files.png)

So lets try to find the word "dogs" in these files and see what comes up: we will use the command `grep "dogs" *` which will go through all the files and find any containing the word dogs.

![dogsfound](Week5LabScreenShots/grepdogs.png)

So we found dogs twice within animals.txt, which is useful to know that there are two references to the string "dogs". We will now be using this on something vastly most massive, which is why we would want to use this in the first place. Here we have a folder downloaded from https://anc.org/data/oanc/download/ that contains a ton of text with various content.

Lets try this on the massive folder of text files!
![direct](Week5LabScreenShots/direct.png)

Uh oh, we found a bunch of directories instead, this is because of how the pattern and grep work. Lets look at the file structure:
```
-technical
-->911report
-->biomed
-->government
-->plos
```

The technical folder only has directories, so the output makes sense since grep can't search a directory. So how do we search all the files in the directories? This is where the `-r` command option comes in, which will recusively search all of the files in the folders and their subdirectories. This makes it very easy to find files. Lets try to find our dogs in the technical folder:

![dogsfound](Week5LabScreenShots/dogsfound.png)

Here we go, we search our current directory recursively, which we can see a biomed subdirectory folder contains the string "dogs" a lot. What happens if we search for the goverment subdirectory recursively for dogs? 

![dogsnotfound](Week5LabScreenShots/dogsnotfound.png)

Well it seems that the government doesn't like dogs, since grep found nothing. This is because we went into a directory that didn't have the biomed as a subdirectory, so we didn't see any of those files that came up. What if we search the entire desktop for fun?

![desktop](Week5LabScreenShots/desktopsearch.png)

We are now again finding the files, since somewhere in our desktop is our biomed folder in a subdirectory. Since the `-r` command goes through everything below the subdirectories and eventually find our file.

Let start changing how we see our output, right now it's very messy and spewing lines of text. What if we only just want the FILES that contain our query instead of printing out all of the lines. The option for us is `-l`, which makes this come true. Lets show an example:

![onlyfiles](Week5LabScreenShots/lcommand.png)

Now the output shows us just the files, which is very handy that means we can control how we use grep and the outputs we get. 

Lets say we want to see if some weird text is in any of these files, a search so impossible to show up that we expect nothing.

![crazysearch](Week5LabScreenShots/impossible.png)

This means that nothing has been found with our crazy text, which makes sense that no file would show up on this. Which means our command still works as expected. Instead, lets see if there are any mentions of cats in these files.

![catsearch](Week5LabScreenShots/cats.png)

With our search for cats there are a couple of files that are different, missing, or new to us now, which helps us figure out which one are exclusive to cats or dogs or contain both.

This is great and all that we have filtered our output, but we did lose a little bit of information. We don't know which files would contain the mention of strings more than others, some files could be more about dogs than the other. This is where the `-c` option can fill in the gaps for us.

![count](Week5LabScreenShots/count.png)

This lets us know how many times each time a file contains "dogs" which lets us know a count instead of an existance. Something really annoying has come up however, a ton of files of course will have no reference to dogs, yet grep is still telling us this. A way to get around this is to instead just pipe input in the files we with grep and use it again for a count of instances: 

![pipes](Week5LabScreenShots/pipes.png)

This looks a lot better, since now all we have is instances where dog is acutally said. If we do this for cats, we can also take a look at how they compare:

![catpipes](Week5LabScreenShots/catpipes.png)

We can now see that dogs get mentioned generally more than cats in these papers, with more files and mentions in those files, with dogs being brought up 59 times. With the `grep` command you can do mass analysis on folders to get ideas on what is contained in them and possible make comparisions.