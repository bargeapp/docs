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

## Endpoints

See the <a href="#javascript-tests">Javascript Tests</a> and <a href="#selenium-tests">Selenium Tests</a> pages for specific endpoints