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
|cafile|Location of CA file, if not globally trusted and ssl is enabled|
|keyfile|Location of key file, required for client auth when ssl is enabled|
|certfile|Location of cert file, required for client auth when ssl is enabled|

There are other attributes which are contextual and they are listed here:

|Attribute|Description|Applicable to|
|---|---|---|
|database|Database Name|Postgres|
|org|Organisation owning the repositories in scope|Github|
|project|Project owning the repositories in scope|Bitbucket|
|use-hints|Flag used to determine whether object enrichment should be done by reading comments, tags, properties etc|Databases,Git Service,Object Store|
|provider|Name of the provider if multiple provider exist for a type - eg Github, Bitbucket| |

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
    enabled: true
    includes:
      - internal
    options:
      host: "kafka.ops-catalog.io"
      port: "9092"
      username: "kafka"
      password: "file:./tmp/kafkapassword"
      ssl: "false"
      use-hints: "true"
    classification:
      team: "keepers"
      domain: "storage"
      type: "Topic"
      capability: "operations"
      businessUnit: "tech"
    duplicatesStrategy: "ignore"
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
|SNS|SNS Object Tags|
|SQS|SQS Object Tags|
|Lambda|Lambda Tags|
|Kubernetes Workloads|Annotations|
|Endpoints in Gateway API & Kubernetes|Annotations|
|Airflow|Tags Array in Dags|
|Git|Message specified in tag named catalog|
|ALB|Object Tags|

In Scenarios where it is not possible to read further enrichment hints from the above locations, especially true for databases and Git, if running with restricted permissions,
one can disable lookup by specifying ```use-hints: "false"```. When not provided, it use-hints defaults to true.



Duplicates can be handled by providing a strategy value at instance level.

```yaml
  instance:
    ...
    duplicatesStrategy: ""
```

Following are the possible values for ```duplicatesStrategy```

|Strategy|Description|
|---|---|
|skip| Drop the discovered item |
|ignore| Ignore and add discovered item to the catalog|
|mergeLeft|Use existing catalog object as the base and override with attributes found in discovery|
|merge|Shorthand for mergeLeft|
|mergeRight|Use discovered object as the base and override with attributes found in catalog|
|replace|Replace discovered item with original item from the catalog|

Discovery Instances are enabled by default. At times, we may want to disable a declared discovery instance and for this we have the ```enabled``` flag. Enabled flag can be evaluated at runtime as well with simple expressions.
Few examples of valid expressions are listed below.

|Expression|Meaning|
|---|---|
|enabled: "${env.SSL_STATE==on}"|Enable the discovery config when environment variable SSL_STATE is set to "on"|
|enabled: "${env.GOOS!=darwin}"|Only enable this discovery when not running on MacOS|
|enabled: "${on=on}"|It also handles text to text comparison. Useful when lhs or rhs the outcome of template substitution|
|enabled: true| A boolean static value to enable discovery config|

See <a href="https://github.com/ops-catalog/examples/blob/main/datasets/docker-discovery/pg1.yaml" target="_blank">Example Postgres Discovery Config</a> to check how expressions are used to enable different discovery targets.


Discovery Handler only supports equal and not equal checks currently.


