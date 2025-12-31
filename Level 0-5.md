### 🔸 Level 0 → Level 1

**Objective**  
Connect to the Bandit server via SSH and retrieve the password stored in a file.

**Commands Used**
ssh, cat

**Step-by-step**
1.ssh bandit0@bandit.labs.overthewire.org -p 2220

2.Connected to remote machine using provided credentials

3.cat readme

4. Displayed the password stored in the README file

**_Result:** Password successfully retrieved_  

### 🔸 Level 1 → Level 2

**Objective**  
Read the password stored in a file named - (dash), which conflicts with command-line syntax.

**Commands Used**
cat, ./, quoting

**Step-by-step**
1. ls
Located the file named -

2. cat ./-
Read the file by prefixing with ./ to avoid interpreting - as an option

**_Result:** Password successfully retrieved_  

### 🔸 Level 2 → Level 3

**Objective**  
Retrieve a password stored in a file with spaces in its name.

**Commands Used**
cat, escaping spaces or quoting

**Step-by-step**
1. ls
Found the file named spaces in this filename

2. cat "spaces in this filename"
Quoted filename to treat spaces as literal characters

**_Result:** Password successfully retrieved_  
### 🔸 Level 3 → Level 4

**Objective**  
Find a hidden file inside the inhere directory that contains the password.

**Commands Used**
ls, cd, ls -a, cat

**Step-by-step**
1.cd inhere
Entered the directory containing hidden files

2.ls -a
Listed files including hidden entries

3.cat .hidden
Displayed content of the hidden password file

**_Result:** Password successfully retrieved_  
### 🔸 Level 4 → Level 5

**Objective**  
Find the correct file among many, based on file type, then retrieve the password.

**Commands Used**
ls, cd, ls -a, file, cat

**Step-by-step**
1. cd inhere
Entered directory with multiple disguised files

2.ls -a
Viewed all items

3.file ./-file07
Used file to identify which one contains readable ASCII text

4.cat ./-file07
Displayed password

### **Key Learning:**
**- Remote access fundamentals**
You connected to a Linux machine over SSH and navigated a real shell — the starting point of hands-on security work.

**-Reading and extracting information safely**
Commands like cat, paired with careful navigation, helped you pull secrets from files without modifying them.

**-Handling tricky filenames**
You learned techniques to work with:

filenames starting with dashes (./-)

filenames containing spaces ("file name")

hidden files (ls -a, dotfiles)
This sharpened your comfort with shell quirks attackers often abuse.

**-Discovering what isn’t immediately visible**
Hidden files and directory structures taught you to look beyond defaults — a habit core to enumeration in cybersecurity.

**-Identifying useful files among noise**
The file command became your flashlight in a cluttered room, helping you recognize which files contain meaningful content regardless of misleading names.

**-Thinking in terms of intent, not just commands**
Instead of randomly typing commands, you began interpreting what the level wants you to discover — a mindset shift toward structured problem-solving.
