# Bash Smoothies

## Human readable output of space consumption

See also: http://www.linfo.org/du.html

```sh
du -hs demo-0.0.1-SNAPSHOT.jar
```

List directory sizes with human readable output

```sh
du -hs *
```

List directory sizes & total with human readable output

```sh
du -hsc *
```

List files and directories, sort by size and call less

```sh
du -h | sort -n | less
```

Provide a list of the names and sizes of directories and files in the current directory that contain the word linux: 

```sh
du -ah | grep linux
```

One way in which du can be used to produce a list of (mostly) directories and files in a directory tree that are consuming large amounts of disk space is to use grep to search for all the lines that contain the upper case letter M (i.e., for megabytes) or G (for gigabytes), such as

```sh
du -ah | grep M
```

## Load testing from console

```sh
ab -c 1 -n 1000 -p blafasel.txt -T "application/json" "http://domainrecommendation-service-server.domrec-wsdplt268.pearl1.websales.united.domain:9090/domrec/domain/recommendation"
```

blafasel.txt:

```json
{"query":"blafasela","country":"de","phase":"GA","configuration":"geoIpTldVariation","type":[""],"onlyTld":null,"order":"relevance","optional":{"GEO_IP":["74.125.18.150"],"CUSTOMER_NUMBER":[""],"ZIP_CODE":[""]},"pageSize":"5","pageOffset":"0"}
```

## Grep

```sh
grep -B 50 "05:13:50,004:2014-12-10 05:13:50||4|||20|20|10|312266" domrec-executorService-stats-2014-12-10.log
```

## Awk
```sh
awk -F "|" '{if ($8=="10") print $0}' domrec-executorService-stats-2014-12-10.log
```

## Cut
```sh
cut -d "|" -f 7 	10.log | sort | uniq -c
```

## Find pom.xml files that contain a string pattern
```sh
find . -name 'pom.xml' -exec grep -H "4.10.20-SNAPSHOT" {} \;
```


## Sort a csv file by a column

* read file via cat
* parse csv by awk where thge delimiter is a tab character; prepend the selected column
* sort lines
* keep everything from the second column on

```sh
cat report_2015-11-25_2015-11-25.csv | awk -F "\t" '{print $4"\t"$0}' | sort | cut -f 2- > report_2015-11-26_2015-11-26.csv.sorted
```

## Login as root with wvqyec AMPUA password
```sh
sudu su -
```

## Applications on Ubuntu:
```sh
/usr/lib/hive
/var/lib/hive
/etc/hive	
```

## Linux Service start, stop, restart
```sh
service hive-server2 start|stop|restart
```

## List all files in long format, order by modification time descending
```sh
ls -latr
```

## Print value of a symbolic link or canonical file name
```sh
readlink -f /usr/lib/hive/lib/libmysql-java.jar
--> follows recursively all sybolic links down to target file
```


## Put a job into background:
```sh
CTRL+Z
```

## Get a job into the foreground:
```sh
fg
```

## List all running jobs:
```sh
jobs
```

## Kill first job after calling 'jobs':
```sh
kill %1 
```

## Kill all jobs mathing a name
```sh
ps -ef | grep "airflow" | grep -v grep | awk '{print $2}' | xargs kill -9
```
or
  
```sh  
pkill -f "airflow"
```

## Tree view of files and folders:
Download tree from homebrew
```sh
tree -L 2
```

## Watch: execute a program periodically, showing output fullscreen
Watch thread pool statistics of elasticsearch every 2 seconds

```sh
watch -n 2 "curl -s localhost:9200/_cat/thread_pool"
```

* n : time intervall in seconds
* s: silent mode in curl. No Download information.
	 
To watch the contents of a directory change, you could use

```sh
watch -d ls -l
```

## PSSH: parallel ssh program
Check the health of hosts in a cluster

```sh
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

```sh
find /path/to/base/dir -type d -exec chmod 755 {} +
```

### To recursively give files read privileges:

```sh
find /path/to/base/dir -type f -exec chmod 644 {} +
```

### Or, if there are many objects to process:

```sh
chmod 755 $(find /path/to/base/dir -type d)
chmod 644 $(find /path/to/base/dir -type f)
```

Or, to reduce chmod spawning:

```sh
find /path/to/base/dir -type d -print0 | xargs -0 chmod 755 
find /path/to/base/dir -type f -print0 | xargs -0 chmod 644
```
Alternative:

```
chmod -R u+rwX,go+rX,go-w /path
```
Meaning:

    -R    = recursively;
    u+rwX = Users can read, write and execute;
    go+rX = group and others can read and execute;
    go-w  = group and others can't write


## Going to a specific line number using Less in Unix:

```sh
sed -n '320123'p filename 
```

If you want a range then you can:

```sh
sed -n '320123,320150'p filename 
```

If you want from a particular line to the very end then:

```sh
sed -n '320123,$'p filename 
```

## Curl

```sh
curl -X GET http://domrec.1and1.com/domrec/monitor/ping
```

```sh
curl -H "Content-Type: application/json"  -H "Accept: application/xml" -X POST -d '{"query":"blafasela","country":"de","optional":{"name":["Foo"],"lastname":["Bar"]},"pageSize":"5","pageOffset":"0"}' http://somedomain/somepath
```

## whatis 'keyword'

Der Befehl whatis dient dazu, eine sehr knappe, einzeilige Beschreibung eines bestimmten Befehls anzuzeigen.

## apropos 'keyword'
Mit dem Befehl apropos entlocken Sie der Hilfe etwas mehr an Informationen über den gesuchten Terminalbefehl.

## Test net connectivity:
```sh
nc -zv hoebwa3mwdev.mw.server.lan 10080
```

## Measure run time of a shell command
```sh
time <command>
```

## Shell Scripts
* Parameter Evaluation: 
  * See Elasticsearch startup /usr/share/elasticsearch/bin
  * See Tomcat startup

```sh
  # Print command line usage / help
usage() {
    echo "Usage: $0 [-vdh] [-p pidfile] [-D prop] [-X prop]"
    echo "Start elasticsearch."
    echo "    -d            daemonize (run in background)"
    echo "    -p pidfile    write PID to <pidfile>"
    echo "    -h"
    echo "    --help        print command line options"
    echo "    -v            print elasticsearch version, then exit"
    echo "    -D prop       set JAVA system property"
    echo "    -X prop       set non-standard JAVA system property"
    echo "   --prop=val"
    echo "   --prop val     set elasticsearch property (i.e. -Des.<prop>=<val>)"
}

# Parse any long getopt options and put them into properties before calling getopt below
# Be dash compatible to make sure running under ubuntu works
ARGV=""
while [ $# -gt 0 ]
do
    case $1 in
      --help) ARGV="$ARGV -h"; shift;;
      --*=*) properties="$properties -Des.${1#--}"
           shift 1
           ;;
      --*) [ $# -le 1 ] && {
                echo "Option requires an argument: '$1'."
                shift
                continue
            }
           properties="$properties -Des.${1#--}=$2"
           shift 2
           ;;
      *) ARGV="$ARGV $1" ; shift
    esac
done



# Parse any command line options.
args=`getopt vdhp:D:X: $ARGV`
eval set -- "$args"

while true; do
    case $1 in
        -v)
            "$JAVA" $JAVA_OPTS $ES_JAVA_OPTS $es_parms -Des.path.home="$ES_HOME" -cp "$ES_CLASSPATH" $props \
                    org.elasticsearch.Version
            exit 0
        ;;
        -p)
            pidfile="$2"
            shift 2
        ;;
        -d)
            daemonized="yes"
            shift
        ;;
        -h)
            usage
            exit 0
        ;;
        -D)
            properties="$properties -D$2"
            shift 2
        ;;
        -X)
            properties="$properties -X$2"
            shift 2
        ;;
        --)
            shift
            break
        ;;
        *)
            echo "Error parsing argument $1!" >&2
            usage
            exit 1
        ;;
    esac
done

# Start up the service
launch_service "$pidfile" "$daemonized" "$properties"

exit $?
```


Alternative:


```sh
while [ "$1" != "" ]; do
    case $1 in
        -d | --date )           
            shift
            p_date=$1
            ;;
        -c | --continent )      
            shift
            if [ "$1" = "EU" ] || [ "$1" = "US" ]; then
                p_continent="$1"
            else
                echo "No valid cluster location. Only EU and US are allowed!"
                exit
            fi
            ;;
        -o | --outputdir)
            shift
            p_outputdir="$1"
            ;;    
        -h | --help )           
            usage
            exit
            ;;
        * )                     
            usage
            exit 1
    esac
    shift
done
```


## Extract Template name from Template URL

```sh
cut -f 6 any_configuration_20160610_112122.csv | grep  "(?<=/download/templates/(?:text|doc))/.*"
```

## Suppress output when starting a process

```sh
dashing start > /dev/null 2>&1
```

## Summing up values of a CSV file by column

```sh
awk '{s+=$1} END {print s}' mydatafile
```

## Install a Debian package
```sh
dpkg -i /home/myuser/myproject_1.0.0-SNAPSHOT_all.deb
```
