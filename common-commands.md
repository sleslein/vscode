# Common Commands

This file continas several commands for various CLI's

## Git

**Create a new brach off current**

```terminal
git checkout -b [branchName]
```

Removing local branches which have been removed from the remote server

```terminal
git branch | grep -v "master" | xargs git branch -d
```

## General

**Edit Bash RC**
The following command will open the .bashrc in VS Code.

```terminal
.eb
```

It is an alias for the followng

```terminal
alias .eb='code ~/.bashrc'
```

**Update Bash RC Source**
After editing the .bashrc file, this command will update the alises

```terminal
.sb
```

It is an alias for the followng

```terminal
alias .sb='source ~/.bashrc'
```
