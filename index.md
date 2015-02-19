---
layout: index
---

## Overview

- This is a REST API based primarily on the JSON API standard (http://jsonapi.org/).
- Authorization is similar to the Client ID / Client Secret strategy of OAuth 2.
- All GET requests return collections.
  - List operations also include a meta key which contains, at the least, pagination information.
  - Show operations typically include more information about the requested resource than their equivalent representation in a list operation.
-Pagination is implemented using the page query string parameter.

## Authorization

The Client ID and Client Secret can be passed to calls in one of three ways:

- Headers:
  - Using the X-CLIENT-ID and X-CLIENT-SECRET http headers
- Query String Parameters:
  - Using the client_id and client_secret query string params
- Post Payload
  - For POST/PUT operations, the payload can also contain the client_id and client_secret params

## Payload Formats:

Payload bearing API requests should be sent as JSON payloads with headers set properly:

    Content-Type: application/json
    Accept: application/json

## Endpoints:

### Accounts:

https://nest4less.com/api/partner/v1/accounts


List

    GET      /api/partner/v1/accounts          (account_list.json)

    curl 'https://nest4less.com/api/partner/v1/accounts' -H 'X-CLIENT-SECRET: <secret>'\
    -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'X-CLIENT-ID: <clientid>'

Create

    POST     /api/partner/v1/accounts          (send account_create_update.json, returns account.json)

    curl 'https://nest4less.com/api/partner/v1/accounts' -H 'X-CLIENT-SECRET: <secret>'\
    -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'X-CLIENT-ID: <clientid>'\
    --data-binary $'{"account": {"name": "Blah Person","email": "test@test.test","company": "Blah Company","zip": "02703"}}'

Show

    GET      /api/partner/v1/accounts/<id>     (account.json)

    curl 'https://nest4less.com/api/partner/v1/accounts<id>' -H 'X-CLIENT-SECRET: <secret>'\
    -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'X-CLIENT-ID: <clientid>'

Update

    PUT      /api/partner/v1/accounts/<id>     (send account_create_update.json, returns account.json)

    curl 'http://nest4less.dev/api/partner/v1/accounts/87' -X PUT -H 'X-CLIENT-SECRET: <secret>'\
    -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'X-CLIENT-ID: <clientid>'\
    --data-binary $'{"account": {"name": "Blah Personz","email": "test@test.test","company": "Blah Company"}}'


## Listening for DOM events emitted by the iFrame

The Nest4Less iFrame emits events that an integration partner can use to track their users' usage.  These events can be capture with code such as:


    window.addEventListener("message", function(event){
      if(event.message.vendorEvent){
        console.log(event.message.vendorEvent);
        console.log(event.message.url);
        console.log(event.message.id);
        console.log(event.message.title);
      }
    }, false);


## iFrame embed params

When embedding the iFrame, there are a couple of options you can pass via query string.

email: dictates where requested resources will be emailed to

share_url: overrides the location where, when a user shares a resource, individuals clicking on that shared resource will be sent

given an embed link:
```
http://nest4less.com/embed/partner2222
```

and params
```
{email: 'test@test.com', share_url: 'http://nest4less.com'}
```

these can be specified by instead embedding
```
http://nest4less.com/embed/partner2222?share_url=http%3A%2F%2Fnest4less.com&email=test%40test.com
```

<script src="https://gist.github.com/nest4less/646d9433399950e07d12.js"></script>
