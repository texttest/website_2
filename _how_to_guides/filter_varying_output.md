---
layout: how_to_guide
title: Filter Varying Output with Scrubbers
---

# Filter Varying Output with Scrubbers

Often when you're Approval testing a program it will produce some output that varies every time you run the test. You don't want the test to fail every time when a process ID or a date changes. In TextTest we call this 'filtering run dependent text' or 'scrubbing' the output.

For example if this is your approved standard output file:

	2021-09-10 06:13:09,622 Initializing AcmeDB ...
	2021-09-10 06:13:09,873 Setting up x y and z
	2021-09-10 06:13:10,123 Running self checks
	2021-09-10 06:13:10,224 AcmeDB Started! process_id=4474
	2021-09-10 06:13:10,224 Ready to accept connections

Since the timestamps and process ID are different every time you run the program, by default your test case will fail every time it runs. The rest of the article explains three different ways to handle this problem.

## Solution 1 - filter the timestamps and process ids

In your config file for the tested application, add an entry like this:

	[scrubbers]
	stdout:^\d{4}-\d{2}-\d{2} \d{2}:\d{2}:\d{2},\d{3}{REPLACE timestamp}
	stdout:(process_id)=\d+{REPLACE \1=1234}


This leads to filtered output like this:

	timestamp Initializing AcmeDB ...
	timestamp Setting up x y and z
	timestamp Running self checks
	timestamp AcmeDB Started! process_id=1234
	timestamp Ready to accept connections


The key 'stdout' here means that the run-dependent (varying) text will be found in standard output. You could also write 'stderr' here for standard error, or another filename key.

The idea is to write a regular expression that matches the part of the line you want to remove or replace. You can use an online regex tool to help you to design a good one - for example [pythex](https://pythex.org/), [pyrexpPython ](https://pythonium.net/regex) or [regex101.com](https://regex101.com/). TextTest uses the [Python regular expression syntax](https://docs.python.org/3/library/re.html#regular-expression-syntax).

Just after the regex, you can optionally add some curly brackets and give TextTest further instructions about what to do when it matches this pattern. In the first example above it will replace everything that matched the regex with the fixed string 'timestamp'. In the second example it uses a capture group in the regex to capture the non-varying part and make the filtered output more readable as well as stable. 

## Solution 2 - filter several lines of irrelevant output

You might prefer to just ignore all the output lines between "Initializing AcmeDB" and "Ready to accept connections". In that case you could do run-dependent text like this:

	[scrubbers]
	stdout:^\d{4}-\d{2}-\d{2} \d{2}:\d{2}:\d{2},\d{3}{REPLACE timestamp}
	stdout:Initializing AcmeDB{->}Ready to accept connections


Which would reduce the output to this:

	timestamp Initializing AcmeDB ...
	timestamp Ready to accept connections

The directive `x{->}y` tells TextTest to filter all the lines in between the ones that match x and y.

For full documentation about all the available TextTest options, see [the reference documentation](http://texttest.sourceforge.net/index.php?page=documentation_4_0&n=run_dependent_text#run_dependent_text).

## Solution 3 - Use something more targeted and readable for testing

In general you might not want to use your ordinary logs as a basis for testing. Often they contain a lot of irrelevant details that will make your test unstable and fail for no good reason. It might be better to write a custom logger or Printer that only prints out the important things that happen. Since you design that from scratch just for Approval testing, you have full control and can choose to not output any process ids or timestamps in that log.




