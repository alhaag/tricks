# GIT

### Verifications

View last commits:

```
$ git log
```

Check which commits have not been pushed to origin:

```
$ git log origin/refactory..refactory
```

## Reverts
Revert all file mode changes:
```
$ git diff -p \
    | grep -E '^(diff|old mode|new mode)' \
    | sed -e 's/^old/NEW/;s/^new/old/;s/^NEW/new/' \
    | git apply
```

Revert file modifications:
```
$ git checkout file.txt 
```
### Transfer all branch to master

```
git checkout seotweaks
git merge -s ours master
git checkout master
git merge seotweaks
```
The result should be your master is now essentially seotweaks.

(-s ours is short for --strategy=ours)

### Rename branch (local and remote)

```
git checkout <old_name>
git branch -m <new_name>
git push origin --delete <old_name>
git push origin -u <new_name>
```

### Delete branch (local)
```
git branch -d <branch_name>
```
### Delete branch (remote)
```
git push <remote_name> --delete <branch_name>
```

### TAG

View TAGs:
```shell
$ git tag
```


Create TAG:

```shell
$ git tag -a v0.0.1 -m "Comment"
$ git push origin v0.0.1
```
or
```shell
$ git tag v0.0.1
$ git push origin <branch> --tags
```

### Configuration

Ignore filemod:

```shell
$ git config --global core.fileMode false
```

Show git branch on user bash:
```
# parse branch                                                                                                        
function parse_git_branch () {                                                                                          
   git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'                                                    
}

# PS1 conf
PS1="\n\[$IGrey\]┌──[\D{%d/%m/%y-%H:%M:%S}]──(\[$IGreen\]\u@\h\[$IGrey\]:\[$IBlue\]\w\[$IGrey\] \$(/bin/ls -1 | /usr/bin/wc -l | /bin/sed 's: ::g') files, \$(/bin/ls -lah | /bin/grep -m 1 total | /bin/sed 's/total //'))\[$IYellow\]\$(parse_git_branch) \n\[$IGrey\]└> \[$IGreen\]$ \[$White\]"

```

### Extras
Local light web interface to view changes:
```
$ sudo apt install lighttpd
$ cd project
$ git instaweb (access on 127.0.0.1:1234)
$ git instaweb --stop
```

Diff with Meld:
```
$ sudo apt-get install meld

# NEW FILE ~/scripts/gitDiff.py
--------
#!/usr/bin/python
import sys
import os
os.system('meld "%s" "%s"' % (sys.argv[2], sys.argv[5]))
--------

$ git config --global diff.external ~/scripts/gitDiff.py
```

