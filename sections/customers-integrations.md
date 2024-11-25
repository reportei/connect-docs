Customers Integrations
======

Customer integrations refer to the connections your customers establish with various platforms, such as Instagram, Facebook, and others the, see [Show merchant settings](#merchant-settings) to check available integrations.

When interacting with customer integrations, you’ll use the x-customer-token for secure access to customer-specific data.

**Customer Integration Status**: Every customer integration is prompted to be expired or have the token revoked by the customer, with that, you can check the `status` field of the customer integration to check if the integration is active. See the [Show a customer integration](#show-a-customer-integration) for more status details.

Endpoints:

- [Create a customer integration session](#create-a-customer-integration-session)
- [Show a customer integration](#show-a-customer-integration)
- [Delete a customer integration](#delete-a-customer-integration)

Create a customer integration session
--------------

This endpoint allows you to create a session for customers to manage and integrate their networks. The session acts like a "checkout" process, where the customer can view existing integrations and other available networks for integration.

* `POST /customer-integrations/session` will return an object containing the session details, including a session link (`session_link`) that the customer will use to access their integration management page.

**Optional parameters**: `redirect_url` Url that shows up in the button at the footer of the web page, used as a final redirect after the customer finishes integrating the accounts.

**Authorization**: Both the `Authorization` header (Bearer token) and customer api_token (`x-customer-token`) must be provided in the request headers.

**Session Expiry**: The session has a duration of `5 minutes`, after that if the link is accessed, `401 Unauthorized` will be returned.

**Session Link**: Once a session is generated, you might access or redirect the customer to `session_link`, this will display the web page where the user will be able to manage current and new integrations. 

###### Example JSON Request
<!-- START POST /customer-integrations/session -->
``` json
{
  "redirect_url": "https://reportei.com/dashboard"
}
```

###### Example JSON Response
<!-- START POST /customer-integrations/session -->
```json
{
  "integration_session": {
    "session_uuid": "679e77d9-b270-4fb9-9f2c-27bcaebddc52",
    "session_link": "http://connect.reportei.com/customer-integrations/session/679e77d9-b270-4fb9-9f2c-27bcaebddc52",
    "expires_at": "2024-10-02T06:14:50.898761Z",
    "merchant": "Reportei",
    "merchant_uuid": "c1e6c85a-6441-4107-ab36-b8bf581b40e0",
    "customer": "Reportei Customer",
    "customer_uuid": "073c1e15-94d0-49b3-9861-a0e9b7ffb06c",
    "redirect_url": "https://reportei.com/dashboard"
  }
}
```
<!-- END POST /customer-integrations/session -->
###### Copy as cURL

``` shell
curl -s -X POST -H "Authorization: Bearer $ACCESS_TOKEN" \
-H "x-customer-token: $CUSTOMER_TOKEN" \
https://connect.reportei.com/customer-integrations/session
```

Show a customer integration
--------------

* `GET /customer-integrations/{$uuid}` will return an object containing the customer integration.

Possible statuses: `active`, `expired`, `revoked`.

If an integration has a status different than `active`, in order to enable it again, you need to create a new session and prompt the user to reintegrate the network, there will be a text message indicating that the integration needs attention.

###### Example JSON Response
<!-- START GET /customer-integrations/{$uuid} -->
```json
{
  "customer_integration": {
      "uuid": "4addc0da-8583-4dbb-a0e9-c7e2e8470f50",
      "source_name": "reportei",
      "status": "active",
      "created_at": "2024-09-24 17:08:08",
      "updated_at": "2024-09-24 17:08:08",
      "integration": {
        "name": "Instagram Business",
        "slug": "instagram_business"
      }
  }
}
```
<!-- END GET /customer-integrations/{$uuid} -->
###### Copy as cURL

``` shell
curl -s -H "Authorization: Bearer $ACCESS_TOKEN" \
-H "x-customer-token: $CUSTOMER_TOKEN" \
https://connect.reportei.com/customer-integrations/{$uuid}
```

Delete a customer integration
--------------

* `DELETE /customer-integrations/{$uuid}?session_id={$session_uuid}` will delete a customer integration with {{$uuid}}.

**Required Parameters**: This endpoint requires you to pass both the integration uuid and a valid session uuid.

###### Example JSON Response
<!-- START DELETE /customer-integrations/{$uuid}?session_id={$session_uuid} -->
```json
{
  "success": true,
  "message": "Record successfully removed"
}
```
<!-- END DELETE /customer-integrations/{$uuid}?session_id={$session_uuid} -->
###### Copy as cURL

``` shell
curl -s -H "Authorization: Bearer $ACCESS_TOKEN" https://connect.reportei.com/customer-integrations/{$uuid}
```