# Kafka Docker Setup

This repository provides a Docker Compose configuration to run **Apache Kafka** and **Zookeeper** using Bitnami images. Additionally, it includes **Kafdrop**, a web-based UI for monitoring Kafka topics.

## 🛠️ Features
- **Zookeeper**: Manages Kafka brokers.
- **Kafka**: A distributed event streaming platform.
- **Kafdrop**: Web UI for managing Kafka topics.

## 🚀 Quick Start

### Prerequisites
Ensure you have the following installed:
- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)

### Run the Kafka Cluster
```sh
docker-compose up -d
```

### Stop the Kafka Cluster
```sh
docker-compose down
```

## 🔗 Services & Ports
| Service  | Description | Port |
|----------|------------|------|
| **Zookeeper** | Kafka coordination service | `2181` |
| **Kafka** | Event streaming platform | `9092` (External) / `29092` (Internal) |
| **Kafdrop** | Web UI for Kafka monitoring | `9000` |

## 🧐 Access Kafka UI
Open **Kafdrop** in your browser:
```
http://localhost:9000
```

## 📌 Configuration Details
- Kafka uses **Zookeeper** for broker coordination.
- Listeners are configured for **internal (29092)** and **external (9092)** communication.
- **Kafdrop** connects to Kafka via the internal broker port.

## 📚 Useful Kafka Commands

### List Topics
```sh
docker exec -it $(docker ps --filter "name=kafka" --format "{{.ID}}") kafka-topics.sh --bootstrap-server localhost:9092 --list
```

### Create a Topic
```sh
docker exec -it $(docker ps --filter "name=kafka" --format "{{.ID}}") kafka-topics.sh --bootstrap-server localhost:9092 --create --topic my-topic --partitions 1 --replication-factor 1
```

### Produce Messages
```sh
docker exec -it $(docker ps --filter "name=kafka" --format "{{.ID}}") kafka-console-producer.sh --broker-list localhost:9092 --topic my-topic
```
(Type a message and press Enter to send.)

### Consume Messages
```sh
docker exec -it $(docker ps --filter "name=kafka" --format "{{.ID}}") kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic my-topic --from-beginning
```

## 🔄 Restart Kafka and Zookeeper
```sh
docker-compose restart kafka zookeeper
```

## 🧹 Cleanup (Remove all volumes)
```sh
docker-compose down -v
```

## 📝 License
This project is open-source and available under the [me](LICENSE).
