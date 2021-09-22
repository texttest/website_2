---
layout: how_to_guide
title: Access test data
---

# Access test data

By default TextTest lets you give input to your program via command-line options, or via environment variables. Your program might also need additional files with data in.

For example, say you have a file "mydata.txt" that needs to be in the current working directory when you run your test program.

## Solution 1: copy_test_path
Since your program is running in a sandbox directory, you need some way to copy your data files there. Add this entry to your config file:

	copy_test_path:mydata.txt

This will copy a file called 'mydata.txt' into the sandbox when the test runs. It will look for this file first in the test case folder, then in the folder above, then all the way up to $TEXTTEST_ROOT (ie the location of your config file). This means that each test can have their own version of the test data, or alternatively all tests in the suite can use the same test data.

## Solution 2: link_test_path
Since your program is running in a sandbox directory, you need some way to access your data files. Add this entry to your config file:

	link_test_path:mydata.txt

This is very similar to copy_test_path, except on a unix system it will create a softlink to the data instead of copying it. This can be useful if the test data is large. Note: if your program modifies this data then you must use copy_test_path instead, or you risk your tests no longer being isolated from one another.

See [the documentation](http://texttest.sourceforge.net/index.php?page=documentation_4_0&n=texttest_sandbox#link_test_path) for more information.