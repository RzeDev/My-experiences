# Add picture to grub while booting(Ubuntu)

### 1- download picture and open terminal:

![photo](pic/prepare.png-1)
---


### 2- **transfer** a copy of picture to grub with this command:

```bash
sudo cp gnu-lin.png /boot/grub/
ls -l /boot/grub/gnu-lin.png
```

![photo](pic/transfer-photo-to-grub.png-2)
---

### 3- open grub:

```
sudo nano /etc/default/grub
```

in last line add this variable:

> GRUB_BACKGROUND="/boot/grub/gnu-lin.png"

![photo](pic/add-variable.png-3)
---

### 4- save and exit


---

### 5- now update grub with this command:

```
sudo grub-mkconfig -o /boot/grub/grub.cfg 
```
or
```
sudo update-grub
```
----

### 6- Now reboot system 
![photo](pic/end.jpg-4)
