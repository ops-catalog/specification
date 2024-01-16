### Scorecard
Ops Catalog uses a series of checks to provide a score for each catalog item. This can serve as a guide to improving and refining the data that is contributed by owners of each catalog item.

Each catalog item has a grade that is determined by the score. Possible grades are A+, A, B, C, D, E, F.

The score node is attached to each catalog item where you can see both the label and value.

```json
    "score": {
        "value": 64,
        "label": "D"
      }
```

The debt section of the catalog item response has additional information on how points were deducted.

```json
    {
      "debt": {
        "entries": [
          {
            "name": "Tier information should be populated",
            "description": "1 point(s) deducted",
            "severity": "medium"
          },
          {
            "name": "A valid contact is recommended",
            "description": "2 point(s) deducted",
            "severity": "medium"
          }
        ]
      }
    }
```
