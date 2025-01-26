## Kafka tests

### Execute with podman

```shell
brew install podman-compose

//start podman 
podman machine init        
podman machine start

//start using docker-compose.yml
podman-compose up -d       
```

### Test
## Copy kafka-container-id
```
podman ps
```

```shell
CONTAINER ID  IMAGE                                    COMMAND               CREATED        STATUS        PORTS                                               NAMES
d9a924fd7506  docker.io/wurstmeister/kafka:latest      start-kafka.sh        2 minutes ago  Up 2 minutes  0.0.0.0:9092->9092/tcp, 9093/tcp                    kafka_kafka_1
```
## Create a new topic
```shell
podman exec -it d9a924fd7506 /opt/kafka/bin/kafka-topics.sh --create --zookeeper zookeeper:2181 --replication-factor 1 --partitions 1 --topic my-topic
```

## Produce and consume messages
### Produce
```shell
podman exec -it d9a924fd7506 /opt/kafka/bin/kafka-console-producer.sh --broker-list localhost:9092 --topic my-topic
```

### Consume
```shell
podman exec -it d9a924fd7506 /opt/kafka/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic my-topic --from-beginning
```

## Stop and remove containers
```shell
docker-compose down
```