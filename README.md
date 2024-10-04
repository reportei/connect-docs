The Reportei Connect API
==================

Welcome to the Reportei Connect API! If you're looking to integrate your application with Reportei, you're in the right place. We're happy to have you!

## Getting Started

To use this API, you'll need the following:

- An API key (Bearer Token) for authentication.
- The `x-customer-token` for endpoints that interact with specific customer data
- Download the Postman collection for this API from [here](./sections/Reportei%20Connect.postman_collection.json)

## Authentication

All API requests require authentication via the `Authorization` header using a Bearer token. For endpoints that deal with customer-specific data, you also need to provide an `x-customer-token`.

### Bearer Token Authentication

Include the Bearer token in the `Authorization` header of your API requests:

```
Authorization: Bearer {access_token}
```

### Bearer Token + Customer Token

For customer-specific endpoints, both the Bearer token and the `x-customer-token` must be included:

```
Authorization: Bearer {access_token}
x-customer-token: {customer_token}
```

The `x-customer-token` is provided when you create a customer and is necessary for any subsequent customer-related requests. Make sure to store it securely.

## Pagination

Most list endpoints are paginated. You can control the page size and navigate through pages using query parameters. Each paginated response includes metadata, such as total entries and current page, to help manage results efficiently.

### Example Paginated Response:

```json
{
  "data": [
    {
      "uuid": "caedbbbe-7d93-476f-b965-bf97cd7ce874",
      "name": "Reportei Customer 1",
      "created_at": "2024-09-24 17:07:34",
      "updated_at": "2024-09-24 17:07:34"
    }
  ],
  "meta": {
    "current_page": 1,
    "from": 1,
    "last_page": 1,
    "per_page": 15,
    "to": 2,
    "total": 2
  }
}
```

### Pagination Parameters:

- `page` (optional): The current page number. Default is `1`.
- `per_page` (optional): The number of items per page. Default is `15`.

## Error Handling

All errors will return an HTTP status code alongside a descriptive message in the response body. Common status codes include:

- `401 Unauthorized`: Authentication failure, invalid or missing Bearer token or `x-customer-token`.
- `403 Forbidden`: Access to the resource is not allowed.
- `404 Not Found`: The requested resource could not be found.
- `500 Internal Server Error`: Something went wrong on our end.

### Example Error Response:

```json
{
  "response": "Invalid Customer Token"
}
```

## Response Formats

All API responses are returned in JSON format.

### Example Successful Response:

```json
{
  "customer": {
    "uuid": "caedbbbe-7d93-476f-b965-bf97cd7ce874",
    "name": "Reportei Customer",
    "created_at": "2024-09-24 17:07:34",
    "updated_at": "2024-09-24 17:07:34",
    "merchant": "Reportei"
  }
}
```

## Rate Limits

To ensure optimal performance and fairness, the API enforces rate limits. The rate limits are displayed in the response headers of each request. For more details on your current rate limits, you can check the merchant settings via the `/merchants/settings` endpoint.

-------

These API docs are licensed under [Creative Commons (CC BY-SA 4.0)](http://creativecommons.org/licenses/by-sa/4.0/). Please share, remix, and distribute as you see fit.
