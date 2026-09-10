# Apache Kafka Hands-On Lab

A practical Apache Kafka laboratory using Docker.

## Lab Objectives

- Understand Kafka architecture
- Deploy a Kafka cluster
- Create and manage topics
- Understand partitions
- Understand replication
- Work with producers and consumers
- Understand consumer groups
- Practice Kafka CLI commands
- Understand Kafka in microservices architecture

## Lab Structure

1. Kafka Cluster
2. Kafka Topics
3. Producer & Consumer
4. Partitions
5. Replication
6. Consumer Groups
7. Kafka CLI
8. Kafka with Microservices

## Architecture

```text
                    Kafka Cluster

        ┌──────────┐  ┌──────────┐  ┌──────────┐
        │ Kafka-1  │  │ Kafka-2  │  │ Kafka-3  │
        │ Broker 1 │  │ Broker 2 │  │ Broker 3 │
        └─────┬────┘  └────┬─────┘  └────┬─────┘
              │             │             │
              └─────────────┼─────────────┘
                            │
                     Kafka Topics
                            │
                    ┌───────┴───────┐
                    │               │
                Producer         Consumer
