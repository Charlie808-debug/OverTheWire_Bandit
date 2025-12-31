### **🔸 Level 26 → Level 27**

**Objective**
Use a private SSH key to log in as the next user, bypass a restricted environment that automatically closes, and escape into a usable shell to read the password.

**Commands Used**

```
ssh -i
chmod
terminal resizing
vi escape
./bandit27-do
```

**Step-by-step**

1. `ssh -i bandit26.sshkey bandit26@bandit.labs.overthewire.org -p 2220`
   Logged in using provided private key, but session closes immediately due to a restricted environment
2. Resized terminal window small enough to trigger pagination during login
   This forces the banner output into `more`
3. When the `:` prompt of `more` appeared, pressed `v`
   Entered `vi` editor mode embedded inside `more`
4. From `vi`, escaped into a shell and executed:
   `./bandit27-do cat /etc/bandit_pass/bandit27`
   Retrieved the password via the setuid helper binary

***Result:*** Password successfully retrieved

---

## **🔸 Level 27 → Level 28**

**Objective**
Clone a Git repository to extract the password stored within.

**Commands Used**

```
git clone
cd
cat
```

**Step-by-step**

1. `git clone ssh://bandit27-git@localhost:2220/home/bandit27-git/repo`
   Cloned the repository containing password data
2. `cd repo`
3. `cat README`
   Displayed the password present in the repository

***Result:*** Password successfully retrieved

---

## **🔸 Level 28 → Level 29**

**Objective**
Explore Git commit history to find a password that existed in a previous version of the repository.

**Commands Used**

```
git clone
git log --oneline
git show
```

**Step-by-step**

1. `git clone ssh://bandit28-git@localhost:2220/home/bandit28-git/repo`
2. `cd repo`
3. `git log --oneline`
   Viewed commit history
4. `git show <previous_commit_hash>`
   Inspected older commit to read the password stored before removal

***Result:*** Password successfully retrieved

---

## **🔸 Level 29 → Level 30**

**Objective**
Identify and switch to a Git branch where the password is stored.

**Commands Used**

```
git clone
git branch -a
git checkout
git show
```

**Step-by-step**

1. `git clone ssh://bandit29-git@localhost:2220/home/bandit29-git/repo`
2. `cd repo`
3. `git branch -a`
   Listed available branches
4. `git checkout dev`
   Switched to the development branch containing the password
5. `cat README.md`
   Displayed password stored on the branch

***Result:*** Password successfully retrieved

---

## **🔸 Level 30 → Level 31**

**Objective**
Locate a password that is stored as a Git tag.

**Commands Used**

```
git clone
git tag
git show
```

**Step-by-step**

1. `git clone ssh://bandit30-git@localhost:2220/home/bandit30-git/repo`
2. `cd repo`
3. `git tag`
   Listed tags associated with the repository
4. `git show <tag_name>`
   Revealed the content tagged in repository metadata, including the password

***Result:*** Password successfully retrieved

---

### Key Learning

* **Escaping restricted shells using internal program behavior**
  You exploited program flow (`more` → `vi` → shell escape) to break out of jailed environments, gaining confidence in *interactive binary escape paths*.

* **Navigating Git as an investigative tool**
  You learned that passwords aren’t always stored in the current version — sometimes they live in:

  * active files,
  * older commits,
  * branches,
  * or tags.
    This built intuition for *time-traveling through repositories* to uncover history.

* **Tracking sensitive data through development artifacts**
  Realized how secrets can leak via commit history, metadata, abandoned branches, and tagged snapshots — mirroring real-world supply chain vulnerabilities.

* **Understanding layered access workflows**
  Private key usage + setuid helper binaries + terminal manipulation showed how authentication, privilege elevation, and environment control intertwine.

* **Systematic retrieval instead of guessing**
  You didn’t brute force or search blindly — you followed developer breadcrumbs (`README`, commit logs, tags), reinforcing methodical enumeration.
