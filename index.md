## Overview

- This is a REST API based primarily on the JSON API standard (http://jsonapi.org/).
- Authorization is similar to the Client ID / Client Secret strategy of OAuth 2.
- All GET requests return collections.
	- List operations also include a meta key which contains, at the least, pagination information.
	- Show operations typically include more information about the requested resource than their equivalent representation in a list operation.
- Pagination is implemented using the `page` query string parameter.

## Authorization

### User API

Use `X-AUTH-Token` HTTP header.

### Partner API

- Headers: Use `X-CLIENT-ID` and `X-CLIENT-SECRET` HTTP headers
- Query String Parameters: Use `client_id` and `client_secret`
- Payload: For POST/PUT requests, the payload may contain `client_id` and `client_secret`

## Payload Formats:

Payload bearing API requests should be sent as JSON payloads with headers set properly:

   Content-Type: application/json
   Accept: application/json

## Endpoints

Root: https://rev-insite.com/

### User

#### Categories

* List

  `GET /api/v1/categories`

#### Impressions

* List

  `GET /api/v1/impressions`

#### Invitations

* List

  `GET /api/v1/invitations`

* Create

  `POST /api/v1/invitations`

  Payload:

  ```
  {
    "invitation": {
      "email": string,
      "vendor_id": integer, // optional, may only be specified for existing vendors, although email takes precedence if present
      "name": string,
      "company": string,

      "category": string, // must only be specified for new vendors

      // optional
      "phone": string,
      "business_type": string
    }
  }
  ```

#### Partnerships

* List

  `GET /api/v1/partnerships`

  Params: `provider_directory_id` or `service_provider_id`

### Partner

* List

  `GET /api/partner/v1/accounts`

* Create

  `POST /api/partner/v1/accounts`

  Payload:

  ```
  {
    "account": {
      "name": “John Doe",
        "email": "test@test.test",
        "company": "Company",
        "zip": "02203"
    }
  }
  ```

* Show

  `GET /api/partner/v1/accounts/:id`

* Update

  `PUT /api/partner/v1/accounts/:id`

  Payload: same as `create`
