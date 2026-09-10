# 01 - Kafka Cluster

## Objective

Deploy and verify a 3-broker Apache Kafka cluster using Docker Compose.

## Architecture

```text
                    Kafka Cluster

        ┌──────────┐  ┌──────────┐  ┌──────────┐
        │ Kafka-1  │  │ Kafka-2  │  │ Kafka-3  │
        │ Broker 1 │  │ Broker 2 │  │ Broker 3 │
        └──────────┘  └──────────┘  └──────────┘
              │             │             │
              └─────────────┼─────────────┘
                            │
                       Kafka Clients

```
## 1. Start Kafka Cluster
```
docker compose up -d
```

## 2. Check Running Containers
```
docker compose ps
```

## 3. Check Container Logs
```
docker logs kafka-1
docker logs kafka-2
docker logs kafka-3
```

## 4. Verify Kafka Broker Connectivity
```
docker exec -it kafka-1 /opt/kafka/bin/kafka-broker-api-versions.sh --bootstrap-server kafka-1:9092
```

## 5. Check Kafka Cluster
```
docker exec -it kafka-1 /opt/kafka/bin/kafka-metadata-quorum.sh \
  --bootstrap-server kafka-1:9092 \
  describe --status
```

## 6. Check kafka Processes
```
docker exec -it kafka-1 ps aux
```

## 7. Check Kafka Port
```
docker exec -it kafka-1 \
  bash -c 'nc -zv kafka-1 9092'
```

## 8. Stop Kafka Cluster
```
docker compose down
```

## 9. Restart kafka Cluster
```
docker compose up -d
docker compose ps
```

## Verification Checklist
- Kafka containers are running
- All 3 brokers are reachable
- Kafka broker API is responding
- Kafka cluster metadata is available
- Kafka logs can be inspected

## Key Concepts
- Kafka Cluster
- Kafka Broker
- Bootstrap Server
- Controller
- KRaft
- Cluster ID
- Broker ID
- Replication
- Fault Tolerance

