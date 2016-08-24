## Find last 50 commits by mhomik

```sh
svn log --search mhomik -l 50
```

## Recursively delete .svn folders:

```sh
rm -rf `find . -type d -name .svn`
```

## Sort lines for 'svn status'
```sh
svn status | sort -k 2
```
