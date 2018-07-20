## Implementation
A JSON file containing permissions is stored in micro services.
Micro services load the JSON file and check incoming requests.

## Objects
ApiEndpoint
```
ApiEndpointId: Interger. Unique identifier
Method: String. HTTP request method. for example GET, POST
Endpoint: String. The path of incoming url. It support wildcard `*`. `*` greedly matches any one or more characters except `/`
IsPublic: Boolean. true if this API is open to the Internet without any credentials. default false
```

Scope
```
ScopeName: String. Unique name
ApiEndpoints: Set. the set of ApiEndpointId.
```

## Permission JSON file
Schema
```
{
  "ApiEndpoints": [ApiEndpoint,]
  "Scopes": [Scope,]
}
```

An example
```
{
  "ApiEndpoints": [
    {
      "ApiEndpointId": 1,
      "Method": "GET",
      "Endpoint": "/resource",
    },
    {
      "ApiEndpointId": 2,
      "Method": "POST",
      "Endpoint": "/wallet",
    },
    {
      "ApiEndpointId": 3,
      "Method": "POST",
      "Endpoint": "/login",
      "IsPublic": true
    },
    {
      "ApiEndpointId": 2,
      "Method": "POST",
      "Endpoint": "/wallet/*/*",
    },
  ],
  "Scopes": [
    {
      "ScopeName": "Customer",
      "ApiEndpointIds": [1,2]
    }
  ]
}
```

