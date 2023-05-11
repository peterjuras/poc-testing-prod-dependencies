# poc-testing-prod-dependencies

Proof of concept on how a production build of a Node.js lambda without dev dependencies could be validated.

**Main idea:**

Run the main script that contains the lambda handler. The handler function is not called, therefore the business logic will not run, but static imports will be evaluated and therefore the script will crash if a dependency is missing.

**Usage**

To run the poc:

1. Run `./test.sh`
   -> It should exit without error
2. Run `./test-prod-dependencies.sh`
   -> It will crash.

**Note:**

There are a lot of cases where this will not work, examples:

- Top level code that requires context (e.g. SNS, S3, other AWS clients)
- Code that uses dynamic imports
- Likely many others :)
