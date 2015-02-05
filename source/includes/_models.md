# Models

## Suite Test

name | description
---- | -----------
id | id of the suite test
javascript_project_id | id of the project
suite | name of the suite
users | number of users
minutes | minutes to run 
status | {pending, booting, preparing, running, finished}
created_at | timestamp
tests | array

## POST Suite Test

> you'll need to change the api_key, project id, and suite parameters below

```http
POST /api/suite_tests HTTP/1.1
Host bargeapp.com
Content-Type: application/json

{
  "api_key": "API_KEY",
  "javascript_project_id": 1,
  "suite": "Signup",
  "users": 100,
  "minutes": 10
}
```

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": 1,
  "javascript_project_id": 1,
  "suite": "Signup",
  "users": 100,
  "minutes": 10,
  "tests": [
    {
      "id": 1,
      "status": "pending",
      "result": "pending",
      "resource_summaries": [],
      "assertion_summaries": [],
      "script": {
        "id": 1,
        "name": "/test-signup.js"
      }
    }
  ]
}
```

POST to `/api/suite_tests` to start a suite test (a test that runs all scripts in a suite)


## GET Suite Test

> you'll need to change the api_key below

```http
GET /api/suite_tests/1 HTTP/1.1
Host bargeapp.com
Content-Type: application/json

{
  "api_key": "API_KEY"
}
```

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": 1,
  "javascript_project_id": 1,
  "suite": "Signup",
  "users": 100,
  "minutes": 10,
  "tests": [
    {
      "id": 1,
      "status": "finished",
      "result": "finished",
      "resource_summaries": [
        {
          "url": "http://www.google.com",
          "successes": 10000,
          "failures": 0
        }
      ],
      "assertion_summaries": [
        {
          "message": "Search button appears",
          "successes": 9000,
          "failures": 1000
        }
      ],
      "script": {
        "id": 1,
        "name": "/test-signup.js"
      }
    }
  ]
}
```

GET `/api/suite_tests/:id` to get details on a suite test

## Test

There are two types of tests: Javascript and Selenium. Currently running Javascript tests via the API is only suppored using the Suite Test endpoints.

name | description
---- | -----------
id | id of the test
type | {JavascriptTest, WebdriverTest}
status | status of the test
users | number of users
minutes | minutes to run 
status | {pending, booting, preparing, running, finished}
suite_test_id | id of the suite test
suite_test | suite test object
script | script object
resource_summaries | array
assertion_summaries | array
created_at |
tests | array

## POST Test
> you'll need to change the api_key, users, minutes and webdriver_session_id below

```http
POST /api/tests/create_webdriver HTTP/1.1
Host bargeapp.com
Content-Type: application/json

{
  "api_key": "API_KEY",
  "users": 100,
  "minutes": 10,
  "webdriver_session_id": 1
}
```

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": 1,
  "status": "pending",
  "users": 100,
  "minutes": 10,
  "resource_summaries": []
}
```

POST to `/api/tests/create_webdriver` to create a Webdriver test

## GET Test

> you'll need to change the api_key below

```http
GET /api/tests/1 HTTP/1.1
Host bargeapp.com
Content-Type: application/json

{
  "api_key": "API_KEY"
}
```

```http
HTTP/1.1 200 Success
Content-Type: application/json

{
  "id": 1,
  "status": "finished",
  "suite": "Signup",
  "users": 100,
  "minutes": 10,
  "type": "JavascriptTest"
  "suite_test_id": 1,
  "suite_test": {
    "id": 1,
    "suite": "Signup"
  },
  "resource_summaries": [
    {
      "url": "http://www.google.com",
      "successes": 10000,
      "failures": 0
    }
  ],
  "assertion_summaries": [
    {
      "message": "Search button appears",
      "successes": 9000,
      "failures": 1000
    }
  ],
  "script": {
    "id": 1,
    "name": "/test-signup.js"
  }
}
```

GET `/api/tests/:id` to get details on a test

## Webdriver Session

A Webdriver Session represents a remote server listening for webdriver commands. Running a Selenium test on Barge requires creating a Webdriver Session, waiting for it to be ready, running the script with the Selenium Remote Webdriver configured to use the session's ip and port, then creating a test.

name | description
---- | -----------
id | id of the session
status | status of the session
ip | ip of the remote server
port | port of the remote server

## POST Webdriver Session
> you'll need to change the api_key below

```http
GET /api/webdriver_sessions HTTP/1.1
Host bargeapp.com
Content-Type: application/json

{
  "api_key": "API_KEY"
}
```
```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": 1,
  "status": "pending",
  "ip": "",
  "port": ""
}
```

POST to `/api/webdriver_sessions`

## GET Webdriver Session

> you'll need to change the api_key below

```http
GET /api/webdriver_sessions/1 HTTP/1.1
Host bargeapp.com
Content-Type: application/json

{
  "api_key": "API_KEY"
}
```
```http
HTTP/1.1 200 Success
Content-Type: application/json

{
  "id": 1,
  "status": "running",
  "ip": "127.0.0.1",
  "port": "8001"
}
```