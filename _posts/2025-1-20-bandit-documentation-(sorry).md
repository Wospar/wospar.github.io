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
