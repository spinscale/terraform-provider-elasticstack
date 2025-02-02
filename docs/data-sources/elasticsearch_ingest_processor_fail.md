---
subcategory: "Ingest"
layout: ""
page_title: "Elasticstack: elasticstack_elasticsearch_ingest_processor_fail Data Source"
description: |-
  Helper data source to create a processor which raises an exception.
---

# Data Source: elasticstack_elasticsearch_ingest_processor_fail

Raises an exception. This is useful for when you expect a pipeline to fail and want to relay a specific message to the requester.

See: https://www.elastic.co/guide/en/elasticsearch/reference/current/fail-processor.html


## Example Usage

```terraform
provider "elasticstack" {
  elasticsearch {}
}

data "elasticstack_elasticsearch_ingest_processor_fail" "fail" {
  if      = "ctx.tags.contains('production') != true"
  message = "The production tag is not present, found tags: {{{tags}}}"
}

resource "elasticstack_elasticsearch_ingest_pipeline" "my_ingest_pipeline" {
  name = "fail-ingest"

  processors = [
    data.elasticstack_elasticsearch_ingest_processor_fail.fail.json
  ]
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- **message** (String) The error message thrown by the processor.

### Optional

- **description** (String) Description of the processor.
- **if** (String) Conditionally execute the processor
- **ignore_failure** (Boolean) Ignore failures for the processor.
- **on_failure** (List of String) Handle failures for the processor.
- **tag** (String) Identifier for the processor.

### Read-Only

- **id** (String) Internal identifier of the resource
- **json** (String) JSON representation of this data source.
