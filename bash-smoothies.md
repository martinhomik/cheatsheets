# Bash Smoothies

## Human readable output of space consumption

See also: http://www.linfo.org/du.html

```
du -hs demo-0.0.1-SNAPSHOT.jar
```

List directory sizes with human readable output
```
du -hs *
```

List directory sizes & total with human readable output
```
du -hsc *
```

List files and directories, sort by size and call less
```
du -h | sort -n | less
```

Provide a list of the names and sizes of directories and files in the current directory that contain the word linux: 
```
du -ah | grep linux
```

One way in which du can be used to produce a list of (mostly) directories and files in a directory tree that are consuming large amounts of disk space is to use grep to search for all the lines that contain the upper case letter M (i.e., for megabytes) or G (for gigabytes), such as
```
du -ah | grep M
```
