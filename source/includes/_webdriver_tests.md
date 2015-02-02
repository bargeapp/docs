# Selenium Tests


## Introduction

Selenium tests enable you to run your _existing_ selenium tests at scale with minimal code changes. You can easily configure your CI tool to run regular Selenium tests on every check-in and Barge tests nightly.

## Getting Started

Selenium tests are meant to be run via the API. You can think of the steps involved as similar to the Arrange Act Assert pattern of unit testing:

There are 3 steps to running a Selenium test on Barge:

1. Tell Barge to start a Webdriver session (api call)
2. Run your test with the Selenium Remote WebDriver using the server information returned from the previous API call
3. Tell Barge to start a test (api call)

## Starting a session

```shell
# you'll need to change the api_key below
curl -X POST -H 'Content-Type: application/json' -H "API_KEY: 123456789abcdef" https://www.bargeapp.com/api/webdriver_sessions
```

POST to `/api/webdriver_sessions`

This will return JSON with the following properties:

name | description
---- | -----------
id | the id of the session
status | the status of the session
ip | the ip address of the server
port | the port of the server
created_at | timestamp

## Running the Test (locally)

```ruby
driver = Selenium::WebDriver.for(:remote, :url => "http://#{ip}:#{port}/")
```
```javascript
// using webdriver.io
client = webdriverio.remote({host: ip, port: port }.init();
```
```coffeescript
# using webdriver.io
client = webdriverio.remote({host: ip, port: port }.init()
```

After you've started a session (above) you'll run your script locally using the Remote Webdriver.

## Running the Barge test

After the local script has finished running you're ready to run a Barge test.

```shell
# you'll need to change the api_key below
curl -X POST -H 'Content-Type: application/json' -H "API_KEY: 123456789abcdef" -d '{"webdriver_session_id": 101, "users": 100, "minutes": 10}' https://www.bargeapp.com/api/tests/create_webdriver
```