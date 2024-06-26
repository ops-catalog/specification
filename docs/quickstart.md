# Ops Catalog Examples
There are a bunch of example configurations available in this project to run Ops Catalog with various extensions.

## Running Ops Catalog Api
Ensure you have Docker/Nerdctl installed and execute the following:

```shell
git clone git@github.com:ops-catalog/examples.git
cd examples
```
You can follow this in <a href="https://github.com/ops-catalog/examples" target="_blank">examples repository</a> as well.

## Recipes
The recipes discussed here can be used for reference to try out a specific use case.

|Recipe Name|Goal|
|---|---|
|simple|run a basic catalog API with static data|
|minimal|run ui,catalog and postgres|
|ssl|run ui, catalog and postgres. Postgres TLS is enabled.|
|edge|run ui and multiple catalog instances. One acts as aggregator and another as edge|
|discovery|finds resources in targets like databases, airflow, k8s, messaging servers|
|fulfillment|provisions resources against databases, message servers|

A run.sh file is provided to make it easier to run various docker compose files. Usage documentation for run.sh is shared below.

```shell
$ ./run.sh                                                                                                                 i
a recipe can be run like this:

  ./run.sh recipe <name>
  ./run.sh down

Recipe command runs one of the available recipes.

name:
-----
simple      - a catalog server with sample catalog items loaded from ./datasets/catalog/my-account
minimal     - a basic setup with catalog, ui, postgres and some seed data
ssl         - a basic setup with catalog, ui and postgres with TLS
edge        - aggregator catalog discovers data from edge catalog
discovery   - performs discovery against few targets like postgres, cassandra, airflow, k8s, kafka and presents in UI
fulfillment - provisions resources in catalog which are not yet in target servers

Down command shuts down the running containers.

```

### Recipe: simple
This is probably the simplest use case. We are mounting catalog items into a folder and serving it via catalog instance. This minimilastic config can be queried and filtered through a HTTP API call.

To run this recipe, invoke

```shell
./run.sh recipe simple
```

Docker containers started with ./run.sh command can be stopped using ```./run.sh down```

Since this step only requires a single docker container to run, it can also be invoked directly like so:

```shell
docker run \
-v $(pwd)/datasets:/opt/app/datasets \
-v $(pwd)/recipes/simple:/opt/app/config \
-e CONFIG_FILE=/opt/app/config/config.yaml -p 8080:8080 \
-it opscatalog/catalog:latest
```

#### Test Access
Load the following link to view catalog item:

|Link|Description|
|---|---|
|http://localhost:8080/api/catalog| Catalog Listing|
|http://localhost:8080/api/catalog?kind=Resource| List Resources Only|
|http://localhost:8080/api/catalog?kind=Component|List Components Only|


### Recipe: minimal
If you have resource constraint, you can run selected profile as well and accordingly update engines list in setup/containers/ops-catalog/conf/discovery.yaml or fulfillment.yaml

We can run the command like below to bring up ops catalog API, a stand-in for objects in a Kubernetes cluster,  a postgres instance with two databases and a basic UI.

```shell
./run.sh recipe minimal
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
    businessUnit: "retail"
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

#### UI
Ops Catalog can provide data to your existing backstage instance. Navigate to http://localhost:7007/catalog to see Ops Catalog objects within backstage UI.


#### Tearing Down
Each Recipe run can be cleaned up by running ```./run.sh down```

### Recipe: ssl

To run with SSL enabled, set SSL_STATE to on in your .dockerenv or one of the env files. A .ssl file is provided for reference and this setup can be run with SSL by executing:

```shell
./run.sh recipe ssl
```

### Recipe: edge
A number of catalog instances can be run in federated mode. This allows for local teams to run their own edge catalog for their unique workflows. A more global catalog instance can then act as aggregator to compose data from all catalogs.

You can simulate this by running the following:

```shell
./run.sh recipe edge
```


### Recipe: discovery
This compose file also runs a standalone kafka, postgres and cassandra and seeds them with initial objects so they can be collected by the discovery module.

```shell
./run.sh recipe discovery
```

### Recipe: fulfillment
The compose file is somewhat similar to discovery as it is now writing back to the targets.

```shell
./run.sh recipe fulfillment
```


## Cleanup Activity
To cleanup what we did just then, run the following command to remove all running containers associated with this project.

```shell
./run.sh down
```

or

```shell
docker compose down
```
