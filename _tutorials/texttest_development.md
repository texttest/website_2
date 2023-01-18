---
layout: tutorial
title: Developing TextTest
---

# Developing TextTest

This tutorial explains how to set up a working development environment for TextTest.

Perhaps you are missing a feature in TextTest or want to fix a bug in it. Before embarking on TextTest development you will want to discuss your plans with the project maintainers. Raise an issue on github, and/or send a message about it to the [texttest mailing list](https://sourceforge.net/projects/texttest/lists/texttest-users). When you've done that you will need to check out the code, make your change, test it, then send a pull request to the project maintainers. 

## Clone the code and the self tests

For convenience, create a folder where you can keep all the texttest repositories. Set the environment variable $TEXTTEST_HOME to point at it in your shell.

Linux/OSX:

    $ mkdir texttest_dev
    $ cd texttest_dev
    $ export TEXTTEST_HOME=$PWD
    $ echo $TEXTTEST_HOME

Windows powershell:

    $ mkdir texttest_dev
    $ cd texttest_dev
    $ $env:TEXTTEST_HOME = $PWD
    $ echo $env:TEXTTEST_HOME

This last command should print out the value of the environment variable TEXTTEST_HOME so you can check it is set correctly, it should contain the full path of the texttest_dev folder.

In the TEXTTEST_HOME folder, clone the [texttest sourcecode](https://github.com/texttest/texttest) and the [self tests](https://github.com/texttest/selftest). They are two different repositories:

    $ git clone https://github.com/texttest/texttest
    $ git clone https://github.com/texttest/selftest

## Build and install texttest from source

You may find it convenient to set up a [virtual environment](https://docs.python.org/3/library/venv.html) and use that python to install texttest, so you can easily switch between your locally built texttest and the released version. 

Linux/OSX:

    $ cd $TEXTTEST_HOME/texttest
    $ virtualenv venv
    $ venv/bin/activate
    $ which python

Windows powershell:

    $ cd $env:TEXTTEST_HOME/texttest
    $ virtualenv venv
    $ .\venv\Scripts\activate.ps1
    $ (Get-Command python).Path

That last command will print the location of the python executable that your shell will use so you can check virtualenv is working. It should print a path under the `venv` folder. 

Then you can build and install texttest as a python package, where you can still edit and develop the source files:

    $ pip install -r requirements.txt
    $ pip install --editable texttest

This should create a texttest executable under the 'bin' directory of your venv python installation. This should be on your $PATH so that this command will work:

    $ texttest --help

You can now run and test your local copy of texttest.

## run the self tests

Start the texttest static GUI:

    $ cd $TEXTTEST_HOME/selftest
    $ texttest -c ../texttest

The '-c' flag indicates the checkout we want to test. In this case we point it at the sourcecode we are testing. Then you can use the static GUI to select which tests to run. You should be able to run everything under "TestSelf".

If any tests fail, you will need to [configure your diff tool](/how_to_guides/configure_editor.html) to view failure information.

## Updating the documentation

Texttest currently has two websites. This one, [texttest.org](http://texttest.org), and the older one on [texttest.sourceforge.net](http://texttest.sourceforge.net/). Clone the [texttest.org sourcecode](http://github.com/texttest/website_2) and the [texttest.sourceforge.net sourcecode](https://github.com/texttest/website).

Each of those repositories has some instructions in their README file to help you.

## Submitting your change to the project maintainers

Send a pull request in the usual way. Pull requests are more likely to be accepted if they are small, well documented, and the self tests pass.
