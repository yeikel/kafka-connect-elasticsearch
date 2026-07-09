# Kafka Connect Elasticsearch Connector

> **This is a community fork of [confluentinc/kafka-connect-elasticsearch](https://github.com/confluentinc/kafka-connect-elasticsearch).**
>
> The main difference from the upstream project is **Elasticsearch 9 support**. The upstream connector targets older Elasticsearch versions, while this fork upgrades the Elasticsearch Java client and related dependencies to be compatible with Elasticsearch 9.x.

kafka-connect-elasticsearch is a [Kafka Connector](http://kafka.apache.org/documentation.html#connect)
for copying data between Kafka and Elasticsearch.

## Key differences from upstream

| Feature | This fork | Upstream (confluentinc) |
|---|---|---|
| Elasticsearch compatibility | 9.x (also compatible with 8.x) | 7.x / 8.x |
| Elasticsearch Java client | 8.19.x | older versions |

# Development

To build a development version you'll need a recent version of Kafka as well as a set of upstream Confluent projects, which you'll have to build from their appropriate snapshot branch. See the [FAQ](https://github.com/confluentinc/kafka-connect-elasticsearch/wiki/FAQ) for guidance on this process.

You can build kafka-connect-elasticsearch with Maven using the standard lifecycle phases.

# Configuring
## Creating an Elasticsearch user and assigning required privileges
### Create an Elasticsearch role
```
curl -u elastic:elastic -X POST "localhost:9200/_security/role/es_sink_connector_role?pretty" -H 'Content-Type: application/json' -d'
{
  "indices": [
    {
      "names": [ "*" ],
      "privileges": ["create_index", "read", "write", "view_index_metadata"]
    }
  ]
}'
```
### Create an Elasticsearch user
```
curl -u elastic:elastic -X POST "localhost:9200/_security/user/es_sink_connector_user?pretty" -H 'Content-Type: application/json' -d'
{
  "password" : "seCret-secUre-PaSsW0rD",
  "roles" : [ "es_sink_connector_role" ]
}'
```

# Contribute

- Source Code: https://github.com/yeikel/kafka-connect-elasticsearch
- Issue Tracker: https://github.com/yeikel/kafka-connect-elasticsearch/issues
- Upstream project: https://github.com/confluentinc/kafka-connect-elasticsearch
- Learn how to work with the connector's source code by reading our [Development and Contribution guidelines](CONTRIBUTING.md).


# License

This project is licensed under the [Confluent Community License](LICENSE).

