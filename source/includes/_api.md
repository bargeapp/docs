# API

Barge provides a RESTful, JSON-based API for running tests and retrieving results.

## Authentication

Just append your API key to an HTTP header named `API_KEY` or a query string parameter named `api_key`. Note: for the examples we'll be using the HTTP header method for POSTs and the query string parameter for GETs.