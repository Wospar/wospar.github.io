---
layout: post
title: bandit documentation
---
[game found here](https://overthewire.org/wargames/bandit/bandit0.html)

ssh bandit[]@bandit.labs.overthewire.org -p 2220

ls to see what files are here
less readme to see the text inside, where we find
ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If - 1

ls to see files, 
then less (or cat ) ./- in order to read the file with a weird name
giving us:
263JGJPfgU6LtdEvgfWU1XP5yac29mFx - 2

ls won't work, so you have to surround the filename in ""
you can then follow the previous steps 
ls "spaces in this filename"
less "spaces in this filename"
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx - 3

cd to change directories to inhere
then use ls -a to show all files and directories
use less .hidden to see
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ - 4

navigate to inhere using cd
then do file ./* to show all files and their format
this shows us one ascii file out of the ten. (-file07) it contains 
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw - 5

for this, i used the du command, specifically du -hab, which filters by bytes and human-readability. then you just look through until you see a file matching the description. in this case, that is maybehere07/.file2
it contains the next password, which is 
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG - 6

this next one requires the use of the find command. we want to filter by size, group and owner. using the -size 33c tag, we can quickly find the file we are looking for, which is bandit7.password
the password is:
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj - 7

this one is pretty simple. we use the grep command to find what we want. 
cat data.txt | grep millionth
this prints us the line with the password on it, the password being
dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc - 8

to find this password, we want to use the uniq command to find the unique line in the file. however, when we use it, it doesnt print correctly. to solve this, we want to sort the file first, in order to filter by occurrence. to so this, we run:
sort data.txt | uniq -u
this gives us the password, which is:
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM - 9

this binary file is reall small so i just looked through it until I found the password. theres probably another way to do this but this requires very little effort.
FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey - 10

for this, we need to decode the base64 data in the file. to do this, we run
base64 -d data.txt
this gives us the password of
dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr - 11


Pass 12: 
we want to run
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
in order to reshuffle the letterds into the desired password
7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4 - 12

Pass 13: 
bandit12@bandit:~$ mktemp -d
/tmp/tmp.[ ]
bandit12@bandit:~$ cd /home/bandit12
bandit12@bandit:~$ cp data.txt /tmp/tmp.[ ]
bandit12@bandit:~$ cd /tmp/tmp.[ ]
bandit12@bandit:~$ mv data.txt newdata
bandit12@bandit:~$ xxd -r new data
Tried tar, gzip, bzip2, xxd. None working yet
Read the file prefixes in order to find out what compression software it uses:
In order:
Xxd -r
Gunzip
Bzip2 -d
Gunzip
Tar -xf
Tar -xf data5.bin
Xxd data6.bin
Bzip2 -d data6.bin
Tar -xf data6.bin.out
Xxd data8.bin
Gunzip data8.gz
FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn - 13


ssh -i sshkey.private -p 2220 bandit14@localhost
Navigate to /etc/bandit_pass/bandit14
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS - 14


I used nmap to make sure I knew the port
Then used NetCat (nc)
nc localhost 30000
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo - 15


Using openssl's s_client command, you connect to the localhost on the correct port (30001), and submit your password
bandit15@bandit:~$ openssl s_client -connect localhost:30001
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
Correct!
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx

closed


kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx - 16
We need to use nmap to find the open ports, so you do
nmap localhost -p 31000-32000
Once we find the ports, we need to see which ones return an ssl key
We run the same command as before to find out
openssl s_client -ign_eof localhost:31790
This command gives us the ssl key for the next level

-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----


In order to get into lvl 17, you have to convert this into a private ssh key. To do this, enter your .ssh folder and make a new file. Insert this text into the file, and connect in the same way you did on level 14. Use ssh -i [filename] and you'll be in no problem
From here, you use diff -qy passwords.new passwords.old, which compares them and prints out whatever line differs, giving us the password of 


x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO - 18
Ssh allows commands to be run immediately during the connection. You can do this by just adding the command to the end of your ssh call
ssh bandit18@bandit.labs.overthewire.org -p 2220 ls 
ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme
This gives us 


cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8 - 19
For this level, our directory contains bandit20-do, which is a binary executable. This helps us because it allows us to access certain files as the user bandit20. This means that we can access the password using their credentials. 
./bandit20-do less /etc/bandit_pass/bandit20
This shows us the contents of bandit_pass as though we are bandit20, and give us the password 


0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO - 20
for this next level, we use the Netcat command
this creates a server on port x that can do whatever we want, in this case broadcast the previous password
to do this, we would do this command:
echo "password" | nc -l -p port#
then we want to connect suconnect to the server using ./suconnect
this gives us the next password, which is 


EeoULMCra2q0dSkYj561DX7s1CpBuOBt - 21
for this level, we need to look into the cronjob folder to see what commands are being run. we see that user 22 is running the file /usr/bin/cronjob_bandit22.sh. this file contains the location our next password, which is /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv. in this file is our password - 


tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q - 22
for this one, we start the same way as last time, but this time instead of a file with the location, there is a script. normally, it is able to tell who you are, but we can fool it by echoing the part that we want. in this case, we want to say "echo I am user bandit23 | md5sum | cut -d ' ' -f 1"
this makes the script think that we are bandit23, meaning it will give us the location where the password is stored.
the string of characters it gives us is the name of a /tmp file. if we cat it, it will give us the password, which in this case is


0Zf11ioIjMVN551jX3CmStKLYqjk54Ga - 23
in the same manner as the previous 2 levels, we look through the cronjob tab to find where the file being run is stored. we find the cronjob_bandit24.sh file, which executes and deletes all files in the /var/spool/$myname/foo directory. for this, we want to run a script that writes out the user password stored in the bandit_pass directory into a user-generated file. we can start by making a temp directory for all our stuff. we want to make a file to store the password, and a script to get the password. the script is very simple, just cat the password into the password file, like this:
#!/bin/bash  
cat /etc/bandit_pass/bandit24 > /tmp/tmp.[#]/password  
after a short delay, that gives us the next password


gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 - 24
for this level, we start off by making another temp folder. from here, we want to write a script that can concatenate the previous password + a 4 digit pin. that script looks like this: 
#!/bin/bash

for x in {0000..9999}
do  
        echo gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 $i >> combinations.txt  
done  

then, we just need to output all of those into the daemon but using netcat. 
cat combinations.txt | nc localhost 30002 > answers.txt

then, we can use the uniq command on asnwers .txt to find what lines contain the password, this gives us an output of 
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
Wrong! Please enter the correct current password and pincode. Try again.
Correct!
The password of user bandit25 is 


iCi86ttT4KSNe1armKiwbQNmB3YJP3q4 - 25
this one is pretty rough. we need to find out what shell the user bandit26 was using and how it works, as well as break out of it in order to get the password. to start, we need to figure out what shell they were using. we can find this by looking through /etc/passwd to find what shell bandit26 has been using. this presents us with a directory: /usr/bin/showtext. displaying the file gives us a bash script: #!/bin/sh

export TERM=linux

exec more ~/text.txt
exit 0
this leads us to the file text.txt, which will be useful later
the solution to log into bandit26 is a bit odd, and i was really confused until I looked it up. basically, if you resize your terminal window to the smallest size, you can break the code running the text diplay, and then open vim. vim allows you to run bash commands without needing to enter the bash shell. from here, you want to set the default shell to bash (:set shell=/bin/bash) then change the shell to default (:shell). from here, you can navigate as normal to access the password file.


s0773xxkk0MXfdqOfPRVr9L3jJBUOgCZ - 27
this level is time sensitive, so make sure to do this quickly, or restart from 26. it's the same command as level 19, basically just a memory test.


upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB - 28
this level requires you to clone a git repository. to start, create a temp directory to stor the files, then run 
git clone ssh://bandit27-git@localhost:2220/home/bandit27-git/repo
this creates the git repository in your local directory, as well as load it from port 2220. inside the git repository is a README file containing our next password


Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN - 29
this level starts off the same way as the previous, but this time we need to know how to look through the commit history. to do this, we need to use the git log command, which shows us all previous commits, as well as what their numbers are. once we know this, we can change branches with the git checkout command, then use the git show command in order to see what has been changed. when we do git show 3621de89d8eac9d3b64302bfb2dc67e9a566decd, we can see that the password is 


4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7 - 29
this level starts in the same way as the previous two, but this time we need to use the branches feature of a git repository in order to find the password. by using the git branch -a command, we can see all of the branches in this particualr repository. the one that we are interested in is the dev branch, since it seems most likely to have a password in it. when we look, we see that there are more commits here than there were in the master branch. when we look at the most recent one, we see that it contains the password for our next level. 


qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL - 30
this time, the password is hidden in a git tag. in order to show tafs, use the git tag command. then, we use the git show command to show the content of the tags. in this case, the tag is labeled "secret". using the git show command give us the password to the next level


fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy - 31
the next challenge involves pushing a file to a remote repo. we want to start the same way as before, with a tmp directory. then, we want to create the file that it wants us to
echo 'May I come in?' > key.txt
we want to push this change live, but we are being filtered by gitignore. to get around this, use the add -f command. then, we can commit those changes. finally, we use git push origin master to give us our final answer


3O9RfhqyAlVBEZpVb6LYStshZoqoSx5K - 32
this time, we are stuck in an all uppercase shell. in order to get back to the normal shell, we need to use the variable $0. once we do this, we are able to use commands normally again. from here, if we use whoami, we can see that we are logged into bandit 33, and can directly read the password. 


tQdtbs5D5i2vJwkO8mEyYEyTL8izoeJ0 - 33
thats all there is to it
