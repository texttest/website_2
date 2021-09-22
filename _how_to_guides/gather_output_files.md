---
layout: how_to_guide
title: Use additional files as part of approved baseline
---

# Use additional files as part of approved baseline

By default TextTest will capture the output from your program that is written to standard output and standard error. You may want to additionally collect other files produced by your program.

## Solution 1: collate local files
Normally you'd like any files created by your program to be written to the [TextTest Sandbox](http://texttest.sourceforge.net/index.php?page=documentation_4_0&n=texttest_sandbox). That means the program should just write them to the current working directory. In that case, you can ask TextTest to pick them up and include them in the baseline with this config file entry:

	[collate_file]
	mylog:dump.log
	another_file:results.txt

This will have TextTest collect a file "dump.log" and "results.txt" in the working directory of your program. For more details, see the [collate_file documentation](http://texttest.sourceforge.net/index.php?page=documentation_4_0&n=extra_files#collate_file).