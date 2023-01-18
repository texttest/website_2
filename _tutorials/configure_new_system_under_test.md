---
layout: tutorial
title: Configuring TextTest with a new System Under Test
---

# Configuring TextTest with a new System Under Test

TextTest can be configured to test anything that is an executable program. Usually you want to store the tests in the same repository as the sourcecode, in a separate folder. The layout should look something like this:

<pre>
my_project/
├─ bin/
│  ├─ my_app.exe
├─ src/
│  ├─ my_app.c
├─ test/
│  ├─ config.myapp
│  ├─ requirements.txt
│  ├─ start_texttest.bat
│  ├─ start_texttest.sh
│  ├─ testsuite.myapp
├─ README.md
</pre>

There is a [starter project for C](https://github.com/texttest/StarterProject.C) which demonstrates this structure. You should be able to adapt it for your programming language. 

The 'start_texttest' command line scripts are generic and will work for any project. The purpose is to create a self-contained 'venv' python environment to run texttest in for this project. 

