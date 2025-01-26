## Basic commands

### List topics
```
podman exec -it d9a924fd7506 /opt/kafka/bin/kafka-topics.sh --zookeeper zookeeper:2181 --list 
```

### Describe topic
```
podman exec -it d9a924fd7506 /opt/kafka/bin/kafka-topics.sh --describe --topic my-topic --bootstrap-server localhost:909
```