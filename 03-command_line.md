# Learn command line

Please follow and complete the free online [Bash Scripting Tutorial](https://ryanstutorials.net/bash-scripting-tutorial/) or [Codecademy's Learn the Command Line](https://www.codecademy.com/learn/learn-the-command-line). These are helpful tutorials. You should be able to go through these in a couple of hours.

**Note:** Bash is not installed on a PC. Rather, PC users must install Cygwin. Once Cygwin has been installed, the command line interface witll _emulate_ bash. You can find all information regarding Cygwin [here](https://www.cygwin.com/).

---

### Q1.  Cheat Sheet of Commands  

Here's a list of items with which you should be familiar:  
* show current working directory path
* creating a directory
* deleting a directory
* creating a file using `touch` command
* deleting a file
* renaming a file
* listing hidden files
* copying a file from one directory to another

Make a cheat sheet for yourself: a list of at least **ten** commands and what they do.  (Use the 8 items above and add a couple of your own.)  

* show current working directory path: pwd
* creating a directory: mkdir
* deleting a directory: rmdir
* creating a file using `touch` command: touch 
* deleting a file: rm
* renaming a file: mv
* listing hidden files: ls -a
* copying a file from one directory to another: cp
* locate a file: locate 
* display contents of a file: cat

---

### Q2.  List Files in Unix   

What do the following commands do:  
`ls`  : list files in directory that are not hidden
`ls -a`  :list all files in directory (includes hidden as well)
`ls -l`  :list files in directory that are not hidden in long format (properties, owner, group, size, and time)
`ls -lh` : llist files in directory that are not hidden in long format with readable file size format 
`ls -lah` : list all files in directory (includes hidden as well) in long format with readable file size format 
`ls -t`  : list files in directory that are not hidden in the order it was modified
`ls -Glp`  list files in directory that are not hidden in long format without owner and adds a '\' for directories and 

---

### Q3.  More List Files in Unix  

Explore these other [ls options](http://www.techonthenet.com/unix/basic/ls.php) and pick 5 of your favorites:

ls -laR: list all files including hidden ones with the contents of the subdirectories
ls -lat: list all files including hidden ones by time stamp
ls -ld: list only directories
ls -lau : list all files including hidden ones by the last time they were accessed
ls -1: list directories one line line per entry

---

### Q4.  Xargs   

What does `xargs` do? Give an example of how to use it.

Xarg allows you to pipe the data you have called out to perform additional operations
 

