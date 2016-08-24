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
