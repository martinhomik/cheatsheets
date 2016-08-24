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

## Load testing from console

```
ab -c 1 -n 1000 -p blafasel.txt -T "application/json" "http://domainrecommendation-service-server.domrec-wsdplt268.pearl1.websales.united.domain:9090/domrec/domain/recommendation"
```

blafasel.txt:
```json
{"query":"blafasela","country":"de","phase":"GA","configuration":"geoIpTldVariation","type":[""],"onlyTld":null,"order":"relevance","optional":{"GEO_IP":["74.125.18.150"],"CUSTOMER_NUMBER":[""],"ZIP_CODE":[""]},"pageSize":"5","pageOffset":"0"}
```

## Grep
```
grep -B 50 "05:13:50,004:2014-12-10 05:13:50||4|||20|20|10|312266" domrec-executorService-stats-2014-12-10.log
````

## Awk
```
awk -F "|" '{if ($8=="10") print $0}' domrec-executorService-stats-2014-12-10.log
````

## Cut
```
cut -d "|" -f 7 	10.log | sort | uniq -c
````

## Find pom.xml files that contain a string pattern
```
find . -name 'pom.xml' -exec grep -H "4.10.20-SNAPSHOT" {} \;
````


## Sort a csv file by a column

* read file via cat
* parse csv by awk where thge delimiter is a tab character; prepend the selected column
* sort lines
* keep everything from the second column on
```
cat report_2015-11-25_2015-11-25.csv | awk -F "\t" '{print $4"\t"$0}' | sort | cut -f 2- > report_2015-11-26_2015-11-26.csv.sorted
```

## Login as root with wvqyec AMPUA password
```
sudu su -
````

## Applications on Ubuntu:
```
/usr/lib/hive
/var/lib/hive
/etc/hive	
````

## Linux Service start, stop, restart
```
service hive-server2 start|stop|restart
````

## List all files in long format, order by modification time descending
```
ls -latr
```

## Print value of a symbolic link or canonical file name
```
readlink -f /usr/lib/hive/lib/libmysql-java.jar
--> follows recursively all sybolic links down to target file
```


## Put a job into background:
```
CTRL+Z
````

## Get a job into the foreground:
```
fg
````

## List all running jobs:
```
jobs
````

## Kill first job after calling 'jobs':
```
kill %1 
````

## Kill all jobs mathing a name
```
ps -ef | grep "airflow" | grep -v grep | awk '{print $2}' | xargs kill -9
```
or
  
```  
pkill -f "airflow"
````

## Tree view of files and folders:
Download tree from homebrew
```
tree -L 2
````

## Watch: execute a program periodically, showing output fullscreen
Watch thread pool statistics of elasticsearch every 2 seconds
```
watch -n 2 "curl -s localhost:9200/_cat/thread_pool"
```
* n : time intervall in seconds
* s: silent mode in curl. No Download information.
	 
To watch the contents of a directory change, you could use
```
watch -d ls -l
````

## PSSH: parallel ssh program
Check the health of hosts in a cluster
```
pssh -i -h list.of.cluster.hosts curl -s localhost:9200/_cat/health
```

## ClusterSSH

TODO

## chmod

7 = all rights
6 = read and write
5 = read and execute
4 = read only
3 = execute and write
2 = write only
1 = execute only
0 = no rights


### To recursively give directories read&execute privileges:

```
find /path/to/base/dir -type d -exec chmod 755 {} +
```

### To recursively give files read privileges:
```
find /path/to/base/dir -type f -exec chmod 644 {} +
```

### Or, if there are many objects to process:
```
chmod 755 $(find /path/to/base/dir -type d)
chmod 644 $(find /path/to/base/dir -type f)
```
Or, to reduce chmod spawning:
```
find /path/to/base/dir -type d -print0 | xargs -0 chmod 755 
find /path/to/base/dir -type f -print0 | xargs -0 chmod 644
```
Alternative:
```
chmod -R u+rwX,go+rX,go-w /path
```
Meaning:

    -R = recursively;
    u+rwX = Users can read, write and execute;
    go+rX = group and others can read and execute;
    go-w = group and others can't write


## Going to a specific line number using Less in Unix:
```
sed -n '320123'p filename 
````

If you want a range then you can:
```
sed -n '320123,320150'p filename 
```
If you want from a particular line to the very end then:
```
sed -n '320123,$'p filename 
```
