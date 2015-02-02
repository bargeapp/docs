# Javascript Tests

## Introduction

Javascript tests are supported by integrating with Github. The easiest way to integrate is just to sign up using your Github account. You can also sign up with your email address but you'll need to run some extra steps to get things working (instructions will appear on the project page).

## Supported Frameworks

At the moment Barge supports PhantomJS and CasperJS written in JavaScript or CoffeeScript. If you'd like to see Barge support another framework please let us know by emailing us at <a href="mailto:hello@bargeapp.com">hello@bargeapp.com</a>.

## Getting Started

After enabling repository you'll need to add the `@barge` comment to your scripts. This is just a comment at the top of your scripts that starts with `@barge` and takes optional parameters (below).

## @barge parameters

Though none of the parameters are _technically_ required we *highly* explicitly recommend setting the `suite` and `framework`.

Name | Description
---- | -----------
suite | Named grouping for the script.
framework | This is the command you would run to execute the test locally. One of: [`phantomjs`, `casperjs`, `casperjs test`]. If left blank we'll attempt to auto-determine the framework.
args | Command line arguments to pass to the framework.

```javascript
// @barge suite="User Signup" framework="casperjs" args="--ssl-protocol=any"
```

```coffeescript
# @barge suite="User Signup" framework="casperjs" args="--ssl-protocol=any"
```

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

### Retrieving suite test

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