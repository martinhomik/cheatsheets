# Hive Smoothies

## Setting variables

```sql

-- Set JVM heap space to 4 GB
SET mapreduce.map.java.opts=-Xmx4G;
SET mapreduce.reduce.java.opts=-Xmx4G;
-- Set number of reduces tasks
SET mapreduce.job.reduces=120;
-- Set compression of Hive's intermediate output (between MR Jobs)
SET hive.exec.compress.intermediate=true;
-- Set Map Output compression
SET mapreduce.map.output.compress=true;
-- Set compression coded for Hive's intermediate output and for map output
SET mapreduce.map.output.compress.codec=org.apache.hadoop.io.compress.SnappyCodec;
-- Set Hive output compression
SET hive.exec.compress.output=false;
-- Setting Gzip for output compression leads to very small output files
SET mapreduce.output.fileoutputformat.compress.codec=org.apache.hadoop.io.compress.GzipCodec;
-- Set RECORD type compression for performance
SET mapreduce.output.fileoutputformat.compress.type=RECORD;


-- Set job scheduler queue name
SET mapreduce.job.queuename=slow;
-- Start reduce phase when 95% of the map phase is finished
SET mapreduce.job.reduce.slowstart.completedmaps=0.95;

-- Various performance settings also used in other projects
SET mapreduce.task.io.sort.mb=2047;
SET mapreduce.task.io.sort.factor=200;
SET mapreduce.job.reduce.slowstart.completedmaps=0.95;
SET io.file.buffer.size=131072;
SET mapreduce.reduce.shuffle.parallelcopies=40;

-- some unknown settings
set hive.input.format=org.apache.hadoop.hive.ql.io.CombineHiveInputFormat;
set hive.merge.mapfiles=true;

```

### Set Dynamic Partitioning

```sql
SET hive.exec.dynamic.partition=true;
SET hive.exec.dynamic.partition.mode=non-strict;

CREATE TABLE `mydb.mytable`(
...
	PARTITIONED BY ( 
	  `P_YEAR_UTC` STRING,
	  `P_MONTH_UTC` STRING,
	  `P_DAY_UTC` STRING,
	  `P_DAYSTRING_UTC` string COMMENT 'e.g. 2015-01-31'
    )
	STORED AS PARQUET
	TBLPROPERTIES ("parquet.compression"="SNAPPY");
	
	
	
INSERT OVERWRITE TABLE bl_oms.t_pixelbox_oms_mhomik
PARTITION ( p_year_utc
          , p_month_utc
          , p_day_utc
          , p_daystring_utc
          )
SELECT
	...
	substr(daystring_utc,1,4) as year_utc ,
	substr(daystring_utc,6,2) as month_utc ,
	substr(daystring_utc,9,2) as day_utc ,
	daystring_utc
FROM otherdb.othertable
;
```

See also: 

- [Hive Dynamic Partitioning](https://cwiki.apache.org/confluence/display/Hive/DynamicPartitions)

### Counting

```sql
-- simple count on a table
select count(*) from mydb.mytable;

-- count disting values in a column
select count(distinct mycolumn) from mydb.mytable;

```

### Show Table Description

```sql
SHOW CREATE TABLE mydb.mytable;
```

### Using Spark engine

```sql
SET hive.execution.engine=spark;
SET spark.executor.instances=48;
SET spark.executor.memory=3072m;
```

## Variable substitutions

- use ```${hivevar:UTC_YEAR}``` in scripts

## Partitions

- Drop all partitions newer than 2000-01-01
- Drop is non-recoverable

```sql
ALTER TABLE mydb.mytable DROP PARTITION (p_daystring_utc >= '2000-01-01') PURGE;
```

- Show partitions 

```sql
SHOW PARTITIONS mydb.mytable;
```