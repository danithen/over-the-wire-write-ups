# [Bandit](https://overthewire.org/wargames/bandit/) CTF
### Bandit is a beginner CTF aimed towards absolute beginners. I recommend if you are using this write-up as a guide to do your own research before you copy the solutions. Remeber the goal of CTF's is to learn and have fun. Happy Hunting!
## Brief Overview:
We will be learning a lot about basic linux commands, if you do not have any experience in linux I **HIGHLY** recommend that you read the man page of every command we use. This CTF is can be accessed from any machine, as we are going to ssh into the server. If you want you can use [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html), but the command line will work just fine.
### What is SSH?
Secure Shell Protocol (SSH), is a networking protocol that allows us to securely access and manage network devices and servers. Basically you can login and execute commands on the system without actually having to be there. If you want to learn more you can read this article by [CloudFlare](https://www.cloudflare.com/learning/access-management/what-is-ssh/)
## Lets Get Started:
Bandit provides a lot of relevent info, recommended commands, and resources so make sure to follow along [here](https://overthewire.org/wargames/bandit/).
### Level 0
In order to start we first need to ssh into the CTF, open the command prompt and run: <br> 
######
    ssh bandit0@bandit.labs.overthewire.org -p 2220
Bandit gave the password for this level: `bandit0` <br>
#### As we continue 
### Level 0 -> Level 1
Once I loaded in to the game I ran the `ls` command to look for any useful files or directories. I saw the "readme" file, and did `cat readme` to print the contents to the screen. The output was: `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`. This is the password for the next level.
### Level 1 -> Level 2
Bandit tells us that the password for the next level is stored in the file -. I logged in and ran `ls` to make sure the file was there. - is a special character in linux, you cannot do `cat -` to get the output. We need to use the "<" operator to redirect the input for the "cat" to the "-" file instead of the keyboard. I ran `cat <-` and the output was: `263JGJPfgU6LtdEvgfWU1XP5yac29mFx`. This is our next password.
### Level 2 -> Level 3
Bandit tells us the location of this password is in the file **spaces in this filename**. I logged into and ran `ls` to double check that the file was there. This is a pretty simple level, all we have to do is place the filename in quotes to ensure we read it as one argument. I ran `cat "spaces in this filename"`, our output is: `MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx`
### Level 3 -> Level 4
Bandit tells us this file is hidden in the **inhere** directory. First thing I did was `cd inhere`, this changed our working directory to **inhere**. Next I did `ls -a`, the -a argument displays simply does not ignore files that start with `.`. The output is the file **...Hiding-From-You** along with the . and .. directories. Remember that Bandit told us we are looking for a file so we should do `cat "...Hiding-From-You"` because it is the only file. The output is: `2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ`
### Level 4 -> Level 5
Bandit tells us to look for the only human-readable file. We run `ls` and see about 10 files, we could simply run `file` for each one of these manually but instead we are going to use a simple BASH script to automate the process(for more info on BASH see [here](https://www.geeksforgeeks.org/bash-scripting-introduction-to-bash-and-bash-scripting/)). 
#####
    for x in $(seq 0 9); do file ./-file0$x; done 
The output showed us that we want to look in -file07. We know this because it was the only file that is ASCII, which is human readable text. Running `cat <-file07` gives us our next password: `4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw`
### Level 5 -> Level 6
Bandit tells us that the password for the next level is stored in a file with these attributes: `human-readable` `1033 bytes in size` `not executable`. I ran `ls` as soon as I logged in, then `cd inhere`, then `ls` again. The output shows us 18 directories, far to many to manually find our file. Instead we will use the find command, running `find -readable -size 1033c ! -executable`. We need to use the negations "!" to find non executable files. The output tells us that maybehere07/file02, after runnning `cat maybehere07/file02` we get our next password: `HWasnPhtq9AVKe0dmk45nxy20cvUa6EG`
### Level 6 -> Level 7
Bandit tells us that the file we are searching for is located somewhere in the server, its has the attributes `owned by user bandit 7` `owned by group bandit 6` `33 bytes in size`. This is pretty easy, we will just use find again but with a couple extra things: `find / -user bandit7 -group bandit 6 -size 33c 2>/dev/null`. The output tells us to look at `/var/lib/dpkg/info/bandit7.password` which gives us the next password: `morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj`. <br> <br>
Originally when I ran the find command I did not have the `2>/dev/null` addition, this caused the output to be mostly permission denied errors. I had to do a bit of research to figure out how to redirect the stderror, and eventually landed on the solution. `2` refers to the stderror (`0` and `1`, refers to stdin and stdout respectively) and `>/dev/null` simply redirects the output to `/dev/null`, a special file that discards any data that is written to it.
### Level 7 -> Level 8
### Level 8 -> Level 9
### Level 10 -> Level 11
### Level 11 -> Level 12
### Level 12 -> Level 13
### Level 13 -> Level 14
### Level 14 -> Level 15
### Level 15 -> Level 16
### Level 16 -> Level 17
### Level 17 -> Level 18
### Level 18 -> Level 19
### Level 19 -> Level 20
