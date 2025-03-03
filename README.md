# Zephyr Consumer

## Descrição

O **Zephyr Consumer** é um microserviço desenvolvido em **Java 17** com **Spring Boot**, responsável por consumir mensagens do **Apache Kafka** e persistir os dados no **PostgreSQL**. Ele processa os eventos publicados pelo **Zephyr Producer** e garante a persistência das informações de forma eficiente.

Este repositório faz parte da plataforma **[Zephyr Platform](https://github.com/marcuslira2/zephyr-platform)**, que compara diferentes abordagens de processamento de dados com Kafka.

---

## 🚀 Funcionalidades

- Consumo de mensagens do **Kafka**.
- Processamento e persistência dos dados no **PostgreSQL**.
- Suporte a diferentes formatos de mensagens.
- Monitoramento e logging estruturado.

---

## 📌 Tecnologias Utilizadas

- **Java 17**
- **Spring Boot** (Web, Kafka, Data JPA, Config)
- **Apache Kafka**
- **PostgreSQL**
- **Docker**
- **Maven**

---

## 📂 Estrutura do Projeto

```
zephyr-consumer/
├── src/
│   ├── main/
│   │   ├── java/com/zephyr/consumer/
│   │   │   ├── config/      # Configurações do Kafka e Spring Boot
│   │   │   ├── service/     # Serviço de consumo e persistência
│   │   │   ├── repository/  # Repositório para interação com o banco
│   │   │   ├── entity/      # Modelos de dados
│   │   ├── resources/
│   │   │   ├── application.yml  # Configuração do projeto
│   ├── test/                 # Testes unitários
├── Dockerfile                # Dockerização do serviço
├── pom.xml                   # Dependências do projeto
```

---

## ⚙️ Configuração

### 📌 Variáveis de Ambiente

O `application.yml` deve ser configurado para apontar para o broker Kafka e o banco PostgreSQL:

```yaml
spring:
  kafka:
    bootstrap-servers: kafka:9092
    consumer:
      group-id: zephyr-consumer-group
      auto-offset-reset: earliest
  datasource:
    url: jdbc:postgresql://postgres:5432/kafkateste
    username: postgres
    password: postgres
    driver-class-name: org.postgresql.Driver
  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
```

Outros parâmetros podem ser ajustados conforme necessidade.

---

## 🛠️ Como Rodar o Projeto

### 🛠️ Executando Localmente

1. Clone o repositório:
   ```bash
   git clone https://github.com/marcuslira2/zephyr-consumer.git
   ```
2. Entre na pasta do projeto:
   ```bash
   cd zephyr-consumer
   ```
3. Execute o Maven para compilar e rodar:
   ```bash
   mvn spring-boot:run
   ```

### 💪 Executando com Docker

1. Compile o projeto:
   ```bash
   mvn clean package
   ```
2. Construa a imagem Docker:
   ```bash
   docker build -t zephyr-consumer .
   ```
3. Execute o contêiner:
   ```bash
   docker run --network=minha_rede -p 8081:8081 zephyr-consumer
   ```

---

## 💽 Monitoramento e Logs

Para visualizar logs do consumidor:
```bash
docker logs -f zephyr-consumer
```

Para verificar o status do consumidor no Kafka:
```bash
docker exec -it kafka kafka-consumer-groups --bootstrap-server kafka:9092 --group zephyr-consumer-group --describe
```

---

## 📄 Licença

Este projeto está sob a licença **MIT**. Sinta-se livre para usar, modificar e contribuir!

---

## 💌 Contato
Caso tenha alguma dúvida ou sugestão, entre em contato via [GitHub Issues](https://github.com/marcuslira2/zephyr-consumer/issues).

