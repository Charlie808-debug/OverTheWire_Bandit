## **🔸 Level 31 → Level 32**

**Objective**
Add a file to a Git repository that normally ignores `.txt` files and push it to trigger password retrieval.

**Commands Used**

```
git clone
echo
git add -f
git config
git commit
git push
```

**Step-by-step**

1. `git clone ssh://bandit31-git@localhost:2220/home/bandit31-git/repo`
   Cloned the repository where `.txt` files are ignored
2. `echo -n "May I come in?" > key.txt`
   Created the required file despite `.gitignore`
3. `git add -f key.txt`
   Forced Git to track the file even though ignored
4. Set identity and commit:

   ```
   git config user.name "bandit31"
   git config user.email "bandit31@bandit.labs.overthewire.org"
   git commit -m "Add key file"
   ```
5. `git push origin master`
   Pushed changes, and the remote responded with the password

***Result:*** Password successfully retrieved

---

## **🔸 Level 32 → Level 33**

**Objective**
Escape an environment that converts all typed input to uppercase, blocking normal commands.

**Commands Used**

```
$0
whoami
cat
```

**Step-by-step**

1. Logging in places you inside a shell that uppercases input
2. Executed `$0` to spawn a fresh shell without letter-case transformation
3. `cat /etc/bandit_pass/bandit33`
   Read the password normally from the unrestricted shell

***Result:*** Password successfully retrieved

---

## **🔸 Level 33 → Level 34**

**Objective**
Use the retrieved password to access the final Bandit level and confirm completion.

**Commands Used**

```
ssh
cat
```

**Step-by-step**

1. Logged in using the password from Level 32
2. Accessed the final password file to confirm successful completion

***Result:*** Bandit wargame completed successfully 

---

# **Key Learning**

**- Bypassing ignore rules to influence system behavior**
  You learned to override `.gitignore` through forced staging (`git add -f`), showing how attackers can slip data past intended rules when misconfigurations exist.

**- Understanding that restrictions often apply only to *input*, not *execution***
  Level 32 reinforced that even when your keystrokes are transformed, shell variables and program execution pathways remain stable — a reminder to look for *what isn’t restricted* rather than staring at what is.

**- Thinking beyond the obvious shell**
  `$0` taught you that shells stack like layers; escaping one doesn’t require breaking it — just *invoking another*.

**- Recognizing that persistence beats obstacles**
  The final stretch rewarded every skill built along the way: decoding, privilege boundaries, version control forensics, restricted shell escapes, automation, and enumeration.

**- Awareness that real leaks often live in development artifacts**
  Levels 27–31 showed that secrets hide in commits, tags, ignored files, pushed metadata, or overlooked branches — a real-world lesson in software supply chain security.

and we’ll convert your work into a profile-worthy asset.
