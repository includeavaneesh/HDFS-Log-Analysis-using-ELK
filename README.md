docker-compose up -d

curl -X GET "localhost:9400/_cluster/health?pretty"

curl -X PUT "localhost:9400/_all/_settings" -H 'Content-Type: application/json' -d'
{
  "index": {
    "number_of_replicas": 2
  }
}'

curl -X GET "localhost:9400/_cat/nodes?v"

curl -X GET "localhost:9200/_cluster/health?pretty"

docker-compose stop es02

curl -X POST "localhost:9400/test-index/_doc" -H 'Content-Type: application/json' -d'
{
  "test_field": "This is a test after node failure"
}'

docker-compose start es02