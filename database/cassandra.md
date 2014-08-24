# Apache Cassandra

## Requirements
  * Java 7 64bits Server Edition
  * Python 2.5+ (Cassandra Tools)
  * Cassandra Cluster Manager (CCM)

## Installation
```sh
# Install Java jre 7u67
sudo rm -rf /usr/lib/jvm
sudo mkdir /usr/lib/jvm
sudo tar -xzf server-jre-7u67-linux-x64.tar.gz -C /usr/lib/jvm
sudo update-alternatives --install "/usr/bin/java" "java" "/usr/lib/jvm/jdk1.7.0_40/bin/java" 1
sudo update-alternatives --set java /usr/lib/jvm/jdk1.7.0_40/bin/java

# Install JNA
sudo apt-get install libjna-java

# Download latest Apache Cassandra (DataStax Comunity Edition)
wget http://downloads.datastax.com/community/dsc.tar.gz

# Untar
tar -xzf dsc.tar.gz
```

## Package Installation Default Folder
```sh
/var/lib/cassandra #=> Data directories
/var/log/cassandra #=> Log directory
/var/run/cassandra #=> Runtime files
/usr/share/cassandra #=> Environment settings
/usr/share/cassandra/lib #=> JAR files
/usr/bin #=> Binary files
/usr/sbin
/etc/cassandra #=> Configuration files
/etc/init.d #=> Service startup script
/etc/security/limits.d #=> Cassandra user limits
/etc/default
```
## cassandra.yaml
```sh
cluster_name (default: 'Test Cluster')
# All nodes in a cluster must have the same value.

listen_address (default: localhost)
# IP address or hostname other nodes uset to connect to this node

commitlog_directory (default: /var/lib/cassandra/commitlog)
# Best practice to mount on a separate disk in production (unless SSD)

data_file_directories (default: /var/lib/cassandra/data)
# Storage directory for data tables (SSTables)

saved_caches_directory (default: /var/lib/cassandra/saved_caches)
# Storage directory for key caches and row caches

rpc_address / rpc_port (default: localhost / 9|60)
# listen address / port for Thrift client connections

native_transport_port (default: 9042)
# listen address for Native CQL Driver binary protocol
```

## cassandra-env.sh
```sh
# JVM Heap Size settings
MAX_HEAP_SIZE="1024M"
# Maximum recommended in production is currently 8G due to current limitations in Java garbage collection
# System Memory | Heap Size
# ------------------------------------
# < 2GB         | 1/2 of system memory
# 2GB to 4GB    | 1GB
# > 4GB         | 1/4 system memory, but not more than 8GB

HEAP_NEWSIZE="256M" 
# Generally set to 1/4 of MAX_HEAP_SIZE
```

## log4j-server.properties
```sh
# Cassandra system.log location
# Default location: /var/log/cassandra/system.log
# system.log is numerically renamed as it grows over time

# TRACE > DEBUG > INFO > WARN > ERROR > FATAL
# Default logging level is INFO

# Configuring log level
# cassandra/conf/log4j-server.properties
log4j.rootLogger=INFO,stdout,R

# Log location settings
# cassandra/conf/log4j-server.properties
log4j.appender.R.File=/var/log/cassandra/system.log
```
## Cassandrsa  Start and Stop
```sh
cd cassandra/bin
cassandra <options>
# start Cassandra in foreground (default is background process)
-f
# Log process ID in named file; useful to stop Cassandra by PID
-p <filename>
# print the version and exit
-v
# Pass a startup parameter (see documentation)
-D <parameter>

# Start a Cassandra instance - foreground
bin/cassandra -f
# Start a Cassandra instance - background, with PID
bin/cassandra -p PID
# Start a package insall instance
sudo service cassandra start

# Stop Cassandra
# Foreground
ctrl + c
# Background
ps ax | grep cassandra
kill <pid>
# Package
sudo service cassandra stop
```

## Cassandra logs
```sh
# System log location set by configuration
install/conf/log4j-server.properties

# System.log
# system state log file, duplicates stdout, configurable by logging level

# CommitLog
# table-specific files used during INSERT and UPDATE operations
```

## Cassandra Cluster Manager (CCM)
```sh
# Created and manages multi-node clusters on a local machine
# Useful for configuring development and test clusters
# NOT used for configuring production clusters

# Open Source utility
# Created by Sylvain Lebresne of DataStax
# Source code is available at https://github.com/pcmanus/ccm
# Requires Python 2.7+, PyYAML, Ant

# Use CCM
# CCM may target a cluster or its nodes
# One cluster is always the current default for cluster commands
ccm [cluster command] [options]
# Nodes are automatically named node1, node2, node3, etc...
ccm [node name] [node command] [options]
# ccm -help to list all comands
# ccm [command] -help to list help and options for a specific command

# CCM supports over 40 commands, including
create #=> create a new cluster using specified Cassandra version
list #=> display list of local clusters managed by CCM
populate #=> add n nodes to current empty cluster using default options
add #=> add node to current cluster
start #=> start all nodes in current cluster
status #=> display up/down status for each node in specified cluster

# CCM commands
------------------------------------------------------------------------------
create      add         populate    list        switch      status
remove      liveset     clear       start       stop        flush
compact     stress      updateconf  updatelog4j cli         setdir
bulkload    setlog      scrub       show        remove      ring
flush       drain       cleanup     repair      scrub       shuffle
stablesplit decommision json        cqlsh       setdir      version
------------------------------------------------------------------------------

ccm create cluster1 --cassandra-version 1.2.15
ccm create cluster2 --cassandra-version 2.0.6
ccm list
ccm populate --nodes 3
ccm start
ccm status
ccm node2 stop
ccm status

git clone https://github.com/pcmanus/ccm.git
cd ccm/
sudo ./setup.py install
cd ..
wget https://bootstrap.pypa.io/ez_setup.py
sudo python ez_setup.py 
sudo easy_install pyYaml
sudo easy_install six

sudo mkdir -p /usr/local/ant
sudo tar -xzf apache-ant-1.9.4-bin.tar.gz -C /usr/local/ant
export ANT_HOME=/usr/local/ant/apache-ant-1.9.4/
export JAVA_HOME=/usr/lib/jvm/jdk1.7.0_67
export PATH=${PATH}:${ANT_HOME}/bin

ccm create demo_1node -v 2.0.1 -n 1 -s -d

# CCM Folder
~/.ccm

ccm create demo_3node -v 2.0.7
ccm populate -n 2
ccm node2 show
ccm add node3 -i 127.0.0.3 -j 7300
ccm start
ccm node2 stop
```

## CQL
```sh
# Cassandra Query Language
# Primary interface to the Cassandra DBMS:cqlsh, DevCenter, native drivers
# Modeled after Structured Query Language (SQL) for familiarity

# Data definition and manipulation language (DDL and DML)
CREATE      ALTER       GRANT       REVOKE      DROP        USE
TABLE       INDEX       USER        TRIGGER     KEYSPACE
SELECT      INSERT      UPDATE      DELETE      TRUNCATE    BATCH

# Data types
blob, boolean, decimal, double, float, int, text, varchar
timestamp, uuid, timeuuid, counter
set, list, map

# No table joins => Query driven design
```

## cqlsh
```sh
# An interactive, command-line utility for executing CQL statements
# Interacts with its local Cassandra instance, by default
# Supports tab completion for commands

# /bin/cqlsh
cqlsh [options] [host [port]]

-k [keyspace] # open cqlsh to interact with a specified keyspace
-f [file_name] # execute commands in file_name then exit
-u [user] -p [password] # authenticate with credentials
-h # display online help for cqlsh

# cqlsh supports
# CQL DDL and DML commands for schema definition and data manipulation
# CQL shell commands to support CQL use

# CQL is a Cassandra capability, not restricted to cqlsh
# CQL shell commands may only be used with cqlsh

Commands    |Description
----------------------------------------------------------------------
CAPTURE     |Captures command output and appends it to a file
CONSISTENCY |Shows the current consistency level, or given a level, sets it
COPY        |Imports and exports CSV (comma-separated values) data
DESCRIBE    |Provides information about a Cassandra cluster or data objects
EXIT        |Terminates cqlsh
SHOW        |Shows the Cassandra version, host, or data type assumptions
SOURCE      |Executes a file containing CQL statements
TRACING     |Enables or disables request tracing

bin/cqlsh
EXIT;

ccm node2 cqlsh

HELP;
HELP SELECT;

# SOURCE: load and execute an external CQL file
cqlsh> HELP SOURCE;
SOURCE '<file>';


# SHOW: display version, host, or session information
cqlsh>HELP SHOW;
SHOW VERSION;
SHOW HOST;
SHOW SESSION <sessionid>;

# DESCRIBE: display information about a specified CQL artifact
cqlsh>HELP DESCRIBE;
DESCRIBE KEYSPACE;
DESCRIBE KEYSPACE [<keyspacename>];
DESCRIBE TABLES;
DESCRIBE TABLE <tablename>;
DESCRIBE CLUSTER;
DESCRIBE [FULL] SCHEMA;

```


















