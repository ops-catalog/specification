### FAQs

##### Is Catalog Server essential?
While Catalog Server serves as a reference implementation, its purpose is to foster collaboration in the DevOps space regarding the standardized capture of assets and attributes. You have the flexibility to select and adopt functionalities that align with their needs. Contributing custom implementations to the community would be mutually beneficial, enhancing the collective understanding and utility of the system.

##### Why do I need API?
You can avoid performing dry run. It becomes a shared asset which many tools can use for their operations.

##### How do I handle environment specific properties?
To address environment-specific properties, consider incorporating them into templates with selectors, enabling the activation of specific templates based on the relevant environment. Alternatively, you may opt to place these properties in separate sources, allowing for controlled inclusion—particularly beneficial in environments requiring independent instances for each specific setting.







