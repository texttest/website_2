---
layout: tutorial
title: Locating the tests and the system under test
---

# Organizing your test files

The file `config.app` (where `app` is the short name of your system under test) is central. The location of this file should be set as the `TEXTTEST_ROOT` environment variable, or specified with the `-d` flag when you start texttest:

    texttest -d /path/to/config/file/directory

For example, if your config file is called `config.hello` and is located in a folder `/users/emily/workspace/hello`:

    texttest -d /users/emily/workspace/hello

Sometimes you store the test suite in a different location to the system under test (typically for systems where the sourcecode is spread over several git repositories, and you have a separate repo for end-to-end tests). In that case you will need to also specify the path to the system under test using `TEXTTEST_CHECKOUT` or the `-c` command line flag when you start texttest:

    texttest -d /path/to/config/file/directory -c /path/to/system/under/test/directory

For example, if your config file is called `config.hello` and is located in a folder `/users/emily/workspace/hello`, and your system under test is located in : 
