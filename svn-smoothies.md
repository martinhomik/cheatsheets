## Find last 50 commits by mhomik
```=
svn log --search mhomik -l 50
```

## Recursively delete .svn folders:
```
rm -rf `find . -type d -name .svn`
```

## Sort lines for 'svn status'
```
svn status | sort -k 2
````
