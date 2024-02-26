# Ops Catalog Examples
There are a bunch of example configurations available in this project to run Ops Catalog with various extensions.

### Running Ops Catalog Api
Ensure you have Docker/Nerdctl installed and execute the following:

```
git clone git@github.com:ops-catalog/examples.git
cd examples
docker run \
-v $(pwd)/datasets:/opt/app/datasets \
-v $(pwd)/conf:/opt/app/config \
-e CONFIG_FILE=/opt/app/config/simple.yaml -p 8080:8080 \
-it opscatalog/catalog:latest
```
This runs a minimilastic config where the catalog content can be queried and filtered through a HTTP API call.

### Test Access
Load the following link to view catalog item:

|Link|Description|
|---|---|
|http://localhost:8080/api/catalog| Catalog Listing|
|http://localhost:8080/api/catalog?kind=Resource| List Resources Only|
|http://localhost:8080/api/catalog?kind=Component|List Components Only|


### Ops Catalog with minimal data
If you have resource constraint, you can run selected profile as well and accordingly update engines list in docker/ops-catalog/conf/discovery.yaml or fulfillment.yaml

We can run the command like below to bring up ops catalog API, a stand-in for objects in a Kubernetes cluster,  a postgres instance with two databases and a basic UI.

```
docker compose --env-file docker/.minimal -f docker/docker-compose.yaml --profile minimal up -d
```

To test discovery and fulfillment, create a new schema against the running postgres.

```shell
docker exec -it postgres psql -Upostgres -dservicing
servicing=# CREATE SCHEMA IF NOT EXISTS refdata;
servicing=# \q
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

```shell
docker exec -it postgres psql -Upostgres -dpreferences
preferences=# select catalog_name, schema_name from information_schema.schemata;
preferences=# \q
```


Check the catalog entry via api calls. The default refresh frequency is served data is set at 5 minutes which you can change by updating ops-catalog/conf/*.yaml

```shell
http://localhost:8080/api/catalog?name=merchants
http://localhost:8080/api/catalog?name=servicing.refdata
```

If you list files under datasets/discovered-items you should also see few new folders depending on what discovery engines were enabled. In the case of minimal profile, you will see k8s and postgres folders populated with catalog items.

### UI
Ops Catalog can provide data to your existing backstage instance. Navigate to http://localhost:7007/catalog to see Ops Catalog objects within backstage UI.

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


### Cleanup Activity
To cleanup what we did just then, run the following command to remove all running containers associated with this project.

```
docker compose -f docker/docker-compose.yaml down --remove-orphans
```

To run with SSL enabled, set SSL_STATE to on in your .dockerenv or one of the env files. A .ssl file is provided for reference and this setup can be run with SSL by executing:

```
docker compose --env-file docker/.ssl -f docker/docker-compose.yaml --profile minimal up -d
```
