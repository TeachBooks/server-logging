# server-logging

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
