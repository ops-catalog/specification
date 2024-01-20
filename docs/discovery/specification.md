A discovery configuration has the type attribute which tells us the engine name that will be able to process it.
The instance attribute contains a list of engine instances to scout for resources.

The majority of the information about all engines can be held in a grand total of these five properties under options attribute:

|Attribute|Description|
|---|---|
|host|the server address|
|port|port to connect to|
|username|username for auth|
|password|password for auth|
|ssl| flag to specify whether TLS is required|

There are times when you would like to include or exclude certain objects from being discovered. It is possible to specify a regular expression for both under ```filter``` attribute.

If you want to provide owner information for discovered items, you can provide the classification attributes like in the example below.

```yaml
kind: Discovery
metadata:
  name: "kafka-discovery"

type: kafka

instance:
  - name: "kafka-1"
    filter:
      excludes: [".*"]
      includes: ["account.*", "deployments.*", "aws-sts.*"]
    includes:
      - internal
    options:
      host: "kafka.ops-catalog.io"
      port: "9092"
      username: "kafka"
      password: "file:./tmp/kafkapassword"
      ssl: "false"
    classification:
      team: "keepers"
      domain: "storage"
      type: "Topic"
      capability: "operations"
```


Similarly, you can specify the template names as includes attributes. The template names will be applied to all discovered items. Note that the classification attributes will be preferred over what is included by templates.

To allow maximum flexibility, item level overrides are possible to specify on discovered items in the form of tags, annotations or comments.


The below table summarises the ways to override for each resource type

|Resource Engine|Override Approach|
|---|---|
|Postgres|Comments on Schema|
|Cassandra|Comments on catalog table in each keyspace|
|Kafka| None |
|S3|S3 Object Tags|
|Kubernetes Workloads|Annotations|
|Endpoints in Gateway API & Kubernetes|Annotations|
|Airflow|Tags Array in Dags|
|ALB|Object Tags|


