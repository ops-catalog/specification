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
      location: "https://github.com/open-catalog-alliance/discovery-sink.git"
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

    - location: "https://github.com/open-catalog-alliance/discovery-sink.git"
      extension: ".yaml"
      name: "discovery-sink"
      enabled: true
      options:
        username: "skhatri"
        password: "file:./tmp/password"


    - location: "https://github.com/open-catalog-alliance/specification.git"
      extension: ".yaml"
      name: "git-source"
      enabled: false
      options: 
        username: "skhatri"
        password: "file:./tmp/password"
        subpath: examples/my-account

    - location: "git@github.com:open-catalog-alliance/specification.git"
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
