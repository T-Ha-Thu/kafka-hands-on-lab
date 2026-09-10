# 02 - Kafka Topics

## Objective

Learn how to create, list, describe, and manage Kafka topics.

## Environment

- Apache Kafka
- Docker
- 3 Kafka Brokers
- Topic: `order-created`

## 1. Create Topic
Create a topic with 3 partitions and a replication factor of 3.
```bash
docker exec -it kafka-1 /opt/kafka/bin/kafka-topics.sh \
  --create \
  --topic order-created \
  --bootstrap-server kafka-1:9092 \
  --partitions 3 \
  --replication-factor 3
```

## 2. List Topics
```bash
docker exec -it kafka-1 /opt/kafka/bin/kafka-topics.sh \
  --list \
  --bootstrap-server kafka-1:9092
```

## 3. Describe Topic
```bash
docker exec -it kafka-1 /opt/kafka/bin/kafka-topics.sh \
  --describe \
  --topic order-created \
  --bootstrap-server kafka-1:9092
```

## 4. Verify Topic Configuration
```bash
docker exec -it kafka-1 /opt/kafka/bin/kafka-configs.sh \
  --bootstrap-server kafka-1:9092 \
  --entity-type topics \
  --entity-name order-created \
  --describe
```
