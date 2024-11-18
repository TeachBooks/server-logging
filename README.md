# server-logging

The server-logging setup uses the elk stack tool for ingesting logs and visualising the logs. The elk stack tool consists of the following components:
1. elasticsearch
2. kibana
3. logstash
4. filebeat

In brief, this is how the following components work:
1. Filebeat collects logs from the log files.
2. Filebeat sends logs to Logstash, where they are parsed.
3. Logstash forwards structured logs to Elasticsearch.
4. Elasticsearch stores and indexes the logs.
5. Kibana visualizes the indexed data as dashboards, enabling monitoring and analysis.

# Running server-logging setup locally

Before running the docker containers locally, you have to populate the the directory `nginx/logs` with the log files.

The log files for the `mude.citg.tudelft.nl` server are located at the directory `/var/log/nginx`. This directory contains the following files:

1. access.log.*
2. access.log.gz.*

Below is a description of how to run the ELK stack tool locally and start visualising the logs.

1. clone the repository

2. initialize the Elasticsearch users and groups required by docker-elk by executing the following command:
```
docker compose -f elk-compose.yml up setup
```

3. If everything went well and the setup completed without error, start the other stack components:
```
docker compose -f elk-compose.yml -f extensions/filebeat/filebeat-compose.yml up -d
```

4. access the kibana visualization tool at localhost:5601

5. to stop all the containers:
```
docker compose -f elk-compose.yml -f extensions/filebeat/filebeat-compose.yml down
```

# Deployment issue
The same setup needs to be deployed on mude-utilities.citg.tudelft.nl server.

The same setup is deployed on the mude-utilities.citg.tudelft.nl server at home/elk-server-logging.

The mude-utilities.citg.tudelft.nl has an nginx reverse proxy running as a docker container.

The kibana container should be accessible through the nginx reverse proxy. However, this is not the case. Accessing mude-utilities.citg.tudelft.nl/kibana redirects to the login page.

nginx and kibana container are both on the same network, and nginx can also access the kibana container; hence, the docker network settings are correct.