## 03 - Kafka Producer & Consumer

# Objective

learn how to produce messages to a Kafka topic and consume messages from the topic.
Understand the basic message flow between Kafka Producker,Kafka Topic and Kafka Consumer.

## 1. Start Kafka Producer
```bash
docker exec -it kafka-1 /opt/kafka/bin/kafka-console-producer.sh \ 
  --topic order-created \ 
  --bootstrap-server kafka-1:9092
```
In Terminal (1)
<img width="1222" height="143" alt="2" src="https://github.com/user-attachments/assets/6c24c676-209a-4ba3-968a-97018202abd8" />

## 2. Start kafka Consumer
```bash
docker exec -it kafka-2 /opt/kafka/bin/kafka-console-consumer.sh \ 
  --topic order-created \
  --bootstrap-server kafka-2:9092 \ 
  --from-beginning
```
In Terminal (2)
<img width="1173" height="267" alt="3" src="https://github.com/user-attachments/assets/5af03fea-c7d0-4477-b98c-d15bf220fe03" />

## Message Flow

Kafka Producer
      |
      | Message
      v
order-created Topic
      |
      | Message
      v
Kafka Consumer

## Key Concepts
- Producer — Sends messages to Kafka.
- Consumer — Reads messages from Kafka.
- Topic — Logical destination where Kafka stores messages.
- Partition — Messages are stored inside topic partitions.
- --from-beginning — Reads available messages from the beginning of the partition(s).

## Verification

- Producer successfully sent messages to the order-created topic.

- Consumer successfully received messages from the topic.

- Real-time Producer → Kafka → Consumer message flow was successfully verified.
