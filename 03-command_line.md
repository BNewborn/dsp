# Learn command line

Please follow and complete the free online [Bash Scripting Tutorial](https://ryanstutorials.net/bash-scripting-tutorial/) or [Codecademy's Learn the Command Line](https://www.codecademy.com/learn/learn-the-command-line). These are helpful tutorials. You should be able to go through these in a couple of hours.

**Note:** Bash is not installed on a PC. Rather, PC users must install Cygwin. Once Cygwin has been installed, the command line interface witll _emulate_ bash. You can find all information regarding Cygwin [here](https://www.cygwin.com/).

---

### Q1.  Cheat Sheet of Commands  
Make a cheat sheet for yourself: a list of at least **ten** commands and what they do.  (Use the 8 items given and add a couple of your own.)  

Here's a list of items with which you should be familiar: 

Request | Bash Command
--------|---------------
show current working directory path | pwd
creating a directory | mkdir directory_name
deleting a directory | rm -r directory
creating a file using `touch` command | touch file1 file2 file3  touch -am changes modified and accessed times
deleting a file | rm filename.txt
renaming a file | mv OLDPATH_NAME NEWPATH_NAME
listing hidden files | ls -a (directory-optional)
copying a file from one directory to another | cp FILE DESTINATION_FILE or DIRECTORY or cp FILE1 FILE2 FILE3 DESTINATION
*renaming a directory* | rm OLDDIRECTORY NEWDIRECTORY
*Operators* | -eq **equals** -gt **greater than** -lt **less than** also -le and -ge.
*File or Directory?* | -d file/directory **returns true for directory** -f **returns true for file**
*Pull Random Word of Input Length* | num_chars=$1 rand_word2=$(egrep "^[A-Za-z]{$num_chars,$num_chars}$" /usr/share/dict/words | sort -R | head -1) **egrep lesson**
*for, while, until loops* | for name in $names do xyz ,  while [$counter -le 10] do xyz ((counter++)) , until [$counter -eq 10] do xyz ((counter++))
*select* | brings up menu for user interface in bash. select name in $names - build if statement thereafter
http://www.linfo.org/touch.html



---

### Q2.  List Files in Unix   
https://ss64.com/bash/ls.html

Request | Description
--------|---------------
ls  |  lists files in input or default directory
ls -a  | lists all files (including hidden)
ls -l  | Use a long listing format (shows permissions, last modified time, owner, name etc.)
ls -lh | h tells bash to print file size in a readable format. Takes -l and makes it easier to use
ls -lah| Includes benefits of -lh but also includes all hidden files
ls -t  | sory by modified time
ls -Glp| G = color codes entries, l= long listing, p=append indicator (/=@) to entries (directories get slash)

---

### Q3.  More List Files in Unix  

Explore these other [ls options](http://www.techonthenet.com/unix/basic/ls.php) and pick 5 of your favorites:

Request | Description
--------|---------------
ls -m |  lists files as comma separated list
ls -1  | lists all items as separate line (easier to read)
ls -GF | Flags file names (gives them a star) G=color codes files vs directories
ls -lhGS | color coded, easy size to read, sorted by size

---

### Q4.  Xargs   

What does `xargs` do? Give an example of how to use it.
`xargs` allows you to string commands together to have argument lists executed with utility (trying to combine definitions from a few websites)
in terminal, type man xargs to see all documentation

*Example*
#trying to find all .sh files in /users/brian\_newborn/ and move them to archive folder
<br />
`mkdir /users/brian\_newborn/script\_archive`
<br />
#creates directory
<br />
`find /users/brian\_newborn -maxdepth 1 -name "\*.sh" | xargs -I {} mv {} /users/brian\_newborn/scrpt\_archive`
 

