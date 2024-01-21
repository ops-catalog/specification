Fulfillment process requires access to catalog as well as targets against which the fulfillment is to be applied.

We can reuse the discovery config as targets and we can either access in-process catalog API or a remote one. 

Refer to [configuration](../../catalog/configuration#fulfillment) guide on how to add targets.


While most fulfillment targets will create resources or perform some provisioning action, the system also has a broadcast plugin that will send fulfillment data to a resource target. Only kafka is supported today for this mode.

```yaml
fulfillment:
    reference:
      target:
        - name: broadcast
          location: "kafka://kafka.ops-catalog.io:9092/catalog-events"
          options:
            username: "kafka"
            password: "none"
    enabledEngines:
        - broadcast
```

With a setup like above, each fulfillment action is represented as a JSON payload and forwarded to the topic catalog-events.