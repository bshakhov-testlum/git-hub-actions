# API Testing

## REST API
> `http`

**Description:** command for conducting http queries

**Required parameters for HTTP command:**

1. `comment`
2. `alias` - unique name of the API you configured in your integration.xml file


**Optional parameters:**

`condition` - condition according to which this test step will or won't be executed

`threshold` - parameter, where the maximum execution time of the command is defined (milliseconds), if the execution time is exceeded, the step will be defined as failed

**Available HTTP methods:**

```
GET
POST
PUT
DELETE
PATCH
HEAD
OPTIONS
TRACE
```

**Parameters for HTTP methods:**

1. `endpoint` - endpoint for your query
2. `response`
   1. `code` - expected response code
   2. `file` - file with expected result for particular query
3. `header`
   1. `name` - name of header
   2. `data` - data which header has to contain
4. `body` (for those methods, which require body)
   1. `from`
      1. `file` - json file that contains body of your request. This file must be named "request_N.json", where N is number of your test step
   2. `param`
      1. `name` - name of parameter
      2. `data` - data which parameter has to contain
   3. `multipart`
      1. `file`
         1. `name` - key
         2. `fileName` - value
         3. `contentType`
   4. `raw` - you can put your request body just as raw in scenario without file

> **In the middle of the methods there should be a sequence:**
> 1. `response`
> 2. `header`
> 3. `body/param`

### Usage example
```xml
<http comment="Check ability to login added user with valid credentials" alias="MEGA_APP">
   <post endpoint="/jwt/login">
      <response code="200" file="expected_3.json"/>
      <header name="Content-Type" data="application/json"/>
      <body>
         <raw>
            {
            "username": "testlum",
            "password": "testlum123"
            }
         </raw>
      </body>
   </post>
</http>
```

> **A full description of API testing can be found** [here](https://testlum.developerhub.io/version-2/apis)
