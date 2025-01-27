## Description
examples with kafka connect and elastic search

## Containers init
```
podman-compose up -d
```

# Elastic
## Test elastic connect
```
curl http://localhost:9200
{
  "name" : "f901f709f38f",
  "cluster_name" : "docker-cluster",
  "cluster_uuid" : "gmE_RYYvSN-s-4Vv1bKosw",
  "version" : {
    "number" : "7.10.2",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "747e1cc71def077253878a59143c1f785afa92b9",
    "build_date" : "2021-01-13T04:42:47.157277Z",
    "build_snapshot" : false,
    "lucene_version" : "8.7.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
```

## Insert index
`curl -X PUT "127.0.0.1:9200/myindex?pretty"`

```
{
  "acknowledged" : true,
  "shards_acknowledged" : true,
  "index" : "myindex"
}
```

### Insert value to index
`curl -H 'Content-Type: application/json' -XPUT 127.0.0.1:9200/myindex/_doc/1010 -d '{ "name" : "student", "subject" : "kafka", "year" : "2020" }'`

```
//response 
{"_index":"myindex","_type":"_doc","_id":"1010","_version":1,"result":"created","_shards":{"total":2,"successful":1,"failed":0},"_seq_no":0,"_primary_term":1}
```

### Get value index
`curl -XGET '127.0.0.1:9200/myindex/_search?pretty'`

```
//response
{
  "took" : 27,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 1,
      "relation" : "eq"
    },
    "max_score" : 1.0,
    "hits" : [
      {
        "_index" : "myindex",
        "_type" : "_doc",
        "_id" : "1010",
        "_score" : 1.0,
        "_source" : {
          "name" : "student",
          "subject" : "kafka",
          "year" : "2020"
        }
      }
    ]
  }
}
```

```
curl -X POST http://localhost:8083/connectors -H 'Content-Type: application/json' -d \
'{
"name": "elasticsearch-sink",
  "config": {
    "connector.class": "io.confluent.connect.elasticsearch.ElasticsearchSinkConnector",
    "tasks.max": "1",
    "topics": "elastic",
    "connection.url": "http://localhost:9200",
    "type.name": "log",
    "key.ignore": "true",
    "schema.ignore": "true",
    "schemas.enable": "false",
    "transformers": "addSuffix",
    "transformers.addSuffix.type": "org.apache.kafka.connect.transforms.RegexRouter",
    "transformers.addSuffix.regex": "elastic.*",
    "transformers.addSuffix.replacement": "meuindice"
   }
}'
```