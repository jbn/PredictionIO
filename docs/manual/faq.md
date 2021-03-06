---
layout: docs
title: FAQ
---

#   Frequently Asked Questions

|

## Using Prediction.IO

### Q: How to increase Spark driver program and worker executor memory size?
In general, the Prediction.IO `bin/pio` scripts wraps around Spark's `spark-submit` 
script. You can specify a lot of Spark configurations (i.e. executor memory, cores, master
url, etc.) with it. You can supply these as pass-through arguments at the end of 
`bin/pio` command.

For example, the follow command set the Spark master to `spark://localhost:7077`
(the default url of standalone cluster) and set the executor memory to 24G.

```
$ pio run io.prediction.examples.mlc.Evaluation1 -- \
  --master spark://localhost:7077  --executor-memory 24G
```






### Q: How to increase event server JVM memory?
```
$ JAVA_OPTS=-Xmx16g bin/pio eventserver --ip 0.0.0.0 --port 7071
```


## Building Prediction.IO

### Q: How to resolve "Error: Could not find or load main class io.prediction.tools.Console" after ./make_distribution.sh"?
```
$ bin/pio app
Error: Could not find or load main class io.prediction.tools.Console
```
When PIO bumps a version, it creates another jar file with the new version number.

Delete everything but the latest pio-assembly-<VERSION>.jar in $PIO_HOME/assembly directory. For example:
  
```
PredictionIO$ cd assembly/

PredictionIO/assembly$ ls -al
total 197776
drwxr-xr-x  2 yipjustin yipjustin      4096 Nov 12 00:08 .
drwxr-xr-x 17 yipjustin yipjustin      4096 Nov 12 00:09 ..
-rw-r--r--  1 yipjustin yipjustin 101184982 Nov  5 06:05 pio-assembly-0.8.1-SNAPSHOT.jar
-rw-r--r--  1 yipjustin yipjustin 101324859 Nov 12 00:09 pio-assembly-0.8.2-SNAPSHOT.jar

PredictionIO/assembly$ rm pio-assembly-0.8.1-SNAPSHOT.jar
```

### Q: How to resolve ".......[error] (data/compile:compile) java.lang.AssertionError: assertion failed: java.lang.AutoCloseable" when ./make_distribution.sh?

Prediction.IO only support Java 7 or later. Please make sure you have the
correct Java version with the command:

```
$ javac -version
```

