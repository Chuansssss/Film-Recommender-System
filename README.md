# Film-Recommender-System
A film recommender system project based on Item-based Collaborative Filtering Algorithm and a MapReduce structure

## Environment Initialization
This Hadoop cluster and HBase are all built on Docker. Here I assume the Docker is already installed and properly configured in our local machine.
### Hadoop cluster
We have to build the Hadoop cluster and HBase on your Docker. (Mac OSX or Linux)
```shell
$ mkdir bigdata-class2
$ cd bigdata-class2
$ sudo docker pull joway/hadoop-cluster # pull the hadoop image
$ git clone https://github.com/joway/hadoop-cluster-docker
$ sudo docker network create --driver=bridge hadoop # establish a bridge for the communication between different nodes
$ cd hadoop-cluster-docker
```
After this, we can start Hadoop in our Docker.
```shell
$ sudo ./start-container.sh
```
### HBase
Pull the image of HBase to our Docker
```shell
docker pull dajobe/hbase
```

Create the data directory for HBase
```shell
mkdir data
```

Run the image
```shell
id=$(docker run --name=hbase-docker -h hbase-docker -d -v $PWD/data:/data -p 16010:16010 -p 9095:9095 -p 8085:8085 dajobe/hbase)
```
This command will save the id of Docker image in the variable id. We can check the value of id by 
```shell
echo $id
```
Next time when we want to start HBase, we can just use the id by
```shell
docker start <id>
```
And also, here we create a mapping between localhost port 16010, 9095 and 8085 to the corresponding port in Docker. We can check it by http://127.0.0.1:8085 in our browser.

### Run our project
First we have to enter the directory of the Java source code. And then follow the commands below.
```shell
hdfs dfs -mkdir /input

hdfs dfs -put input/* /input  # upload the source input files

hdfs dfs -rm -r /dataDividedByUser

hdfs dfs -rm -r /coOccurrenceMatrix

hdfs dfs -rm -r /Normalize

hdfs dfs -rm -r /Multiplication

hdfs dfs -rm -r /Sum

cd src/main/java/

hadoop com.sun.tools.javac.Main *.java

jar cf recommender.jar *.class

hadoop jar recommender.jar Driver /input /dataDividedByUser /coOccurrenceMatrix /Normalize /Multiplication /Sum

hdfs dfs -cat /Sum/*
```
Then the result of the computation should have already been printed on the terminal. Also we can use cat command to check all the result of the middle stages.


