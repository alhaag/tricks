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
### Configuration

Ignore filemod:

```shell
$ git config --global core.fileMode false
```
