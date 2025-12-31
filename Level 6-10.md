 ### 🔸 Level 6 → Level 7

**Objective**  
Search the entire filesystem and locate a file owned by a specific user and group, matching an exact size.

**Commands Used**
find, stderr redirection 2>/dev/null, cat

**Step-by-step**
1.find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
Searched the filesystem for a file matching ownership and size, while hiding permission errors

2.cat /var/lib/dpkg/info/bandit7.password
Displayed the content of the discovered file

**_Result:** Password successfully retrieved_ 
### 🔸 Level 7 → Level 8

**Objective**  
Extract a unique line from a large text file to obtain the password.

**Commands Used**
cat, sort, uniq, strings, grep

**Step-by-step**
1.sort data.txt | uniq -u
Sorted lines so duplicates align, then filtered for a line appearing only once

2.(alternative approach) strings data.txt | grep "millionth"
Directly extracted printable strings and searched for the target word indicating the correct line

**_Result:** Password successfully retrieved_ 
### 🔸 Level 8 → Level 9

**Objective**  
Find the line in a dataset that appears exactly once — similar to previous level to reinforce pattern recognition.

**Commands Used**
sort, uniq

**Step-by-step**
1.sort data.txt | uniq -u
Sorted and isolated the line with a single occurrence

2.cat <resulting line>
Viewed the unique line containing the password

**_Result:** Password successfully retrieved_ 
### 🔸 Level 9 → Level 10

**Objective**  
Extract hidden password strings from a large random file.

**Commands Used**
strings, grep, pattern matching (^=)

**Step-by-step**
1.strings data.txt | grep "^="
Filtered printable strings and matched those beginning with = to locate the correct line

2.cat <extracted string>
Revealed password-like data

**_Result:** Password successfully retrieved_ 
### 🔸 Level 10 → Level 11

**Objective**  
Decode a base64-encoded text to retrieve the password.

**Commands Used**
base64 -d, cat

**Step-by-step**
1.cat data.txt | base64 -d
Decoded the base64 content contained in the file

2.Read resulting output to obtain password

**_Result:** Password successfully retrieved_ 

### **Key Learning**
**-Targeted filesystem search**
Became confident filtering files using ownership, size, type, and permissions with find, turning the filesystem into something you can query, not wander through.

**-Noise reduction & output control**
Learned to silence errors with 2>/dev/null, keeping focus on useful results — a small trick that dramatically improves clarity when enumerating systems.

**-Data triage through pipelines**
Used chains of sort, uniq, strings, and grep to sift through massive or noisy datasets, extracting meaningful signals from overwhelming noise.

**-Pattern recognition through regex anchors**
Understood that ^ and other pattern tools can pinpoint exact content instead of scrolling endlessly — efficiency over brute-force reading.

**-Encoding awareness**
Recognized when information is encoded (like Base64) and how to decode it reliably, a foundational skill for spotting hidden data in security challenges.

**-Thinking like a filter, not a finder**
Instead of searching with your eyes, you let the shell do the work — a shift toward reproducible, automatable problem-solving.
