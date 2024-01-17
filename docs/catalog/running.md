The Ops Catalog can be run in various modes controlled by settings in config file. The catalog app looks to load a config file provided as CONFIG_FILE environment variable. It defaults to a config.yaml in the same directory as the catalog binary.

A docker image is provided for Catalog Application.

```docker pull opscatalog/catalog:latest```
You can build image locally via ```make go-image```


Running from source is also possible by executing ```go run cmd/catalog.go``` or ```make run-local```

