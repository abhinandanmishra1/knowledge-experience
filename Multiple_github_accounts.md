## **How to setup multiple github accounts on single machine**
_This thing is done using SSH keys_

---

### Follow the given steps to do so :

> Using Two dummy accounts for explanation

Account 1
  - github username - `person1`
  - github email - `person1@gmail.com`

Account 2
  - github username - `person2`
  - github email - `person2@gmail.com`

> Creating ssh keys and config for both accounts
- Go to Home `cd ~`
- Create a folder `mkdir .ssh`
- Go to `.ssh` using `cd .ssh`
- **Generate ssh keys**
  - `ssh-keygen -t rsa -P "" -f person1`
  - `ssh-keygen -t rsa -P "" -f person2`
- These two command will create these files.
  - `person1, person1.pub` 
  - `person2, person2.pub`
  - pub means public key

- These public keys are required to be registered on their respective accounts.

- For person1:
  - Go to it's github account.
  - Open settings.
  - Inside `SSH and GPG` keys.
  - Click on `new ssh key`.
  - Copy the data of `person1.pub` from your computer and paste it inside `key`(in github).
  - Set `title` as `person1`
  - Save

- Do same thing for person2 as well.

> Create `config` file in `.ssh`

- Config files give location of private keys for each github account that was created by the command above.

- Create a config `touch config`
- Paste and change below data inside config.

**config file looks like this**
``` 
Host person1
  HostName github.com
  User git
  IdentityFile ~/.ssh/person1
Host person2
  HostName github.com
  User git
  IdentityFile ~/.ssh/person2
```


Now public keys are added on your github account and your private keys are located in the config file.

---

> After this while working on any project:

### To clone a repository 
- **person1 :** `git clone person1:<github-username-1>/repo1.git`
- **person2 :** `git clone person2:<github-username-2>/repo2.git`

### To set origin to remote
- **person1 :**  `git remote add origin person1:<github-username-1>/myProject.git`
- **person2 :** `git remote add origin person2:<github-username-2>/myProject.git ` 

### [important] In each repository set the right authority using comfig
- Do not set --global user.name or user.email
- set separately for each project
- For **Person1**
  - `git config user.name person1`
  - `git config user.email person1@gmail.com`
- For **Person2**
  - `git config user.name person2`
  - `git config user.email person2@gmail.com`