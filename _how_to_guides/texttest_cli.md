---
layout: how_to_guide
title: Running tests on the Command Line
---

# Running tests on the Command Line

Sometimes you don't have access to the TextTest development tools, and all you want to do is run your tests and get a report of whether they passed or not. You can run a suite of tests using TextTest's command line interface. If any tests fail, it will also let you interactively approve or reject the new results.

### Linux
Open a command prompt in the same folder as the test suite, then start texttest's command-line interface:

    texttest -con

### Windows
First set the environment variable `TEXTTEST_HOME` to the location of your test suite, then start texttest on the command line:

    texttest -con

## Expected output
For a hello world application you might expect this kind of output:

    $ texttest -con
    Using Application Hello World
    Running Hello World test-suite tests
    Running Hello World test-case smoke
    Comparing differences for Hello World test-suite tests
    Comparing differences for Hello World test-case smoke - SUCCESS! (on stderr.hello,stdout.hello)

## Other command-line options

If you want to run the tests unattended, for example in a CI server, see [running tests unattended](batch_mode.html). Find out more about texttest's available options in the  [command-line options reference](http://texttest.sourceforge.net/index.php?page=documentation_4_0&n=options_default).