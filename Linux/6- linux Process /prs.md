## 1- what is process:
### Linux calls each running program a process. The Linux system assigns each process a process ID (PID) and manages how the process uses memory and CPU time based on that PID. When a Linux system first boots, it starts a special process called the init process. The init process is the core of the Linux system; it runs scripts that start all of the other processes running on the system, including the processes that start the text consoles and graphical windows you use to log in
---

## 2- PS command:
### command to look current running process
```bash
ps 
```
### output: 
| PID   |   TTY     |   TIME    |   CMD
| ---   |   ---     |   ---     |   ---
|12618  |   pts/1   | 00:00:00  |   bash
|13291  |   pts/1   | 00:00:00  |   ps

### by default ***ps*** show only the process that are running in user shell. also the time means that the means that how much process used CPU

### ps has three different styles of options:

* **Unix-style options:** start with a single dash `-`
* **BSD-style options:** do not use a dash
* **GNU long options:** start with two dashes `--`

### for example, to see every process running on the system:

```bash
ps -ef
```

### output contains:

| Column | Meaning                                                    |
| ------ | ---------------------------------------------------------- |
| UID    | The user who is responsible for running the process        |
| PID    | The process ID of the process                              |
| PPID   | The process ID of the parent process                       |
| C      | The processor utilization over the lifetime of the process |
| STIME  | The system time when the process was started               |
| TTY    | The terminal from which the process was started            |
| TIME   | The cumulative CPU time used by the process                |
| CMD    | The command/program that was started                       |

### some process names are shown in brackets `[]`. this means that the process is currently swapped out from physical memory into virtual memory on the hard drive.

---

## 3- Process states

### when a process is waiting for an event, the Linux kernel can put the process into sleep mode.

### there are two important types of sleep

* **Interruptible sleep:** the process receives a signal immediately and wakes up.
* **Uninterruptible sleep:** the process wakes up only when an external event happens, such as hardware becoming available. other signals are saved until the process wakes up.

### Zombie process

### if a process has ended but its parent process has not acknowledged the termination signal, the process becomes a zombie. it stays in this state until the parent acknowledges the termination.

---

## 4- Selecting processes with PS

### when we want to see only specific processes, we can use different options with the ps command. for example, we can select processes based on user, group, PID, terminal, or process state

| Option           | Meaning                                                        |
| ---------------- | -------------------------------------------------------------- |
| `a`              | show every process associated with a TTY terminal              |
| `-A`, `-e`       | show every process on the system                               |
| `-C CommandList` | show only processes running a specific command                 |
| `-g GIDList`     | show processes whose effective group is in GIDList             |
| `-G GIDList`     | show processes whose real group is in GIDList                  |
| `-N`             | show every process except selected processes                   |
| `-p PIDList`     | show only specific PIDs                                        |
| `-r`             | show only processes that are running                           |
| `-t ttyList`     | show processes associated with specific TTY terminals          |
| `-T`             | show processes associated with the current TTY                 |
| `-u UserList`    | show processes whose effective user is in UserList             |
| `-U UserList`    | show processes whose real user is in UserList                  |
| `x`              | remove the restriction of being associated with a TTY terminal |

### real user/group means the user or group associated with the account. effective user/group means a temporary alternative user or group identification, such as with SUID and GUID permissions.

### if you want to make sure you see every process associated with a specific user or group, you can use both effective and real options.

```bash
ps -u Christine -U Christine
```

---

## 5- TOP command:

### ps gives us a snapshot of the processes running on the system, but top shows process information in real-time. this makes top useful when we want to monitor processes and find trends in CPU and memory usage.

```bash
top
```

### the first section of top shows general system information

* current time
* how long the system has been running
* number of logged-in users
* load average

**### load average has three values:**

* **1-minute load average**
* **5-minute load average**
* **15-minute load average**

### the higher the load average, the more load the system is experiencing. a high 1-minute value can happen during a short burst of activity, but a high 15-minute value can indicate that the system may have a problem

**### we can also check load average using:**

```bash
uptime
```

**### uptime shows the same load average information as top and also shows how long the Linux system has been running.**

---

## 6- FREE command:

### the `free` command is used to quickly check memory usage.

```bash
free -h
```

### the `-h` option means human-readable and adds unit labels to make the output easier to read.

### free shows information about:

* **Physical memory (RAM):** total, used, and free memory
* **Swap memory:** total, used, and free swap space
* **Available memory**

---

## 7- TOP process information:

### the process list in top contains several columns:

| Column  | Meaning                                               |
| ------- | ----------------------------------------------------- |
| PID     | The process ID                                        |
| USER    | The username of the process owner                     |
| PR      | The process priority                                  |
| NI      | The nice value                                        |
| VIRT    | The total virtual memory used by the process          |
| RES     | The physical memory used by the process               |
| SHR     | The memory shared with other processes                |
| S       | The process status                                    |
| `%CPU`  | The percentage of CPU time used by the process        |
| `%MEM`  | The percentage of physical memory used by the process |
| `TIME+` | The total CPU time used since the process started     |
| COMMAND | The command/program started by the process            |

### process status in the `S` column:

* `D` = interruptible sleep
* `I` = idle
* `R` = running
* `S` = sleeping
* `T` = traced or stopped
* `Z` = zombie

### by default, top sorts processes based on `%CPU`.

### while top is running, we can press different keys to change how the information is displayed or sorted.

| Command    | Meaning                                   |
| ---------- | ----------------------------------------- |
| `F` or `O` | select the field used for sorting         |
| `R`        | reverse the current sort order            |
| `k`        | kill a specific process                   |
| `r`        | change the priority (renice) of a process |
| `d` or `s` | change the update interval                |
| `u`        | show processes for a specific user        |
| `n` or `#` | set the number of processes to display    |
| `c`        | show command name or full command line    |
| `i`        | show/hide idle processes                  |
| `q`        | exit top                                  |

### by using the sorting options in top, we can find processes that are using too much CPU or other system resources.

---

## 8- WATCH command:

### the `watch` command runs another command repeatedly and shows its output in real-time. by default, it re-runs the command every two seconds.

```bash
watch uptime
```

### this example repeatedly runs `uptime` so we can continuously monitor the system load.

### watch is not limited to process monitoring. we can use it with other commands to monitor changes, such as changes in a directory.