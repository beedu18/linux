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

### Version Control
```sh
# Compact commit log
git log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all

# Changes made in a commit
git show --color --pretty=format:%b <COMMIT_HASH>
```