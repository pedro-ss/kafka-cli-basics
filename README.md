Um repositório para prática de comandos básicos do kafka usando uma imagem docker

# Comandos no Apache Kafka CLI
## no Docker

para criar os containers:
```
docker-compose up -d
```

acessando o container kafka:
```
docker exec -it kafka bash
```

parando o kafka e o zookeeper:
```
docker-compose down -v
```

exibindo a versão do broker kafka:
```
./usr/bin/kafka-broker-api-versions --bootstrap-server
localhost:9092 --version
```

## tópicos

criando um tópico no kafka:
```
./usr/bin/kafka-topics --zookeeper zookeeper:2181 --create --topic
my-first-topic --partitions 3 --replication-factor 1
```

criando tópico, caso não exista:
```
./usr/bin/kafka-topics --zookeeper zookeeper:2181 --create --topic
my-first-topic --partitions 3 --replication-factor 1 --if-not-exists
```

listando tópicos no kafka:
```
./usr/bin/kafka-topics --zookeeper zookeeper:2181 --list
```

listando tópicos excluíndo tópicos internos:
```
./usr/bin/kafka-topics --zookeeper zookeeper:2181 --list --exclude-
internal
```

exibe os detalhes do tópico kafka:
```
./usr/bin/kafka-topics --zookeeper zookeeper:2181 --topic my-first-
topic --describe
```

aumentando o número de partições de um tópico:
```
./usr/bin/kafka-topics --zookeeper zookeeper:2181 --alter --topic
my-first-topic --partitions 5
```

alterando a retenção de um tópico kafka:
```
./usr/bin/kafka-configs --zookeeper zookeeper:2181 --alter --entity-
type topics --entity-name my-first-topic --add-config
retention.ms=259200000
```
obs.: 259200000 ms = 3 dias

limpar tópicos no kafka:
```
./usr/bin/kafka-configs --zookeeper zookeeper:2181 --alter --entity-
type topics --entity-name my-first-topic --add-config
retention.ms=1000
```
aguarda um minuto e então:
```
./usr/bin/kafka-configs --zookeeper zookeeper:2181 --alter --entity-
type topics --entity-name my-first-topic --delete-config
retention.ms
```

deletar tópico kafka:
```
./usr/bin/kafka-topics --zookeeper zookeeper:2181 --delete --topic
my-first-topic
```

### Producers

produzir uma mensagem em um tópico kafka:
```
./usr/bin/kafka-console-producer --broker-list localhost:9092 --
topic my-first-topic
```

produzir uma mensagem em um tópico kafka a partir de um arquivo:

```
./usr/bin/kafka-console-producer --broker-list localhost:9092 --
topic my-first-topic < topic-input.txt
```

produzir mensagens no kafka com chave e valor:
```
./usr/bin/kafka-console-producer --broker-list localhost:9092 --
topic some-topic --property parse.key=true --property
key.separator=*
```

### Consumer

consumindo um tópico kafka:
```
./usr/bin/kafka-console-consumer --bootstrap-server localhost:9092 -
-topic my-first-topic
```
consumindo um tópico kafka e exibindo chave e valor::
```
./usr/bin/kafka-console-consumer --bootstrap-server localhost:9092 \
--topic some-topic \
--formatter kafka.tools.DefaultMessageFormatter \
--property print.key=true \
--property print.value=true
```
consumindo um tópico kafka do início:
```
./usr/bin/kafka-console-consumer --bootstrap-server localhost:9092 -
-topic my-first-topic --from-beginning
```
