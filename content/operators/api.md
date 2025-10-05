---
title: "API Operator"
weight: 1
---
The API operator performs HTTP(S) requests and makes the response available to subsequent steps via files or environment variables.

## Syntax

```yaml
- api: https://postman-echo.com/get?foo1=bar1&foo2=bar2
  method: GET
  headers:
    - "Accept: application/json"
  outputFile: /tmp/example.json
  jsonKey: headers.host
  setEnv: apiResponse
```
* `api`: The API endpoint (URL). Supports templating with environment variables (e.g., `https://api.example.com/{{.APP_ENV}}`).
* `outputFile`: If set, writes the full response body to this file path (directories are created as needed).
* `method`: HTTP method. Defaults to `GET`. Supports `GET`, `POST`, `PUT`, `DELETE`, etc.
* `body`: Request body content. May be a literal string or a template source. If it begins with `file://`, `http(s)://`, or `s3://`, the body is loaded and templated from that location; otherwise the literal string is templated.
* `headers`: Array of `Key: Value` strings added to the request headers (e.g., `"Authorization: Bearer {{.TOKEN}}"`).
* `setBodyEnv`: Sets the entire response body into the named environment variable.
* `setEnv`: Used with `jsonKey` to set a specific JSON field's value into an environment variable.
* `jsonKey`: Dot-notation path to a string field in the JSON response (e.g., `data.token`).
* `onlyIf`: [See detailed docs here](/operators/sub-commands)
* `notIf`: [See detailed docs here](/operators/sub-commands)
* `exitIf`: [See detailed docs here](/operators/sub-commands)

## Examples
### Example 1

```yaml
- api: https://postman-echo.com/get?foo1=bar1&foo2=bar2
  method: GET
  headers:
    - "Accept: application/json"
  outputFile: /tmp/example.json
  jsonKey: headers.host
  setEnv: apiResponse
```
In this example a GET request is made to the postman-echo.com endpoint with the query parameters foo1=bar1 and foo2=bar2. The response is then parsed and the value of the headers.host key is set to the apiResponse environment variable. This makes it incredibly easy to use the response of an API call in subsequent operators.  One useful use for this is to retrieve a vault token and then use it in subsequent operators.

### Example 2

```yaml
- api: https://postman-echo.com/post?test=123
  method: POST
  headers:
    - "Content-Type: application/json"
  body: "The quick brown fox jumps over the lazy dog!"
  setEnv: apiResponse
  jsonKey: data
  outputFile: /tmp/apiResponse2.json
```
In this example we post a short message and read the return results from the data key in the response.  We also write the entire response to a file in the /tmp directory.  The full example response that we received from the server looks like this:
```json
{
  "args": {
    "test": "123"
  },
  "data": "The quick brown fox jumps over the lazy dog!",
  "files": {},
  "form": {},
  "headers": {
    "host": "postman-echo.com",
    "x-forwarded-proto": "http",
    "x-request-start": "t1733100727.944",
    "connection": "close",
    "content-length": "21",
    "x-forwarded-port": "443",
    "x-amzn-trace-id": "Root=1-674d04b7-4b23323952854e6d6bd343a6",
    "accept-encoding": "gzip",
    "user-agent": "Go-http-client/2.0",
    "content-type": "application/json"
  },
  "json": null,
  "url": "http://postman-echo.com/post?test=123"
}
```
Since the `jsonKey` is set to `data`, the `apiResponse` environment variable will be "The quick brown fox jumps over the lazy dog!". The full response is written to `/tmp/apiResponse2.json`. You can use the API operator to interact with any API, then use results in subsequent operators or to trigger follow-up actions.

### Example 3: Using a templated request body from a file/URL/S3

```yaml
- api: https://example.com/auth
  method: POST
  headers:
    - "Content-Type: application/json"
  body: file:///etc/bruce/payloads/login.json.tmpl
  setBodyEnv: AUTH_RESPONSE
```
In this example, the body is loaded from a local template file and rendered using current environment variables before being sent.

In the next section, we'll discuss the Command operator and how to use it in your manifest files.