The ops catalog project reads configuration provided by file either loaded though CONFIG_FILE environment variable or config.yaml located in the same folder as the catalog binary.

The example config.yaml and the content of it are discussed here.

```yaml
options:
  log: {}
  server: {}
  serve: {}
  fulfillment: {}
  discovery: {}
```

### Log
The log configuration node allows you to provide the minimum log level for the catalog application and the format to write the logs in. 

```yaml
  log:
    level: "info"
    format: "json"
```
Valid values for levels are DEBUG, INFO, WARN and ERROR.
The application supports plain text and json log format. Default format for logging is json.

### Server
The address value configured through the server.address attribute is provided as listen host to the go server.

Few example values can show you what is possible:
 :8080, 0.0.0.0:8080 or 127.0.0.1:8080, some-domain.com:8080

```yaml
  server:
    address: ":8080"
```

### Serve
The source attribute in serve node is an array of various different source types to load ops catalog data from. It can be from a http resource or a git project or a folder. Each source can be individually enabled or disabled. Few source examples are provided below.

Thre refresh frequency configuration can be provided to periodically refresh the catalog data by reloading from sources.

The search.index attribute is an array which can be configured to provide indexing and filter criteria when looking up catalog items.

Because ```team``` is one of the attribute values for index, we can query the ops catalog with the query parameter of ?team=<team_name>. Same applies for the other query parameters here.


```yaml
  serve:
    search: 
      index: 
        - "layer"
        - "tier" 
        - "team" 
        - "domain" 
        - "contact"
        - "type"
        - "language"
        - "name"
    refresh:
      frequency: 1m
    source:
    - location: ../specification/examples/my-account
      extension: ".yaml"
      name: "gitsync"
      enabled: true

    - location: "https://github.com/ops-catalog/discovery-sink.git"
      extension: ".yaml"
      name: "discovery-sink"
      enabled: true
      options:
        username: "skhatri"
        password: "file:./tmp/password"


    - location: "http://localhost:8000/my-account-catalog2.gz"
      extension: ".yaml"
      name: "gz-http-catalog-source"
      enabled: false
```

### Discovery
We try to use the same source object structure for both serving and discovery files. You can add as many discovery sources as you would like as well.
Further to that, you can list engines you would like to discover against. Similarly, the refresh frequency attribute helps run the discovery process as frequently as you would like.

Once items are discovered, we would need to persist them somewhere. We can specify a target location to commit the changes to.

```yaml
  discovery:
    source:
      - location: ../examples/datasets/discovery
        extension: ".yaml"
        name: "discover-1"
        enabled: true
    enabledEngines:
      - k8s
      - cassandra
      - kafka
      - airflow
      - postgres
      - s3
    refresh:
      frequency: 10m
    target:
      name: "sink"
      location: "https://github.com/ops-catalog/discovery-sink.git"
      options:
        username: "skhatri"
        password: "file:./tmp/ghkey"
```

If the discovery target and serving source are the same, the newly discovered objects will be available through catalog API as soon as the next serve refresh activity is run.

For teams, who would like to review what has been discovered, it is recommended to commit to a different branch and load serving data from a different branch. A PR review workflow can be added both to validate and to enrich data further before sharing with others.

### Fulfillment



A complete config.yaml is provided for your reference.
```yaml
options:

  log:
    level: "info"
    format: "json"
  server:
    address: ":8080"

  action:
    reference:
      catalog:
        location: "local"
      useDiscovery: true
      target:
        - name: broadcast
          location: "kafka://kafka.ops-catalog.io:9092/catalog-events"
          options:
            username: "kafka"
            password: "none"
    run:
      frequency: 2m
    enabledEngines:
      - cassandra
      - postgres
      - kafka
      - broadcast

  discovery:
    source:
      - location: ../specification/examples/discovery
        extension: ".yaml"
        name: "discover-1"
        enabled: true
    enabledEngines:
      - k8s
      - cassandra
      - kafka
      - airflow
      - postgres
      - s3
    refresh:
      frequency: 10m
    target:
      name: "sink"
      location: "https://github.com/ops-catalog/discovery-sink.git"
      options:
        username: "skhatri"
        password: "file:./tmp/ghkey"


  serve:
    search: 
      index: 
        - "layer"
        - "tier" 
        - "team" 
        - "domain" 
        - "contact"
        - "type"
        - "language"
        - "name"
      parallel: 1
    refresh:
      frequency: 1m
    source:
    - location: ../specification/examples/my-account
      extension: ".yaml"
      name: "gitsync"
      enabled: true

    - location: "https://github.com/ops-catalog/discovery-sink.git"
      extension: ".yaml"
      name: "discovery-sink"
      enabled: true
      options:
        username: "skhatri"
        password: "file:./tmp/password"


    - location: "https://github.com/ops-catalog/specification.git"
      extension: ".yaml"
      name: "git-source"
      enabled: false
      options: 
        username: "skhatri"
        password: "file:./tmp/password"
        subpath: examples/my-account

    - location: "git@github.com:ops-catalog/specification.git"
      extension: ".yaml"
      name: "git-ssh-source"
      enabled: false
      options:
        keyfile: "./tmp/key"
        subpath: examples/my-account

    - location: "$HOME/dev/projects/product/opscatalog/my-account-catalog3.tar"
      extension: ".yaml"
      name: "tar-catalog-source"
      enabled: false

    - location: "$HOME/dev/projects/product/opscatalog/my-account-catalog.tar.gz"
      extension: ".yaml"
      name: "tar-gz-catalog-source"
      enabled: false

    - location: "$HOME/dev/projects/product/opscatalog/my-account-catalog2.gz"
      extension: ".yaml"
      name: "gzip-catalog-source"
      enabled: false

    - location: "$HOME/dev/projects/product/opscatalog/my-account-catalog.zip"
      extension: ".yaml"
      name: "zip-catalog-source"
      enabled: false

    - location: "http://localhost:8000/my-account-catalog.zip"
      extension: ".yaml"
      name: "zip-http-catalog-source"
      enabled: false

    - location: "http://localhost:8000/my-account-catalog2.gz"
      extension: ".yaml"
      name: "gz-http-catalog-source"
      enabled: false

```
