Customers
======

Endpoints:

- [List all customers](#list-all-customers)
- [Show a customer](#show-a-customer)
- [Show current customer settings](#update-who-can-access-a-project)
- [Create a customer](#create-a-customer)
- [Update a customer](#update-a-customer)
- [Delete a customer](#delete-a-customer)

List all customers
--------------

* `GET /customers` will return a paginated list of customers from the current merchant.

###### Example JSON Response
<!-- START GET /customers -->
```json
{
    "data": [
        {
            "uuid": "caedbbbe-7d93-476f-b965-bf97cd7ce874",
            "name": "Reportei Customer 1",
            "created_at": "2024-09-24 17:07:34",
            "updated_at": "2024-09-24 17:07:34",
            "merchant": "Reportei"
        },
        {
            "uuid": "073c1e15-94d0-49b3-9861-a0e9b7ffb06c",
            "name": "Reportei Customer 2",
            "created_at": "2024-09-24 19:06:08",
            "updated_at": "2024-09-24 19:06:08",
            "merchant": "Reportei"
        }
    ],
    "meta": {
        "current_page": 1,
        "from": 1,
        "last_page": 1,
        "path": "http://integrations.reportei.com/api/customers",
        "per_page": 15,
        "to": 2,
        "total": 2,
        "sortBy": null,
        "descending": false
    }
}
```
<!-- END GET /people.json -->
###### Copy as cURL

``` shell
curl -s -H "Authorization: Bearer $ACCESS_TOKEN" https://integrations.reportei.com/customers
```


Show a customer
------------------------

* `GET /customers/{$uuid}` will return customer from merchant given uuid

###### Example JSON Response
<!-- START GET /customers -->
```json
{
  "customer": {
    "uuid": "caedbbbe-7d93-476f-b965-bf97cd7ce874",
    "name": "Reportei Customer 1",
    "created_at": "2024-09-24 17:07:34",
    "updated_at": "2024-09-24 17:07:34",
    "merchant": "Reportei"
  }
}
```
<!-- END GET /people.json -->
###### Copy as cURL

``` shell
curl -s -H "Authorization: Bearer $ACCESS_TOKEN" https://integrations.reportei.com/customers/{$uuid}
```

Show current customer settings
------------------------

* `GET /customers/settings` will return a merchant customer alongside their settings given x-customer-token.

###### Example JSON Response
<!-- START GET /customers/settings -->
```json
{
  "customer": {
      "uuid": "073c1e15-94d0-49b3-9861-a0e9b7ffb06c",
      "name": "Reportei Customer 1",
      "created_at": "2024-09-24 19:06:08",
      "updated_at": "2024-09-24 19:06:08",
      "merchant": "Reportei",
      "integrations": [
        {
          "uuid": "6110b666-0327-4a81-b48e-9feb34d72f78",
          "integration": "Instagram Business",
          "name": "reportei",
          "slug": "instagram_business",
          "status": "active"
        }
      ]
  }
}
```
<!-- END GET /customers/settings -->
###### Copy as cURL

``` shell
curl -s -H "Authorization: Bearer $ACCESS_TOKEN" \
-H "x-customer-token: $CUSTOMER_TOKEN" \
https://integrations.reportei.com/customers/settings
```

Create a customer
--------------

* `POST /customers` creates a new customer for the current merchant.

**Required parameters**: `name` representing the customer name.

This endpoint will return `201 Created` with the current JSON representation of the customer if the creation was a success. See the [Show a customer](#show-a-customer) endpoint for more info on the payload.

**Important notes on Api Token**: When a customer is created, an api_token (`x-customer-token`) is only provided at this moment and must be stored by the consumer. This token is necessary for all subsequent customer-related requests and will not be retrievable again. Be sure to store this token securely, as it will not be provided in any other requests.

###### Example JSON Request

``` json
{
  "name": "Reportei Customer 3"
}
```

###### Example JSON Response
<!-- START POST /customers -->
```json
{
  "customer": {
    "name": "Reportei Customer 3",
    "uuid": "9cdc0998-cd1c-406c-98b2-a40448486657",
    "updated_at": "2024-10-01 17:15:12",
    "created_at": "2024-10-01 17:15:12",
    "merchant": "Reportei",
    "api_token": "6d37ffcc936ffa1d2bf4f99dbea973b760988e6fe755a22c328d3d3f908f5f87"
  }
}
```
<!-- END POST /customers -->
###### Copy as cURL

``` shell
curl -s -H "Authorization: Bearer $ACCESS_TOKEN" -H "Content-Type: application/json" \
  -d '{"name":"Reportei Customer 3"}' \
  https://integrations.reportei.com/customers
```

Update a customer
--------------

* `PUT /customers/{uuid}` updates a customer from the current merchant.

**Required parameters**: `name` representing the customer name.

This endpoint will return `200 OK` with the current JSON representation of the customer if the update was a success. See the [Show a customer](#show-a-customer) endpoint for more info on the payload.

###### Example JSON Request

``` json
{
  "name": "Reportei Customer 3.1"
}
```

###### Copy as cURL

``` shell
curl -s -H "Authorization: Bearer $ACCESS_TOKEN" -H "Content-Type: application/json" \
  -d '{"name":"Reportei Customer 3.1"}' -X PUT \
  https://integrations.reportei.com/customers/{$uuid}
```

Delete a customer
--------------

* `POST /customers/{uuid}` deletes a customer from the current merchant.

This endpoint will return `200 OK` if the deletion was a success.

###### Example JSON Response

``` json
{
    "success": true,
    "message": "Record successfully removed"
}
```

###### Copy as cURL

``` shell
curl -s -H "Authorization: Bearer $ACCESS_TOKEN" -H "Content-Type: application/json" \
  -d '{"name":"Reportei Customer 3.1"}' -X PUT \
  https://integrations.reportei.com/customers
```