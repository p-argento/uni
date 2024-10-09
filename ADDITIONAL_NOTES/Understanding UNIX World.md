Personal Notes on Unix-related stuff
# Linux (and MacOS) Directories
https://www.youtube.com/watch?v=42iQKuQodW4

![[Pasted image 20240203114110.png]]

- `/` (root)
	- use `cd /` to access the root
	- because the starting point in the terminal is actually `/Users/pietro`
- `/BIN` contains Binaries
	- which are essential executables for the OS
	- the command `ls` is here for example
	- also `python3` command is here
		- but the one i am using is in the lib
- `/SBIN` contains System Binaries
	- which should be executed only by the super user (sudo?)
	- like mount or delete user
- `/LIB` contains Libraries
	- shared code between binaries
	- for example the Framework folder with the python version
		- it contains the actual python3 bin used
- `/USR` is the user
	- `USR/BIN`
		- with non-essential binaries installed
		- intended for end user
	- `USR/LOCAL/BIN` 
		- common location for user-installed binaries, often contains executables installed by software that you've manually installed
		- provide a safe place that won't conflict with any software installed by a system package manager
		- they are safe to delete, it is only third-party software
- `$PATH`
	- tell the terminal where to find executables
	- it is an environment variable that contains binaries that can be executed from any folder in the terminal
		- they are basically column separated paths
	- the order of binaries paths in the PATH variable is relevant if there are bins with the same name, for example different versions of python
		- for example in my mac running the bin  `python3` look for bin in lib/frameworks or in usr/bin.
	- run `which <bin_name>` to see the full path of a bin in PATH
	- remember that you can always run a program with the full path, using `usr/bin/python3 or `cd /usr/bin` and then `./`
- `ETC`
	- meaning Editable Text Configuration (or ETCetera)
	- to customize the behaviour of the software on your system
	- many of these files are `.conf`, meaning just text based configuration files that can be modified in an editor (like vim)
- `/HOME`
	- here we found the multiple users using the os
		- each one with its own subfolder
	- on macos, i think it's called `Users` , my folder is in fact `/Users/pietro`
		- it is the starting point when opening the terminal
		- can be accessed also using the shortcut `cd ~`
- `/BOOT`
	- contains files to boot the system itself, like the kernel
- `/DEV`
	- meaning Devices
	- to interact with connected devices as they where regular files
	- for example here you can create partitions
- `/OPT`
	- add-on software
	- you rarely interact with it
	- it is where homebrew download softwares in apple silicon
		- specifically in `opt/homebrew/Cellar`
- `/VAR`
	- meaning Variable files
	- things that change as the OS is being used
	- they are files like logs and cache files
- `/TMP`
	- meaning Temporary files
	- they will not persist between reboots
- `/PROC`
	- illusionary file system that doesn't exist on the disk
	- created on the fly by linux kernel to keep track of running processes

In MacOS root, I see
1. Applications
2. Library
3. System
4. Users
5. Volumes
6. bin
7. cores
8. dev
9. etc
10. home
11. opt
12. private
13. sbin
14. tmp
15. usr
16. var


Linux Directories Explained in 100 Seconds - YouTube
https://www.youtube.com/watch?v=42iQKuQodW4

**Transcript**:

The linux file system it's a cryptic labyrinth of directories defined by the file system hierarchy standard. Navigate through it with the change directory *command cd* forward slash drops you into the root. Then with the *ls command* we can list out the contents of this directory.

First we have the *bin directory* which contains binaries or executables that are essential to the entire operating system. You can run these binaries from the command line at any time things like gzip curl and even the ls command that we just ran. 

But confusingly there's also an *sbin directory* it contains system binaries that should only be executed by the root user, like mount or delete user. 

Many of these binaries may share common libraries which are stored in the *lib directory*.

Now we also have a *usr directory* with its own bin and s-bin directories. The binaries or applications here are non-essential to the operating system itself and intended for the end user. You'll also notice a *local directory under user* it contains any binaries that you compile manually to provide a safe place that won't conflict with any software installed by a system package manager.

All these binaries get mapped together with the *path environment variable* and that's why you can execute them from any directory in the terminal. If you ever want to know where a binary lives run *which* followed by the binary name to view its full path in the file system.

Now at some point you may want to customize the behavior of the software on your system the *etc directory* stands for etc (or editable text configuration) many of these files end in conf and they're typically just text-based config files that you can modify in your editor as an operating system.

Linux can support multiple users in the *home directory*. You'll find a folder named after each user registered on the system it contains the files configuration and software for that user and you need to be logged in as that user or as a root user to modify it. Notice how the file path is a squiggly, that's your normal starting location when you open up a terminal session.

Now let's go back to the root there are a few more directories here that we haven't talked about yet like *boot* . It contains the files needed to boot the system like the linux kernel itself

Then we have *dev* which stands for device files, here you can interface with hardware or drivers as if they were regular files. You might create disk partitions here or interface with your floppy drive

The *opt directory* contains optional or add-on software and you'll rarely interact with it.

*var directory* contains variable files that will change as the operating system is being used things like logs and cache files temp, is for temporary files that won't be persisted between reboots.

And finally we have the weirdest one of all, the *proc directory* is an illusionary file system that doesn't actually exist on the disk, but is created in memory on the fly by the linux kernel to keep track of running processes this has been the linux file system.

# File Permissions

	•	Numerical (Octal) Notation:
	•	Each digit represents a combination of read (4), write (2), and execute (1) permissions.
	•	The three digits represent the owner, group, and others, respectively.

```
chmod -R 755 /path/to/directory
```

Breakdown of Permissions:

	•	4 (r): Read
	•	2 (w): Write
	•	1 (x): Execute

Combine these values to set the desired permissions:

	•	7 (rwx): 4 + 2 + 1
	•	6 (rw-): 4 + 2
	•	5 (r-x): 4 + 1
	•	4 (r–): 4
	•	3 (-wx): 2 + 1
	•	2 (-w-): 2
	•	1 (–x): 1
	•	0 (—): 0


# Bash (and zsh)
https://www.youtube.com/watch?v=I4EWvMFj37g





Bash in 100 Seconds - YouTube
https://www.youtube.com/watch?v=I4EWvMFj37g

Transcript:
(00:00) bash a command language interpreter for interacting with a computer from the command line it's also called a shell because it surrounds the operating system kernel to hide its intricate details while allowing you the programmer to do important stuff like access data and write files by typing simple commands this was a revolutionary concept when it was developed in the early 70s back when programmers were still using punch cards the shell concept evolved over the years with the bourne shell being the most popular
(00:27) version that is until 1989 when the born-again shell or bash came about when you open up the terminal on a unix machine like mac os and most linux distros the default shell is usually bash it provides a prompt where you can type a command which will then be interpreted by the shell and executed on the operating system to find out if you're running bash type in which dollar sign shell from the command line it's like any other application that lives in the binaries directory but bash is also a programming language that allows us to
(00:55) write scripts which means anything we type manually into the command line can be automated with code when you first launch the shell it actually runs a startup script that's defined in the bash profile or bashrc file on your system this allows you to customize the behavior and appearance of the shell whenever you start a new session you can add your own custom bash scripts to any project by creating a file that ends in dot sh for no file extension at all the first line in that file should always be a shebang followed by the path to the
(01:23) application that should run it below that we can start writing commands like echo to print something and they'll be interpreted line by line to create a variable type a name in all caps followed by the equal sign then reference it later in the script using a dollar sign in front of the name now to execute the script simply type the file name into the shell that was easy but what if we want to pass in some arguments when we run the script positional arguments will automatically be assigned variable names of 1 2 3 and
(01:50) so on now in other cases you may need additional user input in the middle of a script you can create loops in bash like a do while loop here that will prompt the user to continue the script on a yes answer or exit on a no answer from there we can implement conditional logic with an if statement which will test if the value on the left side is less than the value on the right side if true then run this command otherwise run the else command another cool feature is that if you have multiple long running processes
(02:17) you can run them in parallel in the background by adding an ampersand after the command this has been bash the born-again shell in 100 seconds if you want to see more short videos like this make sure to hit the like button and subscribe thanks for watching and i will see you in the next one



## Interesting things on ZSH and PATH variable
https://mac.install.guide/terminal/path





