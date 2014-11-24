# Enabling Barge

After signing up and enabling a repository you'll need to add the `@barge` comment to your scripts. This is just a comment at the top of your scripts that starts with `@barge` and takes optional parameters (below).

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