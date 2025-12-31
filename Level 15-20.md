## **🔸 Level 16 → Level 17**

**Objective**
Scan a local port range, locate the port running an encrypted service, connect to it, submit the previous password, and retrieve a private SSH key for the next user.

**Commands Used**

```
nmap
ncat / ncat --ssl
ssh -i
mkdir
nano
chmod
```

**Step-by-step**

1. `nmap -A localhost -p 31000-32000`
   Scanned the port range to find which service was accepting SSL connections
2. Connected to the identified port using SSL:
   `echo "<previous_password>" | ncat --ssl localhost <port>`
   Retrieved an RSA private key as output
3. Saved the key in a temp directory, adjusted permissions (`chmod 600`)
4. Logged in as the next user using the key:
   `ssh -i private.key bandit17@bandit.labs.overthewire.org -p 2220`

***Result:*** Password successfully retrieved

---

## **🔸 Level 17 → Level 18**

**Objective**
Identify the difference between two files and extract the password.

**Commands Used**

```
diff
cat
```

**Step-by-step**

1. `diff passwords.old passwords.new`
   Compared both files to find the altered line
2. The differing line revealed the password for the next level

***Result:*** Password successfully retrieved

---

## **🔸 Level 18 → Level 19**

**Objective**
Bypass a shell that logs you out immediately and read a file remotely.

**Commands Used**

```
ssh "<command>"
cat
```

**Step-by-step**

1. `ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"`
   Passed `cat` as a command during SSH login to avoid triggering the logout behavior
2. Received password output directly from remote execution

***Result:*** Password successfully retrieved

---

## **🔸 Level 19 → Level 20**

**Objective**
Use a SetUID binary to read a privileged password file.

**Commands Used**

```
ls -l
./bandit20-do
cat
```

**Step-by-step**

1. `ls -l`
   Observed that `bandit20-do` runs as `bandit20` due to SetUID permissions
2. `./bandit20-do cat /etc/bandit_pass/bandit20`
   Executed the binary to run `cat` with elevated privileges and read the restricted file

***Result:*** Password successfully retrieved

---

## **🔸 Level 20 → Level 21**

**Objective**
Interact between two processes: use a SetUID binary to send input to a service you control and retrieve the next password.

**Commands Used**

```
nc -lvp <port>
./suconnect <port>
```

**Step-by-step**

1. Started a listener locally:
   `nc -lvp 2341`
2. Sent the previous password using SetUID binary:
   `./suconnect 2341`
3. Listener output returned the next password

***Result:*** Password successfully retrieved

---

---

### **Key Learning **

* **- Focused port enumeration & service validation**
  Built confidence using `nmap` to locate specific services among noise, a core technique for reconnaissance and lateral movement.

* **- Secure communication with encrypted services**
  Used SSL wrappers (`ncat --ssl`, `openssl`) to talk to encrypted endpoints — foundational for interacting with secure protocols.

* **- Key-based authentication mastery**
  Handled private keys safely (`chmod 600`), reinforcing SSH security rules and authentication workflows beyond passwords.

* **- Escaping restricted or hostile shells**
  Executed commands *during* SSH login to avoid forced logout — understanding that command execution can bypass interactive shell traps.

* **- Privilege escalation through SetUID binaries**
  Leveraged binaries configured to run with higher privileges, applying controlled execution to read protected files — a direct link to real-world escalation techniques.

* **- Inter-process communication for data extraction**
  Made services talk to each other (`nc` + SetUID binary), highlighting that chaining tools together often unlocks access that standalone commands cannot.

and we move forward.
