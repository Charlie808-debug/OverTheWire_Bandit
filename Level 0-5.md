###🔸 Level 0 → Level 1 
Objective
Connect to the Bandit server via SSH and retrieve the password stored in a file.

Commands Used
ssh, cat

Steps

ssh bandit0@bandit.labs.overthewire.org -p 2220
Connected to remote machine using provided credentials

cat readme
Displayed the password stored in the README file

Password outcome
Result: Password successfully retrieved

Key learning

First interaction with remote systems through SSH

Remote file reading begins with curiosity and cat
