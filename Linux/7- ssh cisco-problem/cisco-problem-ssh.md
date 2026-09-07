# Connect to a Cisco Switch via SSH (No PuTTY)

### 1- confirm the switch is reachable and check its ssh banner:
```bash
ssh-keyscan 10.20.30.1
```
> note: `ssh-keyscan` only reveal the switch's ssh banner (like `SSH-2.0-Cisco-1.25`), it doesn't connect or save any key — think of it as just knocking on the door.
---

### 2- a common trap, don't use ssh-add to connect:
```bash
ssh-add 10.20.30.1
```
#### this always throw a **"No such file or directory"** error, because `ssh-add` only loads a private key into ssh-agent — it has nothing to do with connecting to a host. for that, `ssh` is the right tool.
---

### 3- try a normal connection:
```bash
ssh netadmin@10.20.30.1
```
#### and here comes the first wall:
```
Unable to negotiate with 10.20.30.1 port 22: no matching key exchange method found.
Their offer: diffie-hellman-group-exchange-sha1,diffie-hellman-group14-sha1,diffie-hellman-group1-sha1
```
#### this switch is old (`SSH-2.0-Cisco-1.25`) and only speaks ancient **KEX** dialects, but modern OpenSSH turns those off by default for security reasons.
---

### 4- teach ssh an old KEX algorithm:
```bash
ssh -oKexAlgorithms=+diffie-hellman-group14-sha1 netadmin@10.20.30.1
```
> watch out for typos here — something like `hellmant` or `ssh1` instead of `sha1` will backfire with:
> `Unsupported KEX algorithm "diffie-hellmant-group14-ssh1"`
---

### 5- second wall, host key type mismatch:
#### once KEX is sorted, a new complaint may pop up:
```
Unable to negotiate with 10.20.30.1 port 22: no matching host key type found.
Their offer: ssh-rsa
```
### the switch only offers an **ssh-rsa** host key, which modern OpenSSH also disables by default.
---

### 6- add HostKeyAlgorithms into the mix:
```bash
ssh -oKexAlgorithms=+diffie-hellman-group14-sha1 -oHostKeyAlgorithms=+ssh-rsa netadmin@10.20.30.1
```
> and just like that, the connection goes through.
---

### 7- (optional) if a cipher error joins the party too:
```bash
ssh -oKexAlgorithms=+diffie-hellman-group14-sha1 -oHostKeyAlgorithms=+ssh-rsa -oCiphers=+aes128-cbc,3des-cbc netadmin@10.20.30.1
```
---

### 8- make peace permanent for this switch:
#### open (or create) the ssh config file:
```bash
nano ~/.ssh/config
```
#### add these lines:
```
Host 10.20.30.1
    KexAlgorithms +diffie-hellman-group14-sha1
    HostKeyAlgorithms +ssh-rsa
    Ciphers +aes128-cbc,3des-cbc
```
#### from now on, just typing `ssh netadmin@10.20.30.1` gets you straight in — no more repeating the incantation every time.