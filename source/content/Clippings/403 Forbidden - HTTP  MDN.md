---
title: "403 Forbidden - HTTP | MDN"
source: "https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/403"
author:
  - "[[MDN Web Docs]]"
published:
created: 2025-02-15
description: "The HTTP 403 Forbidden client error response status code indicates that the server understood the request but refused to process it.This status is similar to 401, except that for 403 Forbidden responses, authenticating or re-authenticating makes no difference.The request failure is tied to application logic, such as insufficient permissions to a resource or action."
tags:
  - "clippings"
---
The HTTP **`403 Forbidden`** [client error response](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#client_error_responses) status code indicates that the server understood the request but refused to process it. This status is similar to [`401`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/401), except that for **`403 Forbidden`** responses, authenticating or re-authenticating makes no difference. The request failure is tied to application logic, such as insufficient permissions to a resource or action.

Clients that receive a `403` response should expect that repeating the request without modification will fail with the same error. Server owners may decide to send a [`404`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/404) response instead of a 403 if acknowledging the existence of a resource to clients with insufficient privileges is not desired.

## Status

## Examples

### Request failed due to insufficient permissions

The following example request is made to an API for user management. The request contains an [`Authorization`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Authorization) header using `Bearer` [authentication scheme](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication#authentication_schemes) containing an access token:

```example
DELETE /users/123 HTTP/1.1
Host: example.com
Authorization: Bearer abcd123
```

The server has authenticated the request, but the action fails due to insufficient rights and the response body contains a reason for the failure:

```example
HTTP/1.1 403 Forbidden
Date: Tue, 02 Jul 2024 12:56:49 GMT
Content-Type: application/json
Content-Length: 88

{
  "error": "InsufficientPermissions",
  "message": "Deleting users requires the 'admin' role."
}
```

## Specifications

| Specification |
| --- |
| [HTTP Semantics   \# status.403](https://www.rfc-editor.org/rfc/rfc9110#status.403) |
