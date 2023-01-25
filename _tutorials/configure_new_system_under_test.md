---
layout: tutorial
title: Configuring TextTest for a new System Under Test
---

# Configuring TextTest for a new System Under Test

TextTest can be configured to test anything that is an executable program. Usually you want to store the tests in the same repository as the sourcecode, in a separate folder. The layout should look something like this:

<pre>
my_project/
├─ bin/
│  ├─ my_app.exe
├─ src/
│  ├─ my_app.c
├─ test/
│  ├─ config.myapp
│  ├─ start_texttest.bat
│  ├─ start_texttest.sh
│  ├─ testsuite.myapp
├─ README.md
</pre>

There is a [starter project for C](https://github.com/texttest/StarterProject.C) which demonstrates this structure. A similar structure would work for any program where you are testing a binary executable. 

The 'start_texttest' command line scripts are designed to run texttest with the correct settings for this project. When you want to run or manage your tests, use this script to start TextTest.

Once you've got this configured, you will be able to write tests. See [hello world tutorial]({{ site.baseurl }}{% link _tutorials/hello_world.md %}), you will be able to begin at the "Starting the TextTest Static GUI" section.