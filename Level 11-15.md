### 🔸 Level 11 → Level 12

**Objective**
Decode a Base64-encoded file to obtain the password.

**Commands Used**

```
base64 -d
cat
```

**Step-by-step**

1. `cat data.txt | base64 -d`
   Decoded the Base64 content into readable text
2. Read the decoded output to reveal the password

***Result:*** Password successfully retrieved

---

### 🔸 Level 12 → Level 13

**Objective**
Decode a ROT13-encoded file and extract the password.

**Commands Used**

```
tr
cat
```

**Step-by-step**

1. `cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'`
   Applied ROT13 transformation to map each letter 13 positions forward
2. Retrieved decoded text containing the password

***Result:*** Password successfully retrieved

---

### 🔸 Level 13 → Level 14

**Objective**
Reverse multiple layers of compression and encoding to reach the final password.

**Commands Used**

```
xxd -r
gzip / gunzip
bzip2 / bunzip2
tar
file
mkdir
mv
cp
```

**Step-by-step**

1. Copied `data.txt` to a temp directory and converted from hex using `xxd -r`
2. Used `file` repeatedly to identify file type after each extraction
3. Decompressed each layer using the correct tool (`gzip`, `bzip2`, `tar`) as detected
4. Continued until the final ASCII text file was obtained and read with `cat`

***Result:*** Password successfully retrieved

---

### 🔸 Level 14 → Level 15

**Objective**
Use a private SSH key to log in as the next user and read their password file.

**Commands Used**

```
nano
chmod 600
ssh -i
cat
```

**Step-by-step**

1. Saved the provided private key into a temporary file using `nano`
2. `chmod 600 <keyfile>` — adjusted permissions so SSH accepts the key
3. `ssh -i <keyfile> -p 2220 bandit14@localhost` — logged in using the key
4. `cat /etc/bandit_pass/bandit14` — accessed the password file for the next level

***Result:*** Password successfully retrieved

---

### 🔸 Level 15 → Level 16

**Objective**
Connect to a service running on a local port and submit the previous password to retrieve the next one.

**Commands Used**

```
nc
echo
openssl s_client
```

> *Two valid approaches exist; using `openssl s_client` is the stable one.*

**Step-by-step**

1. `echo "<previous_password>" | openssl s_client -quiet -connect localhost:30001`
   Sent the password securely to the SSL service running on port **30001**
2. The service validated the password and returned the next one in response

***Result:*** Password successfully retrieved

---
### **Key Learning**
**-Recognizing & decoding common encodings**
Learned to identify when information is wrapped in Base64 or ROT13 and how to decode it reliably using command-line tools instead of external sites.

**-Handling chained transformations**
Broke down multi-layered compression and encoding step by step using file to guide decisions — building patience and systematic problem-solving for real forensic tasks.

**-Interacting with SSH beyond passwords**
Used private keys and permission hardening (chmod 600) to authenticate securely — reinforcing how authentication mechanisms work in Linux systems.

**-Understanding tool behavior through permissions**
Discovered that SSH rejects private keys with permissive access, highlighting how security tools enforce best practices instead of relying on user memory.

**-Communicating with network services directly**
Sent data into listening services using nc and openssl s_client, preparing for later scenarios like banner grabbing, protocol testing, and custom exploit delivery.

**-Developing protocol instincts**
Realized that encoding, compression, and transport are separate layers — and peeling them in the correct order is often the true challenge in security puzzles.
