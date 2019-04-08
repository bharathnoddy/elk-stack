# ELK on Docker
##USAGE:
-clone the directory
```
mkdir esdata   (to hold the elasticsearch data)
ELASTIC_VERSION=6.5.2 docker-compose up       (will set up the ELK stack in you host)
docker-compose down        (shutdown the stack)
```


##Components and config files :
###logstash:
./config/logstash/*  contains all the files requried by logstash container
./config/logstash/pipeline/     -  create config files for logs that needs to be processed by logstash
./config/logstash/logstash.yml  and ./config/logstash/pipeline.yml      -   logstash main configuration files

###elasticsearch:
  The other containers will only start if the health check of the elasticsearch container is healthy. If this container fails for some reason everything else will fail as well

./config/elasticsearch/elasticsearch.yml    -  main config files of elasticsearch which is mounted into the container


###kibana:
./config/kibana/kibana.yml    -  main config files of kibana which is mounted into the container


###NGINX:
  Using Nginx to enable SSL and restrict kibana access


##Curator :
consists of curator config to delete old indices more than 45 days. This can be scheduled to run once a day via cron job or some jenkins job

USAGE:
Install curator
```
pip install elasticsearch-curator
```
--Schedule this to run every day
```
##0 8 * * * root curator ./config/curator/delete_index.yml --config  ./config/curator/curator.yml
```
