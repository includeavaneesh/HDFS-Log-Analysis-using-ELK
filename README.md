# Execution Steps:

Run the docker container
```
docker-compose up -d
```

Check cluster health
```
curl -X GET "localhost:9400/_cluster/health?pretty"
```

Check cluster nodes
```
curl -X GET "localhost:9400/_cat/nodes?v"
```

## Testing node failure

Stop one of the nodes (in this case, only a single node can fail to prevent brain split problem)
```
docker-compose stop es02 
```
Perform a write operation
```
curl -X POST "localhost:9400/test-index/_doc" -H 'Content-Type: application/json' -d'
{
  "test_field": "This is a test after node failure"
}'
```

Start back the server
```
docker-compose start es02
```

# Link to the dataset:
https://github.com/logpai/loghub/tree/master/HDFS#hdfs_v3_tracebench
