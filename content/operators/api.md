---
title: "API Operator"
weight: 1
---
The Command operator is used to execute a command on the system.

## Syntax

```yaml
- api: https://postman-echo.com/get?foo1=bar1&foo2=bar2
  jsonKey: headers.host
  setEnv: apiResponse
```

* `api`: This is the endpoint that you want to execute against, this is also known as the API Endpoint.
* `outputFile`: Given the response that is received the body will be written to this directory.
* `method`: Supports the standard http methods for instance GET/PUT/POST/DELETE
* `body`: Body that will be added to the request.
* `headers`: Array of strings representing headers to be added as key value parirs, keys and values are separated by `:`, Ex: `BasicAuth: foo`
* `jsonKey`: Uses dot notation on the response json object to retrieve a specific value.
* `setEnv`: This works in conjunction with jsonKey and will set the output of the jsonKey to the environment variable.
* `onlyIf`: This sub command will run and if an output is received it will return true and thus allow execution
* `notIf`: This sub command will run and if an output is received it will return false and thus prevent execution

## Examples
### Example 1
```yaml
- api: https://postman-echo.com/get?foo1=bar1&foo2=bar2
  jsonKey: headers.host
  setEnv: apiResponse
```

For reference this request would return a result like this:
```json
{
  "args": {
    "foo1": "bar1"
  },
  "headers": {
    "host": "postman-echo.com",
    "x-forwarded-proto": "http",
    "x-request-start": "t1733099457.114",
    "connection": "close",
    "x-forwarded-port": "443",
    "x-amzn-trace-id": "Root=1-674cffc1-1f5b5d6c43626f5c6bdc3b92",
    "user-agent": "curl/7.81.0",
    "accept": "*/*"
  },
  "url": "http://postman-echo.com/get?foo1=bar1"
}
```

In this example a GET request is made to the postman-echo.com endpoint with the query parameters foo1=bar1 and foo2=bar2. The response is then parsed and the value of the headers.host key is set to the apiResponse environment variable. This makes it incredibly easy to use the response of an API call in subsequent operators.  One useful use for this is to retrieve a vault token and then use it in subsequent operators.

### Example 2

```yaml
- api: https://postman-echo.com/post?test=123
  method: POST
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

Since I set the `jsonKey` to `data` key in the reponse the apiResponse environment variable will be "The quick brown fox jumps over the lazy dog!".  The full response will be written to the /tmp/apiResponse2.json file.  As you can see you can use the api operator to interact with any API and use the results in subsequent operators, or to trigger requests, save data etc.  One of the more useful use cases is to kick off a new brucedom action once a specific event occurs within the local environment by using the API operator to trigger the new action.

In the next section, we'll discuss the Command operator and how to use it in your manifest files.