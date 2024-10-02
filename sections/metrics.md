Customers
======

Endpoints:

- [Get metrics data](#get-metrics-data)
- [Get metrics data asynchronously](#get-metrics-data-async)

Get metrics data
--------------

* `POST /metrics/get-data` will return an object with the values of the requested metrics from a customer integration.

_Required parameters_:

* `customer_integration` - $uuid of desired customer integration.
* `start` - Analysis start date (ISO 8601)
* `end` - Analysis end date (ISO 8601)
* `metrics` - Array containing metric structure

_Optional parameters_:

* `comparison_start` - Comparison start date (ISO 8601)
* `comparison_end` - Comparison end date (ISO 8601)

This endpoint will return an object with the values of the requested metrics.

###### Example JSON Request

``` json
{
  "customer_integration": "4addc0da-8583-4dbb-a0e9-c7e2e8470f50",
  "start": "2024-01-01",
  "end": "2024-09-01",
  "metrics": [
    {
        "id": "b03f07f5-d54a-4df4-b5ff-2448f21c3450",
        "reference_key": "ig:story_replies",
        "component": "number_v1",
        "metrics": [
            "replies"
        ],
        "dimensions": [
            "stories"
        ]
    }
  ]
}
```

###### Example JSON Response

``` json
{
  "b03f07f5-d54a-4df4-b5ff-2448f21c3450": {
    "values": 55645
  }
}
```

<!-- END GET /metrics/get-data -->
###### Copy as cURL

``` shell
curl -s -H "Authorization: Bearer $ACCESS_TOKEN" https://integrations.reportei.com/metrics/get-data
```

Get metrics data asynchronously
--------------

* `POST /metrics/get-data-async` initiates a process to gather the requested metrics data and asynchronously posts the results to the provided `metrics_webhook_url`.

_Required parameters_:

* `metrics_webhook_url` - URL that will receive metrics payload.
* `customer_integration` - $uuid of desired customer integration.
* `start` - Analysis start date (ISO 8601)
* `end` - Analysis end date (ISO 8601)
* `metrics` - Array containing metric structure

_Optional parameters_:

* `comparison_start` - Comparison start date (ISO 8601)
* `comparison_end` - Comparison end date (ISO 8601)

This endpoint will return `200 OK` once the process of getting metrics data has started, after the metrics are fetched, the payload containing the metrics data will be posted to the provided `metrics_webhook_url`.

###### Example JSON Request

``` json
{
  "customer_integration": "4addc0da-8583-4dbb-a0e9-c7e2e8470f50",
  "start": "2024-01-01",
  "end": "2024-09-01",
  "metrics": [
    {
        "id": "b03f07f5-d54a-4df4-b5ff-2448f21c3450",
        "reference_key": "ig:story_replies",
        "component": "number_v1",
        "metrics": [
            "replies"
        ],
        "dimensions": [
            "stories"
        ]
    }
  ]
}
```

###### Example Webhook Payload

``` json
{
  "b03f07f5-d54a-4df4-b5ff-2448f21c3450": {
    "values": 55645
  }
}
```

<!-- END GET /metrics/get-data -->
###### Copy as cURL

``` shell
curl -s -H "Authorization: Bearer $ACCESS_TOKEN" https://integrations.reportei.com/metrics/get-data
```