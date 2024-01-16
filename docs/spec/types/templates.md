### Templates

Incorporating templates into a definition allows for the application of traits from various collections, promoting data reusability. This streamlined approach facilitates the modification of attributes in a centralized location. Templates exhibit hierarchy, enabling them to include traits from other templates, which may, in turn, depend on additional templates.

Essentially, templates share similarities with Catalog Items but are distinguished by having their kind set to ```Template```.

The resolution of templates is the initial step, constructing a collection that can subsequently be applied in non-template declarations. To apply a template in a specific definition, the template name is provided in the includes field, which accepts an array of template names. 

The order in which templates are included matters; the first template in the list is applied first. Subsequent templates override attributes imported later. Ultimately, the original declaration is applied to the effective structure resulting from the template merge, ensuring that any local declarations on the Catalog Item always take precedence over attributes borrowed from templates.


#### How do I create a template?
A template looks like a regular Catalog Item. This template ```account-team``` can now be used by other items (probably) all items in the domain of accounts.

This template also includes another template ```internal```

```yaml
apiVersion: v1
kind: Template
metadata:
    name: account-team
classification:
    team: accountants
    domain: accounts
includes:
    - internal
```

Anything declared in internal will be overridden by attributes in account-team. Similarly, when this is included in the definition of a catalog item, the latter includes will override the attributes in this template. Ultimately, local declaration in catalog item will take precedence over any imported by includes.

![Use of Template in My Account](./../../assets/images/my-account-template.svg)

#### When do I use template?
You can use template to reduce the amount of configuration code you need to manage in many places. By grouping related attributes in a single template, you allow them to be shared within the domain and across the organisation.

#### How do I manage templates?
Templates may coexist with catalog item definitions, but it is advisable for templates to have a dedicated source separate from the main catalog. This separation aids in the meticulous management of crucial attributes, particularly those with a significant impact. Less frequently used or local definitions may be stored on a per-domain or per-team basis, providing a scalable approach as your team expands.



