---
layout: tutorial
title: Write a test for a 'hello world' script
---

# Write a test for a 'hello world' program

First follow the [Getting started with TextTest](/index.html#getting-started-with-texttest) guide to install the TextTest development tools for your platform.

## Creating a Hello World program
Let's create a "hello world" command-line script that we can write tests for. How you will do this will depend on which platform and programming language you are using. In this tutorial we'll assume you are using Python in a linux or mac terminal, or [git bash](https://gitforwindows.org/) on Windows.  

Save this text to a file named `hello.py`:

    #!/usr/bin/env python
    print("Hello, World!")

Make it executable on the command line:

    chmod a+x hello.py

When you've done that you should be able to execute the program and see the message:

    $ ./hello.py
    Hello, World!

Now we are ready to write a test for this program using TextTest.

## Testing Hello World with TextTest

Create a folder to store your test cases in, below `hello.py`, and put two files in it, `config.hello` and `testsuite.hello`

    $ mkdir tests
    $ cd tests
    $ touch config.hello
    $ touch testsuite.hello

Put this text into `config.hello`:

    executable:${TEXTTEST_HOME}/hello.py
    filename_convention_scheme:standard
    full_name:Hello World

For the moment, we can leave `testsuite.hello` empty. We will use the TextTest development tools to create a test case in a minute.

The config file is absolutely central to how TextTest works, and it's important to get the format right.  These three key - value pairs specify for TextTest what's going to be tested, but there are many more options for this file, which we will learn about later on. Note - it's important to use a colon `:` as separator for `key:value`, and that there should be no spaces on either side.

The entry `executable` should contain the full path to the program we want to test. Here we are using the environment variable `TEXTTEST_HOME` but it could be an absolute path on your machine.

The entry `filename_convention_scheme` defaults to `classic`, but the newer scheme `standard` is more consistent and easier to use. It has more sensible  filenames when testing a command line program like this one.

The entry `full_name` refers to the display name of the system under test. The filename suffix (in this case `.hello`) is what's actually used by TextTest to identify the system under test. This has to be short and not contain spaces. Here I've chosen 'hello' for the short name because that is the filename of this program. Additionally specifying a full name like this will make the test reports easier to read and understand.

Now we have a test suite and config file, we can start the TextTest development tool. 

### Linux
Using a command prompt in the same folder as `hello.py`, start texttest:

    $ texttest

### Windows
First set the environment variable `TEXTTEST_HOME` to the folder containing `hello.py`, then start TextTest from the windows menu.

Texttest should open a new window that looks like this:




