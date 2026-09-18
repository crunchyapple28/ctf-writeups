Hello! 🍏 

I was introduced to OverTheWire by my professor and we started the challenges in class, however I intend to complete them on my own as I find that they're very informative and fun! 
The first 5 levels are simple exercises in navigating through the terminal and if you follow the instructions provided by OverTheWire you shouldn't have any problems solving them.

## Bandit Level 0 + 0 → Level 1

Level Goal

The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.
The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

`` $ ssh bandit0@bandit.labs.overthewire.org -p 2220``

$ is a shell prompt, don't type it. 
SSH is a secure shell. It's a protocol for securely connecting to and interacting with another computer over a network.
When you SSH into a machine, you essentially get a remote shell. When prompted, type in the provided password, bandit0, which allows you to log in as user bandit0 and play!
`` -p 2220 `` 
is the specific port we're connecting to.
Make sure to separate bandit0 from the url with a @, and once you get the password don't forget to ``exit`` so you can connect to the next port! This is important because we start each session as an authenticated user, in this case bandit0, so it works as a security tool. 
The password from this level is in the home directory, which we can see by using the command ``ls``. ls lists the files in the current directory. A readme file will pop up, and by using ``cat``, we'll be provided the flag.

<img width="567" height="189" alt="Screenshot 2026-09-18 at 10 51 48" src="https://github.com/user-attachments/assets/b97873e7-d4ee-4168-a87b-d5578fae6442" />


## Bandit Level 1 → Level 2


Level Goal

The password for the next level is stored in a file called - located in the home directory

This time, we log in as user bandit 1 with the password provided from the last level. I recommend storing the passwords somewhere so you don't have to redo the levels every time (or just look them up lol)

``$ ssh bandit1@bandit.labs.overthewire.org -p 2220``

Once logged in, using ``ls`` to view the files will let us see a - file. The way to read dashed file names is by using ``cat ./-``, this will give you the contents of the file. The issue with dashed filenames is that the command line uses a dash to specify options (like rm -r or cat -n), so commands will mistake your filename for a broken command argument, throwing errors like invalid option. 
By providing it with ./ , we're specifying that we're looking for - within our current directory. ``.`` is the directory we're currently in, and ``..`` the parent directory, so if you want to backtrack out of a directory you can simply 
`` cd .. `` and you'll be out. 

<img width="567" height="109" alt="Screenshot 2026-09-18 at 11 04 43" src="https://github.com/user-attachments/assets/3626203c-f511-4a91-b0a2-8382da30447d" />

## Bandit Level 2 → Level 3


Level Goal

The password for the next level is stored in a file called --spaces in this filename-- located in the home directory

Spaces cause issues because we use spaces to separate commands from their arguments in the command line, so the system treats every word as a separate file or command. To bypass this issue, we can simply encase the file name in quotation marks, so 

```
ls

--spaces in this filename--

cat "--spaces in this filename--"
```

However, in this case, another problem arises. Since the filename starts with ``--`` it's interpreted as an option and not as the file name:

<img width="568" height="131" alt="Screenshot 2026-09-18 at 12 21 44" src="https://github.com/user-attachments/assets/a6f462f2-cb1f-4214-97ba-b8cff11a2118" />

To overcome this, we need to do ``cat -- "--spaces in this filename--" ``. The quotations help us overcome the space problem, and the ``--`` tell ``cat`` that everything that comes after that is an argument and not an option. Note that it's two dashes, not one (which you can see by my many trials and errors as I tried to remember this) and that there has to be space between them and the quotation marks, otherwise ``--"--spaces in this filename--"`` will be interpreted as one argument. An argument is simply information we give to a command that we want it to operate on. 

After doing that we get the password for the next level.

<img width="568" height="322" alt="Screenshot 2026-09-18 at 12 18 54" src="https://github.com/user-attachments/assets/eb08fc2f-ac0b-435a-af53-feec631d86d0" />

## Bandit Level 3 → Level 4


Level Goal

The password for the next level is stored in a hidden file in the inhere directory.

Here we learn the `` -la `` function. ``ls`` tells the shell to list out all the contents of the current directory we're in, while the added ``-la`` gives ``ls`` two options, ``l`` for long format, so instead of something like 

```
notes.txt
photo.jpg
secret.txt
```
we get 

```
-rw-r--r--  1  user  staff  1033  Sep 18 12:30  notes.txt
-rw-r--r--  1  user  staff  48291 Sep 17 18:42  photo.jpg
-rw-------  1  user  staff   250  Sep 18 11:05  secret.txt
```
``a`` asks it to list out the hidden files as well, so you could technically do just ``ls -a``, but ``-la`` gives us more information about the files.

<img width="324" height="29" alt="Screenshot 2026-09-18 at 13 06 13" src="https://github.com/user-attachments/assets/d835ddaf-0fa5-4bca-ab59-08eaadca7366" />

Make sure you don't mistake the three dots as a directory, only ``.`` (current) and ``..`` (parent) are directories, the three dots are a part of the filename. So, by going into the **inhere** directory and executing the command above, we get the password for the next level.


<img width="568" height="157" alt="Screenshot 2026-09-18 at 12 55 23" src="https://github.com/user-attachments/assets/fdbf2b9e-9ee3-48c5-a97f-1a21cf87f938" />

## Bandit Level 4 → Level 5


Level Goal

The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

Here we're learning how to combine commands. Within the **inhere** directory we have 10 files, and while you could check them all manually, the point of the challenges is to teach you how to navigate around the terminal 

``find . -type f -exec file {} +``

-``find .`` searching only the current directory
-``type -f`` look for files only
-``-exec file {} +`` execute the file command on all the results returned by find

Running this will give us the file our password is stored in.

<img width="566" height="207" alt="Screenshot 2026-09-18 at 13 14 58" src="https://github.com/user-attachments/assets/27d186d9-358b-4a5c-8848-698cd7757144" />

## Bandit Level 5 → Level 6


Level Goal

The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

human-readable
1033 bytes in size
not executable

Here we're doing essentially the same thing as last time, but with a few more commands. Going into the **inhere** directory, we find 20 directories.

<img width="571" height="116" alt="Screenshot 2026-09-18 at 13 27 57" src="https://github.com/user-attachments/assets/d1334c99-ac67-4483-b20c-59175c3f631c" />


Instead of going through them one by one we can parse through them with

``find . -type f -size 1033c -not -executable -exec file {} + | grep ASCII``

here,
-``.`` search the current working directory only
-``-type f`` look for files only
-``-size 1033c`` look for files that are exactly 1033 bytes in size, c representing bytes
-``-not -executable`` find only non executable files
-``-exec file {} +`` execute the file command on all the results returned by find

Running this tells us the directory in which our file is and what file it is.

<img width="569" height="295" alt="Screenshot 2026-09-18 at 13 30 42" src="https://github.com/user-attachments/assets/3aa1e4f8-391a-44d8-8fe3-355a3ba771ad" />

Note that the ``.file2`` file is hidden, as it didn't appear when we first listed all the contents of the directory. Using ``cat ./.file2``, alternatively ``cat ".file2" we get the password.

Hope this helpes! The OverTheWire website is extremely useful for finding hits or solutions if you get stuck so make use of it!











