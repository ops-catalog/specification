### Download example config
We have an example data set available in GitHub. Clone the repository and navigate to the directory via cli.
```
git clone git@github.com:ops-catalog/example-data.git
cd example-data
```

### Catalog Server
Ensure you have Docker/Nerdctl install and execute the following:

```
docker run \
-v $(pwd)/examples:/opt/data/examples \
-v $(pwd)/conf:/opt/config \
-e CONFIG_FILE=/opt/config/simple.yaml -p 8080:8080 \
-it opscatalog/catalog:latest
```
This runs a minimilastic config where the catalog content can be queried and filtered through a HTTP API call.

### Test Access
Load the following link to view catalog item:
http://localhost:8080/api/catalog?name=checks

### Discovery Mode
This compose file also runs a standalone kafka, postgres and cassandra and seeds them with initial objects so they can be collected by the discovery module.

```docker compose -f docker/with-discovery.yaml up -d```

### Fulfillment Mode
The compose file is somewhat similar to ```with-discovery.yaml``` as it is now writing back to the targets.

```
docker compose -f docker/with-fulfillment.yaml up -d
```
