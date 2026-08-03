
# Extract .rpm binary source

### 1- confirm existincy of .rpm:

```
ls -l
```
![photo](pic/ls-terminal.png-1)
---

### 2- extracp .rpm file with following command:

```
rpm2cpio aria2-1.37.0-9.fc44.x86_64.rpm | cpio -idv
```
![photo](pic/run-command.png-2)
---
### 3- run following command with $PATH command:

```
echo 'export PATH="$HOME/learn/usr/bin:$PATH"' >> ~/.bashrc
```
![photo](pic/enable-bashrc.png-4)
---
### 4- exit terminal or type following command:

```
source ~/.bashrc
```

![photo](pic/enable-bashrc.png-4)

>#### note: if close terminal then no need to type "__*source ~/.bashrc*__" command but if it is not possible to exit terminal and open new one then the command most be typed
---