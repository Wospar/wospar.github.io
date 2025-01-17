---
layout: post
title: Command documentation
---

Scenario: we have been locked out of our machine, and need to find the password in order to regain access.

Start
Our first task was to figure out the IP address of the machine we were trying to hack into. 
1.  To do this, we used the command Nmap to find a list of all the IP addresses currently on the network
2. We started off by asking what our classmates’ computer IP addresses were and found that they all began with 10.0, the third octet was in the range 140-255, and the 4th octet was between 0-255. We only figured this out after trying numerous other nmap switches.
Command: Sudo nmap -O 10.0.140-255.0-255
3. Once we had all the IP addresses we began a process of elimination. We started filtering down the IP addresses that we knew. Until we were left with only the 3 machines that were not currently logged in. 
4. From there we began powering down machines and seeing which ones would not ping. We were able to establish that our IP address was 10.0.140.9.
Machine IP: 10.0.140.9
In order to log in to the target machine, we tried several methods:
1. Attempted to install ssh keys onto the target machine
Commands:  
ssh-keygen  
ssh-copy-id cseh-6@10.0.140.9  
2. When the SSH key attempt proved unusable, we tried using a tool called Hydra to crack the password. The teacher gave us a hint that the password was contained in the file rockyou.txt on his computer. Installing Hydra and getting rockyou.txt proved cumbersome on the machines we had available, but Corey’s machine had both on them. We ssh’d onto his machine and did the following
Commands:  
* ssh cseh-0@10.0.140.3 (access to teacher/admin computer)
* password: security0
* find -name rockyou.txt
* hydra -l cseh-6 -P (path to rockyou) -t 6 ssh://10.0.140.9 (target IP)
~~~~
hydra will brute force passwords using a given input file, in this case 'rockyou.txt', which contained a list of passwords to guess
~~~~
running hydra told us that the password was "qwerty"  
  
Exercise complete!
