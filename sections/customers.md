Customers
======

Endpoints:

- [List all customers](#list-all-customers)
- [Show a customer](#show-a-customer)
- [Show current customer settings](#update-who-can-access-a-project)
- [Create a customer](#get-pingable-people)
- [Update a customer](#get-person)
- [Delete a customer](#get-my-personal-info)

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