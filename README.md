# server-logging

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

4. to stop all the containers:
```
docker compose -f elk-compose.yml -f extensions/filebeat/filebeat-compose.yml down
```

5. access the kibana visualization tool at localhost:5601

# Deployment issue
The same setup needs to be deployed on mude-utilities.citg.tudelft.nl server.

The same setup is deployed on the mude-utilities.citg.tudelft.nl server at home/elk-server-logging.

The mude-utilities.citg.tudelft.nl has an nginx reverse proxy running as a docker container.

The kibana container should be accessible through the nginx reverse proxy. However, this is not the case. Accessing mude-utilities.citg.tudelft.nl/kibana redirects to the login page.

nginx and kibana container are both on the same network, and nginx can also access the kibana container; hence, the docker network settings are correct.