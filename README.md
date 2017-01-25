# protractor-error

A Jasmine wrapper for re-running failed Jasmine tests in Protractor. In the current state, this test runner identifies errors based on the
spec description. If your test suite has collisions in spec descriptions, then the errors run will re-run all specs that match the 
description.

# install

`npm install --save-dev protractor-error` or `npm install -g protractor-error` to add cli

# setup

Require the protractor-error module inside the Protractor config `onPrepare` function. This will execute the function
that adds a `JUnitXmlReporter` to the Jasmine environment. If the `params.errorsRun` flag is set, the module will execute only errored specs 
from the most recent run inside the directory `params.errorsPath`. The error output is written to the directory 
`params.errorsPath` + `params.currentTime`.


# configuration

The module is configured by passing the following args:

`params.errorsPath`: string, directory where the `JUnitXmlReporter` will write output and the module will look for previous run data

`params.currentTime`: string, timestamp of the current test run. Triggering the test with the `protractor-error` cli runner will
set this value automatically.

`params.errorsRun`?: boolean, default `false`, should the module limit the current run to previous errors

Example:

`protractor config.js --params.errorsPath 'jasmineReports' --params.currentTime '2017-01-24T23:53:06' --params.errorRun true`

or 

`protractor-error config.js --params.errorsPath 'jasmineReports' --params.errorRun true`

# cli

To automate setting the `param.currentTime` argument, trigger your protractor tests using the cli.

To run, either install `protractor-error` globally and call: `protractor-error <config> [args]` from the command line, with
the same parameters you would call `protractor`. Or call the script by referencing the node_modules file directly: 
`./node_modules/protractor-error/bin/protractor-error.js <config> [args]`. 