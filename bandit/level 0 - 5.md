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





