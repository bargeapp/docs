# Javascript Tests

## Introduction

Javascript tests are supported by integrating with Github. The easiest way to integrate is just to sign up using your Github account. You can also sign up with your email address but you'll need to run some extra steps to get things working (instructions will appear on the project page).

## Supported Frameworks

At the moment Barge supports PhantomJS and CasperJS written in JavaScript or CoffeeScript. If you'd like to see Barge support another framework please let us know by emailing us at <a href="mailto:hello@bargeapp.com">hello@bargeapp.com</a>.

## Getting Started

After enabling repository you'll need to add the `@barge` comment to your scripts. This is just a comment at the top of your scripts that starts with `@barge` and takes optional parameters (below).

## @barge parameters

Though none of the parameters are _technically_ required we *highly* recommend explicitly setting the `suite` and `framework`.

Name | Description
---- | -----------
suite | Named grouping for the script.
framework | This is the command you would run to execute the test locally. One of: [`phantomjs`, `casperjs`, `casperjs test`]. If left blank we'll attempt to auto-determine the framework.
args | Command line arguments to pass to the framework.

**Example Javascript:** `// @barge suite="User Signup" framework="casperjs" args="--ssl-protocol=any"`

**Example CoffeeScript:** `# @barge suite="User Signup" framework="casperjs" args="--ssl-protocol=any"`