# server-logging

Below is a description of how to run the ELK stack tool locally and start visualising the logs.

1. clone the repository
2. create an nginx/logs directory in the root directory. the `nginx/logs` directory would contain the log files.

### How to run the docker container
initialize the Elasticsearch users and groups required by docker-elk by executing the following command:
```
docker compose -f elk-compose.yml up setup
```

If everything went well and the setup completed without error, start the other stack components:
```
docker compose -f elk-compose.yml -f extensions/filebeat/filebeat-compose.yml up -d
```

to stop all the containers:
```
docker compose -f elk-compose.yml -f extensions/filebeat/filebeat-compose.yml down
```

access the kibana visualization tool at localhost:5601