# API

Barge provides a RESTful, JSON-based API for running tests and retrieving results.

## Authentication

Just append your API key to an HTTP header named `API_KEY` or a query string parameter named `api_key`. Note: for the examples we'll be using the HTTP header method.

```shell
curl https://www.bargeapp.com/api/suites/1?api_key=123456789abcdef
# OR
curl -H "API_KEY: 123456789abcdef" https://www.bargeapp.com/api/suites/1
```
<aside class="notice">
Don't forget to replace `123456789abcdef` with your API key (available in the Account page)
</aside>

## Start a suite test

POST the following parameters to `/api/suites`

```shell
# you'll need to change the api_key, project, and name parameters below
curl -X POST -H 'Content-Type: application/json' -H "API_KEY: 123456789abcdef" -d '{"project": "/torvalds/linux","name": "Users"}' https://www.bargeapp.com/api/suites
```
This will return JSON with the following properties:

name | description
---- | -----------
id | the `id` of the suite test created
baseline | the suite baseline
baseline_multiple | the baseline multiple to use - multiply the baseline by this number to determine the op/s to be tested

```json
{"id":1,"baseline_multiple":1,"baseline":100}
```

## Retrieving suite test

After starting a suite test you can check on the status of the test by executing a GET against `/api/suites/:id`

```shell
# you'll need to change the api key and suite id
curl -X GET -H 'Content-Type: application/json' -H "API_KEY: 123456789abcdef" https://www.bargeapp.com/api/suites/1
```
This will return JSON with the following properties:

name | description
---- | -----------
status | one of [`pending`, `booting`, `preparing`, `running`, `finished`]
tests | if `status` is `finished` then this will contain an array of `test` objects

```json
{"status": "finished", "tests": [{"id": 1}]}
```

## Retrieving test results

After a suite test has finished you can retrieve the test results for each test by executing a GET against `/api/tests/:id`

```shell
# you'll need to change the api_key and test id
curl -X GET -H 'Content-Type: application/json' -H "API_KEY: 123456789abcdef" https://www.bargeapp.com/api/tests/1
```

This will return JSON with the following properties:

name | description
---- | -----------
status | status of the test, one of [`pending`, `booting`, `preparing`, `running`, `finished`]
resource_events | an array of resource objects grouped by second and url

```json
{"status": "finished", "resource_events":[{"url": "http://www.bargeapp.com", "time": "2014-11-10T01:22:28.810", "failures": 0, "successes": 1000}]}
```
