# UNIX cheatsheet


## su - vs su

- Summary

	You cannot login to any account without a password, except as a root.
	So the trick is to do sudo, to login to root, as a root.  :)  
 
	$ sudo su -


- Summary :

Use `su -`

	$ su -   # switch user, invoke login shell


<http://unix.stackexchange.com/questions/7013/why-do-we-use-su-and-not-just-su>

`su -` invokes a login shell after switching the user. 
A login shell resets most environment variables, providing a clean base.

`su` just switches the user, providing a normal shell with an environment nearly the same as with the old user.



## find | grep


    $ find . -name "*.txt" | grep word                # search for a file name 
    $ find . -name "*.txt" | xargs grep -l word -s    # search for word within file names; -l just list names of matching files containing word
    $ find . -name "*.txt" | xargs grep word -s       # search for word within file names, -s suppresses error messages

Use `grep -s` to suppress grep error messages


## How to create large files (whose content is irrelevant)

    $ dd if=/dev/zero of=file.txt bs=10485760 count=100
    $ truncate -s 1G derp 

