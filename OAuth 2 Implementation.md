## Purpose
this document provides a guide/specification for Dudu system.

## Obtain Token

Any implementations of front-end (mobile, web. etc)
```
     +--------+                               +------------------+
     |        |--(A)- Authorization Request ->|     Resource     |
     |        |                               |     Owner        |
     |        |<-(B)- Username and Password -—|                  |
     |        |                               +------------------+
     |        |
     |        |                               +------------------+
     |        |--(C)- Username and Password ->|  Dudu Shopping   |
     | Client |                               |  Authentication  |
     |        |<-(D)----- Access Token -------|  Server          |
     |        |                               +------------------+                  
     |        |                               
     |        |                               +------------------+
     |        |--(E)----- Access Token ------>|  Resource        | 
     |        |                               |  Server          |
     |        |<-(F)--- Protected Resource ---|                  |
     +--------+                               +------------------+
```

Authentication request is username and password.
```
    HTTP/1.1 200 OK
    Content-Type: application/json
    {
      "username":"jack",
      "password":"password"
    }
```

Token response
```
    HTTP/1.1 200 OK
    Content-Type: application/json;charset=UTF-8
    Cache-Control: no-store
    Pragma: no-cache 
    {
      "accessToken":"mF_9.B5f-4.1JqM",
      "tokenType":"Bearer",
      "expiresIn":3600,
      "refreshToken":"tGzv3JOkF0XG5Qx2TlKWIA"
    }
```

Refresh tokens are credentials used to obtain access tokens with same scope. Refresh Token has an implicit expiration time, for example double of expiresIn.

## Make Request With Token
The clients use `Bear` authentication scheme.
An example
```
    GET /resource HTTP/1.1
    Host: server.example.com
    Authorization: Bearer mF_9.B5f-4.1JqM
```

## Server Response to Request Failures
When a request fails, the resource server responds using the appropriate HTTP status code:

- `invalid_request`
      The request is missing a required parameter, includes an
      unsupported parameter or parameter value, repeats the same
      parameter, uses more than one method for including an access
      token, or is otherwise malformed.  The resource server SHOULD
      respond with the HTTP 400 (Bad Request) status code.
- `invalid_token`
      The access token provided is expired, revoked, malformed, or
      invalid for other reasons.  The resource SHOULD respond with
      the HTTP 401 (Unauthorized) status code.  The client MAY
      request a new access token and retry the protected resource
      request.
- `insufficient_scope`
      The request requires higher privileges than provided by the
      access token.  The resource server SHOULD respond with the HTTP
      403 (Forbidden) status code and MAY include the "scope"
      attribute with the scope necessary to access the protected
      resource.

WWW-Authenticate is set. following fields are set type, realm, scope.

- type
  it is `Bear`
- `realm`
   A string to be displayed to users so they know which username and
   password to use. This string should contain at least the name of
   the host performing the authentication and might additionally
   indicate the collection of users who might have access.
- `scope`
   `scope` attribute is a space-delimited list of case-sensitive scope
   values indicating the required scope of the access token for
   accessing the requested resource.

example
```
    HTTP/1.1 401 Unauthorized
    WWW-Authenticate: Bear
    realm="testrealm@host.com",
    scope="costumer,saleAgent”
```

## Scopes
Each API endpoint has one/more scope associated with it. 
An token is issue with one or more scopes to resource owner. 
An endpoint can be access only when the owner hold a scope contains it. 
Endpoints with empty scope can be accessed by any valid tokens.




