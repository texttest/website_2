---
layout: how_to_guide
title: Running tests unattended
---

# Running tests unattended in CI

Sometimes you want to run the tests on the command-line, and simply receive a report of what passed and failed. Typically this is when you are on some kind of Continuous Integration server. TextTest supports 'Batch Mode' for precisely this usecase.

## HTML Report

To enable TextTest to track the results of unattended test runs, add these lines to your config file:

    [batch_result_repository]
    ci:${TEXTTEST_HOME}/ci_results
    [end]
    
    [historical_report_location]
    ci:${TEXTTEST_HOME}/ci_reports
    [end]

This creates a new batch report called 'ci'. It will accumulate test results in the folder `${TEXTTEST_HOME}/ci_results` (in TextTest's own internal format), and will be able to collate all these results as an html report in `${TEXTTEST_HOME}/ci_reports`.

To trigger a batch test run that will write results into the first folder, run this command:

    texttest -b ci -name `date`

The flag `-name` is to give this run a unique name, it doesn't have to be the date.

To generate an html report from all the results gathered in the `batch_results_repository`, collate them with this command:

    texttest -b ci -coll

This should create some files under the folder specified for `historical_report_location`. Open 'index.html' in a browser.

## Keeping a history of test results
In the example above, both the test results location and the test report location are given relative to `$TEXTTEST_HOME` which may vary according to which machine you are running the tests on. It can be useful to gather all test results to the same folders so it doesn't matter which machine is used for the CI run. In this case replace `$TEXTTEST_HOME` with a path to a commonly accessible network location.

## Running only some of the tests
It can be useful to specify only a subset of the tests to run in CI, but run all of them on a nightly or weekly schedule. For example, in your config file:

    [batch_result_repository]
    nightjob:${TEXTTEST_HOME}/ci_results
    ci:${TEXTTEST_HOME}/ci_results
    [end]
    
    [historical_report_location]
    nightjob:${TEXTTEST_HOME}/ci_reports
    ci:${TEXTTEST_HOME}/ci_reports
    [end]

    [batch_filter_file]
    ci:${TEXTTEST_HOME}/tests/selections/commit_tests.txt
    [end]

In this example 'nightjob' runs everything but 'ci' runs only tests that match the selection criteria in the file `${TEXTTEST_HOME}/tests/selections/commit_tests.txt`

That file could contain something like this:

    -ts commit_tests

That would select a test suite named 'commit_tests'.

## Full documentation
There is more information about [running TextTest unattended](http://texttest.sourceforge.net/index.php?page=documentation_4_0&n=running_texttest_unattended).

