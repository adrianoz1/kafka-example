## Consumer groups Params
--bootstrap-server Kafka server to connect
--list List groups
--describe Describe a group
--group Group name
--reset-offsets Reset offset of topic
--topic Topic name

## Consumer group
```
podman exec -it d9a924fd7506 /opt/kafka/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic messages --group consummers
```

## Consumer groups list
```
podman exec -it d9a924fd7506 /opt/kafka/bin/kafka-consumer-groups.sh --bootstrap-server localhost:9092 --list

//result
console-consumer-75595
consummers
new-consummers
```

## Consumer group describe
```
podman exec -it d9a924fd7506 /opt/kafka/bin/kafka-consumer-groups.sh --bootstrap-server localhost:9092 --describe --group consummers


//result
GROUP           TOPIC           PARTITION  CURRENT-OFFSET  LOG-END-OFFSET  LAG             CONSUMER-ID                                                HOST            CLIENT-ID
consummers      messages        0          5               5               0               consumer-consummers-1-53f60105-9449-4f2e-abca-323165f6df19 /127.0.0.1      consumer-consummers-1
consummers      messages        1          4               4               0               consumer-consummers-1-53f60105-9449-4f2e-abca-323165f6df19 /127.0.0.1      consumer-consummers-1
consummers      messages        2          5               5               0               consumer-consummers-1-a0940385-8585-4088-86d5-8e7b0f7a6c3b /127.0.0.1      consumer-consummers-1
```