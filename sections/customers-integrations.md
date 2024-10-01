Customers
======

Endpoints:

- [Create a customer integration session](#create-a-customer-integration-session)
- [Show a customer integration](#show-a-customer-integration)
- [Delete a customer integration](#delete-a-customer-integration)

Create a customer integration session
--------------

For a customer to be able to integrate their networks it is necessary to create a session, it will act like a checkout, once the customer accesses the session_link, they will be redirected to a page inside reportei where they can see their current integrations and all other networks that are available for integration. The session has a duration of `5 minutes`, after that if the link is accessed, `403 Unauthorized` will be returned.

* `POST /customer-integrations/session` will return a paginated list of customers from the current merchant.

###### Example JSON Response
<!-- START POST /customer-integrations/session -->
```json
{
  "integration_session": {
    "session_uuid": "679e77d9-b270-4fb9-9f2c-27bcaebddc52",
    "session_link": "http://integrations.reportei.com/customer-integrations/session/679e77d9-b270-4fb9-9f2c-27bcaebddc52",
    "expires_at": "2024-10-02T06:14:50.898761Z",
    "merchant": "Reportei",
    "merchant_uuid": "c1e6c85a-6441-4107-ab36-b8bf581b40e0",
    "customer": "Reportei Customer",
    "customer_uuid": "073c1e15-94d0-49b3-9861-a0e9b7ffb06c"
  }
}
```
<!-- END POST /customer-integrations/session -->
###### Copy as cURL

``` shell
curl -s -H "Authorization: Bearer $ACCESS_TOKEN" \
-H "x-customer-token: $CUSTOMER_TOKEN" \
https://integrations.reportei.com/customer-integrations/session
```