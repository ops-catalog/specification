### Download example config
We have an example data set available in GitHub. Clone the repository and navigate to the directory via cli.
```
git clone git@github.com:ops-catalog/examples.git
cd examples
```

### Catalog Server
Ensure you have Docker/Nerdctl install and execute the following:

```
docker run \
-v $(pwd)/datasets:/opt/app/datasets \
-v $(pwd)/conf:/opt/app/config \
-e CONFIG_FILE=/opt/app/config/simple.yaml -p 8080:8080 \
-it opscatalog/catalog:latest
```
This runs a minimilastic config where the catalog content can be queried and filtered through a HTTP API call.

### Test Access
Load the following link to view catalog item:
http://localhost:8080/api/catalog


### Discovery Mode (Coming soon)
This compose file also runs a standalone kafka, postgres and cassandra and seeds them with initial objects so they can be collected by the discovery module.

```
docker compose -f docker/with-discovery.yaml up -d
```

### Fulfillment Mode (Coming soon)
The compose file is somewhat similar to ```with-discovery.yaml``` as it is now writing back to the targets.

```
docker compose -f docker/with-fulfillment.yaml up -d
```
