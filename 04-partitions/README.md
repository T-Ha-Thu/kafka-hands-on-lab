## 04 - Kafka Partitions

## Objective

Learn how Kafka partitions are created and used to distribute messages within a topic.
Understand partition assignment, partition numbers, and how messages are stored across multiple partitions.

## 1. Verify Topic Partitions
```bash
docker exec -it kafka-1 /opt/kafka/bin/kafka-topics.sh \ 
  --describe \ 
  --topic order-created \ 
  --bootstrap-server kafka-1:9092
```

## 2. Produce Messages ( Terminal 0 ) ( Round-Robin Partitioner ) 
```bash
docker exec -it kafka-1 /opt/kafka/bin/kafka-console-producer.sh \
  --topic order-created \
  --bootstrap-server kafka-1:9092 \
  --producer-property partitioner.class=org.apache.kafka.clients.producer.RoundRobinPartitioner
```

## 3. Consume Messages from Each Partition

For Partition 0 ( Terminal 1 )
```bash
docker exec -it kafka-2 /opt/kafka/bin/kafka-console-consumer.sh \h \
  --topic order-created \
  --bootstrap-server kafka-2:9092 \
  --partition 0 \
  --from-beginning
```

For Partition 1 ( Terminal 2 )
```bash
docker exec -it kafka-2 /opt/kafka/bin/kafka-console-consumer.sh \
  --topic order-created \
  --bootstrap-server kafka-2:9092 \
  --partition 1 \
  --from-beginning
```

For Partition 2 ( Terminal 3 ) 
```bash
docker exec -it kafka-2 /opt/kafka/bin/kafka-console-consumer.sh \
  --topic order-created \
  --bootstrap-server kafka-2:9092 \
  --partition 2 \
  --from-beginning
```

## Summary
In this lab,
- How Kafka topics are divided into partitions
- How to inspect topic partitions
- How to consume messages from a specific partition
- How Kafka uses message keys for partition selection
- How to use ```RoundRobinPartitioner``` to demonstrate distribution across all partitions
- How to verify messages stored in Partition 0,Paritition 1,Partition 2
