# Linux Terminal Commands and Shortcuts
_A bit beyond the basics_

### Navigation
```sh
cd <path> # go to a specific directory
cd .. # one directory behind
cd ../.. # two directories behind
cd ~ # or cd (go home)
cd - # go to last working directory 
echo $OLDPWD # the above command uses this variable to jump
```

### Screen
```sh
clear # or CTRL + L (clears terminal screen)
```

### Long Commands
```sh
echo "Hi there I'm a really long command" 
# CTRL + A (go to beginning) 
# CTRL + E (go to end)
# CTRL + U (cut everything before cursor - does not use system clipboard)
# CTRL + K (cut everything after cursor - does not use system clipboard)
# ALT + BACKSPACE (cut last word - does not use system clipboard)
# CTRL + Y (paste - does not use system clipboard)
```

### Super User
```sh
sudo !! # run last command as sudo
```

### Files
```sh
tail -f <path_to_file> # view file in real time (very useful while debugging)
```

### Searching
```sh
history | grep -i <search_term> # search your previous commands (spits out everything)
# OR
# CTRL + R (go to reverse search mode)
# type your query and it will show the last command
# CTRL + R again to get previous command with the query
# Repeat and cure amnesia
```

### SSH Keys
```sh
# Generate a new SSH Key
ssh-keygen -t rsa -f ~/.ssh/<KEY_FILENAME> -C <USERNAME> -b 4096 # RSA w/ 4096 bytes
ssh-keygen -t ed25519 -f ~/.ssh/<KEY_FILENAME> -C <USERNAME>
ssh-keygen -t ed25519 -C <USERNAME> # you will be prompted for the file path

# Check the public key
# This is the one you'll need to add to the remote for logging in
cat ~/.ssh/<KEY_FILENAME>.pub

# Copy the content of this file and add(or append) it to the authorized_keys file in your remote server
# The file path in most linux distributions is ~/.ssh/authorized_keys
# Once done, edit the '/etc/ssh/sshd_config' file and add 'PubkeyAuthentication yes' if already present
# Then restart the service using:
sudo service sshd restart # For debian based systems
```

### Version Control
```sh
# Initialize Git
git init

# Change user config for current project
git config user.name "FIRST_NAME LAST_NAME"
git config user.email "EMAIL@EXAMPLE.COM"

# Change user config for all projects
git config --global user.name "FIRST_NAME LAST_NAME"
git config --global user.email "EMAIL@EXAMPLE.COM"

# Check values
git config -l
git config --global -l

# Compact commit log
git log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all

# Changes made in a commit
git show --color --pretty=format:%b <COMMIT_HASH>

# Cloning a specific branch/tag
git clone --depth 1 --branch <name> <repo_url> # will only download HEAD
git clone <repo_url> --branch <name> --single-branch # will download entire branch history leading to HEAD

# Adding a remote repository
git remote add <IDENTIFIER> <REMOTE_URL>

# The following require an ssh key generated in you dev machine to work. 
# The key should also be allowed in your github account 
git remote add github git@github.com:username/repository.git 

# List remote repositories
git remote -v

# Pushing files to the remote repository
# You will be prompted for credentials if an ssh key is not already configured in the dev machine and remote server
git push <REMOTE_REPO_IDENTIFIER> <BRANCH>

# Renaming a remote repository
git remote rename <OLD_IDENTIFIER> <NEW_IDENTIFIER>
```

### User Management
```sh
# Add custom location for user's home directory
mkdir -p <custom_directory_location>

# Add user
sudo useradd -d <custom_directory_location> -s /bin/bash -U <username>

# Change ownership and permissions
sudo chown -R <username>:<username> <custom_directory_location>
sudo chmod -R 750 <custom_directory_location> # Full access to owner, RO for group

# Change Password
sudo passwd <username>

# Add user to a group
sudo usermod -aG <group1>,<group2> <username>
sudo gpasswd -a <username> <groupname>

# Remove user from a group
sudo gpasswd -d <username> <groupname>

# Verify
grep <username> /etc/passwd
grep <username> /etc/group # see if group added

# SSH access
sudo vim /etc/ssh/sshd_config

# Add/Uncomment the following lines
PermitRootLogin no
# PermitRootLogin prohibit-password
# PermitRootLogin without-password
AllowUsers user1 user2 <username>

# Restart the service
sudo service sshd restart # For debian based systems
```

### `.bashrc` File
```sh
# Prettify Git Commits
alias glg="git log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all"

# View Commit Changes
alias gc='git show --color --pretty=format:%b'

# Docker
alias d='docker'
alias dc='docker-compose'
alias dcu='docker-compose up -d --force-recreate'
alias dcl='docker-compose logs -f'

# Kubectl
alias k='kubectl'
alias kgn='kubectl get nodes -o wide'
```
