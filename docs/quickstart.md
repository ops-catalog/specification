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


### Discovery Mode
This compose file also runs a standalone kafka, postgres and cassandra and seeds them with initial objects so they can be collected by the discovery module.

```
docker compose --env-file docker/.discovery -f docker/docker-compose.yaml --profile all up -d
```

### Fulfillment Mode
The compose file is somewhat similar to discovery as it is now writing back to the targets.

```
docker compose --env-file docker/.fulfillment -f docker/docker-compose.yaml --profile all up -d
```

If you have resource constraint, you can run selected profile as well and accordingly update engines list in docker/ops-catalog/conf/discovery.yaml or fulfillment.yaml

```
docker compose --env-file docker/.minimal -f docker/docker-compose.yaml --profile k8s up -d
docker compose --env-file docker/.minimal -f docker/docker-compose.yaml --profile catalog up -d
```

The above two commands will run catalog, kubernetes api and postgres.

To test discovery and fulfillment, create a new schema against the running postgres.

```shell
docker exec -it postgres psql -Upostgres -dservicing 
servicing=# CREATE SCHEMA IF NOT EXISTS refdata;
```

Also drop a new file into the mix

```shell
cat > datasets/my-account/merchant-schema.yaml <<EOF
apiVersion: "v1"
kind: Resource
class: Schema
metadata:
  name: "merchants"
  description: "Merchant Tables are hosted in this schema"
  license: "private"
dependencies:
  upstream: []
  providedBy: postgres.pg-2
  triggers: []
classification:
    tag: ["transaction", "customer"]
    domain: "transaction"
    team: "transaction"
    capability: "onlinebanking"
EOF
```

Once the discovery and fulfillment loop is complete, there should be two new items in the catalog.
The schema called merchant should be visible in postgres as well.

Check the catalog entry via api calls:

```shell 
http://localhost:8080/api/catalog?name=merchants
http://localhost:8080/api/catalog?name=refdata
```
