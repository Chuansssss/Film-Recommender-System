# Film-Recommender-System
A film recommender system project based on Item-based Collaborative Filtering Algorithm and a MapReduce structure

## Environment Initialization
This Hadoop cluster and HBase are all built on Docker. Here I assume the Docker is already installed and properly configured in your local machine.

Then we have to build the Hadoop cluster and HBase on your Docker. (Mac OSX or Linux)
```shell
$ mkdir bigdata-class2
$ cd bigdata-class2
$ sudo docker pull joway/hadoop-cluster # pull the hadoop image
$ git clone https://github.com/joway/hadoop-cluster-docker # 从github上拉取相关代码
$ sudo docker network create --driver=bridge hadoop #搭建一个bridge供hadoop各节点通信
$ cd hadoop-cluster-docker
```
