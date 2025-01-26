## Topic Params

--topic Topic name
--bootstrap-server Kafka server to connect
--partitions Number of partitions the topic should have
--replication-factor Replication factor of the topic
--create Creates a new topic
--alter Alters the number of partitions, replicas, and other configs
--delete Deletes a topic
--describe Shows topic details
--if-not-exists Only alters the topic if it does not exist
--list Lists all topics


### Example create a new topic
```
podman exec -it d9a924fd7506 /opt/kafka/bin/kafka-topics.sh --create --zookeeper zookeeper:2181 --replication-factor 1 --partitions 1 --topic test-topic
```

### List all topics
```
podman exec -it d9a924fd7506 /opt/kafka/bin/kafka-topics.sh --bootstrap-server 127.0.0.1:9092 --list
```

### Create a new topic
```
podman exec -it d9a924fd7506 /opt/kafka/bin/kafka-topics.sh --bootstrap-server 127.0.0.1:9092 --topic new-topic --create --partitions 3 --replication-factor 1
```

```
podman exec -it d9a924fd7506 /opt/kafka/bin/kafka-topics.sh --bootstrap-server 127.0.0.1:9092 --list
__consumer_offsets
my-topic
new-topic
test-topic
```

### Describe a topic
```
podman exec -it d9a924fd7506 /opt/kafka/bin/kafka-topics.sh --bootstrap-server 127.0.0.1:9092 --topic new-topic --describe

//result
Topic: new-topic        TopicId: uewjJBuZStiFwNg4yGZzrA PartitionCount: 3      ReplicationFactor: 1    Configs: segment.bytes=1073741824
        Topic: new-topic        Partition: 0    Leader: 1001    Replicas: 1001 Isr: 1001
        Topic: new-topic        Partition: 1    Leader: 1001    Replicas: 1001 Isr: 1001
        Topic: new-topic        Partition: 2    Leader: 1001    Replicas: 1001 Isr: 1001
```

### Alter topic
```
podman exec -it d9a924fd7506 /opt/kafka/bin/kafka-topics.sh --bootstrap-server 127.0.0.1:9092 --topic new-topic --alter --partitions 4

//describe
podman exec -it d9a924fd7506 /opt/kafka/bin/kafka-topics.sh --bootstrap-server 127.0.0.1:9092 --topic new-topic --describe
Topic: new-topic        TopicId: uewjJBuZStiFwNg4yGZzrA PartitionCount: 4      ReplicationFactor: 1    Configs: segment.bytes=1073741824
        Topic: new-topic        Partition: 0    Leader: 1001    Replicas: 1001 Isr: 1001
        Topic: new-topic        Partition: 1    Leader: 1001    Replicas: 1001 Isr: 1001
        Topic: new-topic        Partition: 2    Leader: 1001    Replicas: 1001 Isr: 1001
        Topic: new-topic        Partition: 3    Leader: 1001    Replicas: 1001 Isr: 1001
```