---
subcategory: "Ingest"
layout: ""
page_title: "Elasticstack: elasticstack_elasticsearch_ingest_processor_dot_expander Data Source"
description: |-
  Helper data source to create a processor which expands a field with dots into an object field. 
---

# Data Source: elasticstack_elasticsearch_ingest_processor_dot_expander

Expands a field with dots into an object field. This processor allows fields with dots in the name to be accessible by other processors in the pipeline. Otherwise these fields can’t be accessed by any processor.

See: elastic.co/guide/en/elasticsearch/reference/current/dot-expand-processor.html


## Example Usage

```terraform
provider "elasticstack" {
  elasticsearch {}
}

data "elasticstack_elasticsearch_ingest_processor_dot_expander" "dot_expander" {
  field = "foo.bar"
}

resource "elasticstack_elasticsearch_ingest_pipeline" "my_ingest_pipeline" {
  name = "dot-expander-ingest"

  processors = [
    data.elasticstack_elasticsearch_ingest_processor_dot_expander.dot_expander.json
  ]
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- **field** (String) The field to expand into an object field. If set to *, all top-level fields will be expanded.

### Optional

- **description** (String) Description of the processor.
- **if** (String) Conditionally execute the processor
- **ignore_failure** (Boolean) Ignore failures for the processor.
- **on_failure** (List of String) Handle failures for the processor.
- **override** (Boolean) Controls the behavior when there is already an existing nested object that conflicts with the expanded field.
- **path** (String) The field that contains the field to expand.
- **tag** (String) Identifier for the processor.

### Read-Only

- **id** (String) Internal identifier of the resource
- **json** (String) JSON representation of this data source.
