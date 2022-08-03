---
layout: tutorial
title: Developing TextTest
---

# Developing TextTest

Perhaps you are missing a feature in TextTest or want to fix a bug in it. Before embarking on TextTest development you might want to raise an issue on github, and/or send a message about it to the [texttest mailing list](https://sourceforge.net/projects/texttest/lists/texttest-users). If you decide you still want to develop TextTest, you will need to check out the code, make your change, test it, then send a pull request to the project maintainers. 

This tutorial explains how to set up a working development environment for TextTest.

## Clone the code and the self tests

For convenience, create a folder where you can keep all the texttest repositories. Set the environment variable $TEXTTEST_HOME to point at it in your shell.

    $ mkdir texttest_dev
    $ cd texttest_dev
    $ export TEXTTEST_HOME=$PWD

In that folder, clone the [texttest sourcecode](https://github.com/texttest/texttest) and the [self tests](https://github.com/texttest/selftest). They are two different repositories:

    $ git clone https://github.com/texttest/texttest
    $ git clone https://github.com/texttest/selftest

## Build and install texttest from source

You may find it convenient to set up a [virtual environment](https://docs.python.org/3/library/venv.html) and use that python to install texttest, so you can easily switch between your locally built texttest and the released version. The following command assumes you have set up a virtualenv and use it when you run `python`.

    $ cd texttest
    $ python setup.py install

This should create a texttest executable under the 'bin' directory of your python installation. This should be on  your $PATH so that this command will run texttest

    $ texttest --help

You can now run and test your locally built texttest.

## run the self tests

Running the tests on the command line, sequentially:

    $ cd $TEXTTEST_HOME/selftest
    $ texttest -con -c ../texttest -l

* The '-con' flag tells it to run texttest on the command line instead of launching the GUI. You may not need this. 
* The '-c' flag to indicate the checkout we want to test. In this case we point it at the sourcecode we are testing. 
* The '-l' flag tells it to run the tests sequentially, which is simpler and less likely to go wrong. You might not need it.

If any tests fail, you will need to [configure your diff tool](/how_to_guides/configure_editor.html) to view failure information.

## Updating the documentation

Texttest currently has two websites. This one, [texttest.org], and the older one on [texttest.sourceforge.net]. Clone the [texttest.org sourcecode](https://github.com/texttest/website_2) and the [texttest.sourceforge.net sourcecode](https://github.com/texttest/website).

Each of those repositories has some instructions in their README file to help you.

## Submitting your change to the project maintainers

Send a pull request in the usual way. Pull requests are more likely to be accepted if they are small, well documented, and the self tests pass.
