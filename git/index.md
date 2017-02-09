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

### TAG

Create TAG:

```shell
$ git tag -a v0.0.1 -m "Comment"
$ git push origin v0.0.1
```
ou
```shell
$ git tag v0.0.1
$ git push origin <brach> --tags
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
