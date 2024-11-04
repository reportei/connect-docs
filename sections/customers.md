Customers
======

In this API, customers refer to your users or clients. You, as the merchant, can use the API to manage your customers and their integrations. When dealing with customer-specific data, you’ll need to include an additional authentication header (x-customer-token), which identifies the specific customer whose data you are accessing. This token ensures secure access to customer data and is required for all customer-related requests.

Endpoints:

- [List all customers](#list-all-customers)
- [Show a customer](#show-a-customer)
- [Show current customer settings](#update-who-can-access-a-project)
- [Create a customer](#create-a-customer)
- [Update a customer](#update-a-customer)
- [Delete a customer](#delete-a-customer)
- [Update a customer payment status](#update-a-customer-payment-status)

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
            "trial_ends_at": "2024-10-08 17:15:12",
            "is_paying": false,
            "merchant": "Reportei"
        },
        {
            "uuid": "073c1e15-94d0-49b3-9861-a0e9b7ffb06c",
            "name": "Reportei Customer 2",
            "created_at": "2024-09-24 19:06:08",
            "updated_at": "2024-09-24 19:06:08",
            "trial_ends_at": "2024-10-08 17:15:12",
            "is_paying": true,
            "merchant": "Reportei"
        }
    ],
    "meta": {
        "current_page": 1,
        "from": 1,
        "last_page": 1,
        "path": "http://connect.reportei.com/api/customers",
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
curl -s -H "Authorization: Bearer $ACCESS_TOKEN" https://connect.reportei.com/customers
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
    "trial_ends_at": "2024-10-08 17:15:12",
    "is_paying": false,
    "merchant": "Reportei"
  }
}
```
<!-- END GET /people.json -->
###### Copy as cURL

``` shell
curl -s -H "Authorization: Bearer $ACCESS_TOKEN" https://connect.reportei.com/customers/{$uuid}
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
      "trial_ends_at": "2024-10-08 17:15:12",
      "is_paying": false,
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
https://connect.reportei.com/customers/settings
```

Create a customer
--------------

* `POST /customers` creates a new customer for the current merchant.

**Required parameters**: `name` representing the customer name.

This endpoint will return `201 Created` with the current JSON representation of the customer if the creation was a success. See the [Show a customer](#show-a-customer) endpoint for more info on the payload.

**Important notes on Api Token**: When a customer is created, an api_token (`x-customer-token`) is only provided at this moment and must be stored by the consumer. This token is necessary for all subsequent customer-related requests and will not be retrievable again. Be sure to store this token securely, as it will not be provided in any other requests.

**Trial Period**: When a customer is created, a trial period of 7 days is automatically applied (`trial_ends_at`), after the trial ends the requests to [Customer Integrations](./customers-integrations.md) and [Metrics](./metrics.md) endpoints will return a `401 Unauthorized`, to continue using the API for this customer, you will need mark them as a paying customer, see [Update a customer payment status](#update-a-customer-payment-status).

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
    "trial_ends_at": "2024-10-08 17:15:12",
    "is_paying": false,
    "merchant": "Reportei",
    "api_token": "6d37ffcc936ffa1d2bf4f99dbea973b760988e6fe755a22c328d3d3f908f5f87"
  }
}
```
<!-- END POST /customers -->
###### Copy as cURL

``` shell
curl -s -X POST -H "Authorization: Bearer $ACCESS_TOKEN" -H "Content-Type: application/json" \
  -d '{"name":"Reportei Customer 3"}' \
  https://connect.reportei.com/customers
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
curl -s -X PUT -H "Authorization: Bearer $ACCESS_TOKEN" -H "Content-Type: application/json" \
  -d '{"name":"Reportei Customer 3.1"}' -X PUT \
  https://connect.reportei.com/customers/{$uuid}
```

Delete a customer
--------------

* `DELETE /customers/{uuid}` deletes a customer from the current merchant.

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
curl -s -X DELETE -H "Authorization: Bearer $ACCESS_TOKEN" -H "Content-Type: application/json" \
  -d '{"name":"Reportei Customer 3.1"}' -X PUT \
  https://connect.reportei.com/customers
```

Update Customer Payment Status
--------------

* `POST /customers/{uuid}/update-payment-status` updates a customer payment status.

**Required parameters**: `is_paying` Value used to inficate if customer is paying or not.


This endpoint will return `200 OK` if the payment status was updated successfully. After the update you will be able to make requests to [Customer Integrations](./customers-integrations.md) and [Metrics](./metrics.md) endpoints even after the trial period has ended.

###### Example JSON Request

``` json
{
  "is_paying": true
}
```


###### Example JSON Response

``` json
{
    "success": true,
    "message": "Customer is now marked as a paying customer"
}
```

###### Copy as cURL

``` shell
curl -s -X POST -H "Authorization: Bearer $ACCESS_TOKEN" -H "Content-Type: application/json" \
  -d '{"is_paying":true}' -X POST \
  https://connect.reportei.com/customers/{$uuid}/update-payment-status
```