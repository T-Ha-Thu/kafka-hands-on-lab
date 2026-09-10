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

<img width="1630" height="211" alt="1" src="https://github.com/user-attachments/assets/38515689-3c55-471c-94ee-b77a91a9289f" />

## 2. Produce Messages ( Terminal 0 ) ( Round-Robin Partitioner ) 
```bash
docker exec -it kafka-1 /opt/kafka/bin/kafka-console-producer.sh \
  --topic order-created \
  --bootstrap-server kafka-1:9092 \
  --producer-property partitioner.class=org.apache.kafka.clients.producer.RoundRobinPartitioner
```

<img width="1065" height="220" alt="4" src="https://github.com/user-attachments/assets/350fb64a-1fcb-476c-84e9-11b193a77ac3" />

## 3. Consume Messages from Each Partition

For Partition 0 ( Terminal 1 )
```bash
docker exec -it kafka-2 /opt/kafka/bin/kafka-console-consumer.sh \h \
  --topic order-created \
  --bootstrap-server kafka-2:9092 \
  --partition 0 \
  --from-beginning
```
<img width="1082" height="316" alt="partition0" src="https://github.com/user-attachments/assets/88aee5c9-9785-4e59-a93c-e31a3651c860" />

For Partition 1 ( Terminal 2 )
```bash
docker exec -it kafka-2 /opt/kafka/bin/kafka-console-consumer.sh \
  --topic order-created \
  --bootstrap-server kafka-2:9092 \
  --partition 1 \
  --from-beginning
```
<img width="1056" height="337" alt="partition1" src="https://github.com/user-attachments/assets/eaa8da24-43cc-4d2c-a333-85697cdf3e25" />

For Partition 2 ( Terminal 3 ) 
```bash
docker exec -it kafka-2 /opt/kafka/bin/kafka-console-consumer.sh \
  --topic order-created \
  --bootstrap-server kafka-2:9092 \
  --partition 2 \
  --from-beginning
```
<img width="1052" height="532" alt="partition2" src="https://github.com/user-attachments/assets/c9b04dfd-2fbb-4504-98c3-94ea9d0f8c3b" />

## Summary
In this lab,
- How Kafka topics are divided into partitions
- How to inspect topic partitions
- How to consume messages from a specific partition
- How Kafka uses message keys for partition selection
- How to use ```RoundRobinPartitioner``` to demonstrate distribution across all partitions
- How to verify messages stored in Partition 0,Paritition 1,Partition 2
