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