# Generate ssh Key for GitHib

### how to start:

Open terminal, Type:

```bash
ssh-keygen -t ed25519 -C "YourEamil@gmail.com"
```

hit Enter:

![photo](assests/ssh-keygen.png-1)

than hit Enter again:

![photo](assests/finish-sshkey.png-2)

now ssh key genereate at **~/.ssh** to get this path type:

```bash
cd ~/.ssh
ls
```

now id_ed25519.pub is my public key of ssh that I alredy generate.

 now to enter entity type this command:

```bash
 eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

now cat ssh id_ed25519.pub with below command:

```bash
cd ~/.ssh
cat id_ed25519.pub
```

must seen this command:
![photo](assests/cat-public-KEY.png-3)

> now ssh key redy to setup in github.
