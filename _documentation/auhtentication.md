---
title: Authentication & Codes
position: 7
---

The main way of API authentication is a client token provided along with your **Hurakann** credentials, so sending this value in the headers of each
request will be enough.

If not provided `Ckey` is sent then the API will return an auth error code: `401 Unauthorized`
{: .error}

The uri is built with a prefix of `v1` for all listed API endpoints, for example: `/v1/user/file`
{: .info}

The next are a list of http codes returned by the API and its meaning

| Code | Name | Description |
|------|------|-------------|
| 200  | Ok   | Success     |
| 201  | Created | Creation successful |
| 204  | No Content | No content in response, similar to 404 but for GET |
| 400  | Bad Request | Something went wrong in the core |
| 404  | Not Found | Some attribute provided in the request was not found in the datastore |
| 501  | Not Implemented | Could not resolve the uri |
| 401  | Unauthorized | No ckey present or not found in datastore (wrong token) |
| 412  | Precondition Failed | Some required attribute was not send in the request | 

