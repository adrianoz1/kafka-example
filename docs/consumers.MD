## Consumer Params
--topic Topic name
--bootstrap-server Kafka server to connect
--from-beginning Reads from the beginning if no prior read has occurred
--group The consumer group
--isolation-level read_committed to read committed messages / read_uncommitted to read all messages (default)
--offset The offset from which to start reading messages. Can also be: earliest (from the beginning) or latest (from the end, default)
--partition The partition to read messages from. Starts from the end unless --offset is specified

## Consumer connect with --from-beginning
```podman exec -it d9a924fd7506 /opt/kafka/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic messages --from-beginning

//result
message 2
message 1
message 3
```

## Consumer different partition of same server
```
podman exec -it d9a924fd7506 /opt/kafka/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic messages --partition 1 --offset 0
message 1
```