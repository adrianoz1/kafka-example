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