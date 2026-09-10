## 05 - Kafka Replication

## Objective

Learn how Kafka replication works in a multi-broker cluster.

This lab covers:
- Replication Factor
- Leader and Replica
- In-Sync Replicas (ISR)
- Broker Failure
- Leader Failover
- min.insync.replicas
- Broker recovery and ISR rejoining
- KRaft controller quorum behavior

## 1. Verify Replication Configuration
```bash
docker exec -it kafka-1 /opt/kafka/bin/kafka-topics.sh \h \
  --describe \
  --topic order-created \
  --bootstrap-server kafka-1:9092
```

# Understanding the output
- Leader - Broker currently handling reads and writes for the partition.
- Replicas - All brokers assigned to store a copy of the partition.
- ISR - Replicas that are currently in sync with the leader.
- Replication Factor 3 - Each partition has 3 copies.
- min.insync.replicas=2 - At least 2 replicas must be in sync for writes that require the configured ISR constraint.

## 2. Produce Replication Test Messages
```bash
docker exec -it kafka-1 /opt/kafka/bin/kafka-console-producer.sh \
  --topic order-created \
  --bootstrap-server kafka-1:9092 \
  --producer-property partitioner.class=org.apache.kafka.clients.producer.RoundRobinPartitioner
```

## 3. Simulate Broker Failure
Stop ```kafka-3```
```bash
docker stop kafka-3
```
Check the containers
```bash
docker ps -a
```
Describe the topic again
```bash
docker exec -it kafka-1 /opt/kafka/bin/kafka-topics.sh \h \
  --describe \
  --topic order-created \
  --bootstrap-server kafka-1:9092
```
Check the topics of before and after down the kafka-3

## 4. Verify Writes with 2 ISR

## 5. Simulate Loss of a Second Broker
```bash
docker stop kafka-1
```
```bash
docker ps -a
```
```bash
docker exec -it kafka-2 /opt/kafka/bin/kafka-topics.sh \ 
  --describe \ 
  --topic order-created \ 
  --bootstrap-server kafka-2:9092
```

## 6. Recover the failed Brokers
```bash
docker start kafka-1
docker start kafka-3
docker ps 
```

## 7. Verify ISR Recovery
```bash
docker exec -it kafka-1 /opt/kafka/bin/kafka-topics.sh \h \
  --describe \
  --topic order-created \
  --bootstrap-server kafka-1:9092
```

# Summary
THis lab demonstrated Kafka replication and broker failure recovery.
Before Failure
- Broker1 
- Broker2
- Broker3
ISR = 2,3,1
RF = 3

After Broker 3 failure
- Broker1
- Broker2
ISR = 2,1
RF = 3

After Broker 1 also failure
- Broker2
KRaft quorum lost
Requests timed out

After recovery
- Broker1
- Broker2
- Broker3
ISR = 2,1,3
RF = 3
