# Kowl
Kowl is a Web UI for Apache Kafka that allows exploring messages, consumers, configurations and more with a focus on a good UI & UX.

### Support Apple M1

### Quick Start

Do you just want to test Kowl against one of your Kafka clusters without spending too much time on the test setup? Here are some docker commands that allow you to run it locally against an existing Kafka cluster:

#### Kafka is running locally

Since Kowl runs in it's own container (which has it's own network scope), we have to use `host.docker.internal` as bootstrap server. That DNS resolves to the host system's ip address. However since Kafka brokers send a list of all brokers' DNS when a client has connected, you have to make sure your advertised listener is connected accordingly, e.g.: `PLAINTEXT://host.docker.internal:9092`

```shell
docker run -p 8080:8080 -e KAFKA_BROKERS=host.docker.internal:9092 rsmnarts/kowl
```

Docker supports the `--network=host` option only on Linux. So Linux users use `localhost:9092` as advertised listener and use the host network namespace instead. Kowl will then be ran as it would be executed on the host machine.

```shell
docker run --network=host -p 8080:8080 -e KAFKA_BROKERS=localhost:9092 rsmnarts/kowl
```

#### Kafka is running remotely

Protected via SASL_SSL and trusted certificates (e.g. Confluent Cloud):

```shell
docker run -p 8080:8080 -e KAFKA_BROKERS=pkc-4r000.europe-west1.gcp.confluent.cloud:9092 -e KAFKA_TLS_ENABLED=true -e KAFKA_SASL_ENABLED=true -e KAFKA_SASL_USERNAME=xxx -e KAFKA_SASL_PASSWORD=xxx rsmnarts/kowl
```
