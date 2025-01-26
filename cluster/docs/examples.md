## Commands cluster

### Init cluster
```
podman-compose up -d
podman ps

CONTAINER ID  IMAGE                                    COMMAND               CREATED         STATUS         PORTS                                               NAMES
d6d9e4b2885b  docker.io/wurstmeister/zookeeper:latest  /bin/sh -c /usr/s...  26 seconds ago  Up 26 seconds  0.0.0.0:2181->2181/tcp, 22/tcp, 2888/tcp, 3888/tcp  cluster_zookeeper_1
86759d7d3e9c  docker.io/wurstmeister/kafka:latest      start-kafka.sh        26 seconds ago  Up 26 seconds  0.0.0.0:9092->9092/tcp, 0.0.0.0:29092->29092/tcp    cluster_kafka-1_1
b7e1dfb6df8a  docker.io/wurstmeister/kafka:latest      start-kafka.sh        25 seconds ago  Up 26 seconds  0.0.0.0:9093->9093/tcp, 0.0.0.0:29093->29093/tcp    cluster_kafka-2_1
0fc28614472f  docker.io/wurstmeister/kafka:latest      start-kafka.sh        25 seconds ago  Up 26 seconds  0.0.0.0:9094->9094/tcp, 0.0.0.0:29094->29094/tcp    cluster_kafka-3_1
```

### Create topic
```
podman exec -it 86759d7d3e9c /opt/kafka/bin/kafka-topics.sh --bootstrap-server 127.0.0.1:9092 --topic messages --create --partitions 3 --replication-factor 3

//describe
podman exec -it 86759d7d3e9c /opt/kafka/bin/kafka-topics.sh --bootstrap-server 127.0.0.1:9092 --topic messages --descri
be


 Topic: messages Partition: 0    Leader: 3       Replicas: 3,2,1 Isr: 3,2,1
        Topic: messages Partition: 1    Leader: 1       Replicas: 1,3,2 Isr: 1,3,2
        Topic: messages Partition: 2    Leader: 2       Replicas: 2,1,3 Isr: 2,1,3
```