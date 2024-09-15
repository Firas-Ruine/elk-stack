
# Elastic Stack (ELK) Docker Setup 🚀

![Elastic Stack](https://img.shields.io/badge/Elastic-Stack-005571?logo=elasticsearch&logoColor=white)
![Docker Compose](https://img.shields.io/badge/Docker-Compose-2496ED?logo=docker&logoColor=white)

This setup uses **Elasticsearch**, **Kibana**, **Logstash**, **Metricbeat**, and **Filebeat** to run a full-featured Elastic Stack with Docker. It is designed to be run locally and provides secure SSL communication between services using self-generated certificates.

## ⚙️ Setup Overview

This repository includes a `docker-compose.yml` configuration to quickly spin up:

- **Elasticsearch** 🟠
- **Kibana** 📊
- **Logstash** 📜
- **Metricbeat** 📈
- **Filebeat** 📂

## 🏗️ Prerequisites

Make sure you have the following installed:

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)

## 📄 Setup Instructions

### Step 1: Clone the Repository

```bash
git clone https://github.com/Firas-Ruine/elk-stack
cd elk-stack
```

### Step 2: Configure Environment Variables

Create a `.env` file or modify the existing one with your custom configuration. Example:

```bash
# Password for 'elastic' user
ELASTIC_PASSWORD=your_elastic_password

# Password for 'kibana_system' user
KIBANA_PASSWORD=your_kibana_password

# Stack version
STACK_VERSION=8.7.1
```

### Step 3: Run the Stack

```bash
docker-compose up -d
```

This will launch all the services and handle SSL certificate generation. To monitor service health:

```bash
docker-compose ps
```

### Step 4: Access the Services

- **Elasticsearch**: [http://localhost:9200](http://localhost:9200) (Basic Auth required)
- **Kibana**: [http://localhost:5601](http://localhost:5601)

## 🔑 Environment Variables

| Variable                  | Description                              |
|----------------------------|------------------------------------------|
| `ELASTIC_PASSWORD`         | Password for the `elastic` superuser     |
| `KIBANA_PASSWORD`          | Password for `kibana_system` user        |
| `STACK_VERSION`            | Version of the Elastic Stack             |
| `CLUSTER_NAME`             | Name of the Elasticsearch cluster        |
| `ES_PORT`                  | Port for exposing Elasticsearch API      |
| `KIBANA_PORT`              | Port for exposing Kibana                 |
| `ENCRYPTION_KEY`           | Encryption key for Kibana                |
| `ES_MEM_LIMIT`             | Memory limit for Elasticsearch container |
| `KB_MEM_LIMIT`             | Memory limit for Kibana container        |

## 🛠️ Service Details

### Elasticsearch

Elasticsearch is the core component of the Elastic Stack, providing powerful full-text search and analytics capabilities. The container setup ensures:

- SSL is enabled between services
- Memory is locked for optimal performance
- Authentication via `elastic` user with basic security

### Kibana

Kibana allows you to visualize Elasticsearch data through a web interface. This setup includes:

- Secure communication with Elasticsearch
- Customizable dashboard for your data insights

### Logstash

Logstash collects, parses, and stores logs from various sources. It forwards logs to Elasticsearch for indexing.

### Beats

- **Metricbeat** monitors your Docker containers, system metrics, and services like Elasticsearch and Kibana.
- **Filebeat** collects log files and forwards them to Logstash or Elasticsearch.

## 📦 Volumes & Data Persistence

| Volume             | Description                                 |
|--------------------|---------------------------------------------|
| `certs`            | Stores the SSL certificates                 |
| `esdata01`         | Data storage for Elasticsearch              |
| `kibanadata`       | Persistent storage for Kibana data          |
| `logstashdata01`   | Persistent storage for Logstash data        |
| `filebeatdata01`   | Persistent storage for Filebeat data        |
| `metricbeatdata01` | Persistent storage for Metricbeat data      |


## 📊 Visualizing Data

Once everything is up and running, you can visualize your data in Kibana. Navigate to the **Discover** section, where you can search and analyze your indexed data.

## 📖 References

- [Elasticsearch Documentation](https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html)
- [Kibana Documentation](https://www.elastic.co/guide/en/kibana/current/index.html)
- [Logstash Documentation](https://www.elastic.co/guide/en/logstash/current/index.html)
- [Beats Documentation](https://www.elastic.co/guide/en/beats/libbeat/current/index.html)

## 🎯 Notes

- Make sure your system has enough resources to run the stack (4GB+ of RAM is recommended).
- To tear down the stack, run:

  ```bash
  docker-compose down -v
  ```

---

Enjoy using the Elastic Stack with Docker! 🎉
