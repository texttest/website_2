---
layout: reference
title: Scrubbing or Filtering output
---

# Scrubbing or Filtering output
If your program produces output that changes every test run, you will want to remove it before comparing output against the approved version, otherwise your test will fail all the time. Typically this means removing process ids, timestamps or temporary directory names.

There is already a [How-to guide]({{ site.baseurl }}{% link _how_to_guides/filter_varying_output.md  %}) which explains how to handle timestamps and process ids. This reference lists all alternatives.

## Quick start guide
At the end of your config file add a section like this:

    [scrubbers]
    stdout:^\d{4}-\d{2}-\d{2} \d{2}:\d{2}:\d{2},\d{3}{REPLACE timestamp}
    stdout:(process_id)=\d+{REPLACE \1=1234}
    stderr:{INTERNAL writedir}

TextTest uses the [Python regular expression syntax](https://docs.python.org/3/library/re.html#regular-expression-syntax). Replace 'stdout' and 'stderr' with the file alias for the relevant file you want to filter.

## Remove the temporary 'sandbox' directory
TextTest runs your program in a temporary directory called the 'sandbox'. This changes every time and it's annoying to write a RegEx to filter it. TextTest provides a mechanism to revove it like this:

    {INTERNAL writedir}

For example to scrub this directory when shown in standard error:

    [scrubbers]
    stderr:{INTERNAL writedir}

## Scrubbing when you encounter a pattern
If you have a RegEx matching a particular part of your output, you can control how much text is then scrubbed.

### Replace the matching text with some fixed text
Replace the matching text with a fixed text

    <pattern>{REPLACE <text>}

For example replacing a process id i stdout:

    [scrubbers]
    stdout:(process_id)=\d+{REPLACE \1=<process id>}

A line like this:

    AcmeDB Started! process_id=1234

Would be scrubbed to look like this:

    AcmeDB Started! process_id=<process id>

### Remove one or more lines
On encountering a match with <pattern>, the default is to remove the single line containing the pattern. You can also specify it to remove <number_of_lines> using {LINES n}. The count includes the line matched, so {LINES 1} has no effect.

    [scrubbers]
    stdout:Database Started with attributes{LINES 3}

Output like this:

    Some log statement
    Database Started with attributes:
    foo=123
    bar=678
    Some other log statement

Would be scrubbed to look like this:

    Some log statement
    Some other log statement

### Remove a section between two patterns
You can also specify two patterns marking the beginning and end of a section of lines that should all be removed.
    
    <pattern1>{->}<pattern2>

The directive between curly brackets can be configured as to whether to include the matching lines or not. 

* {->} - scrub all lines between the ones that match the patterns
* {[->]} - as above but additionally scrub the lines that match the patterns
* {[->}  - as the first case, but additionally scrub the first line
* {->]} - as the first case, but additionally scrub the last line

For example:

    [scrubbers]
    stdout:Database Started with attributes{->]}bar=\d+

Output like this:

    Some log statement
    Database Started with attributes:
    foo=123
    bar=678
    Some other log statement

Would be scrubbed to look like this:

    Some log statement
    Database Started with attributes:
    Some other log statement

## Remove a particular line
If it's always a particular line number use this:

    {LINE <line_number>}

For example to scrub the first line in standard output:

    [scrubbers]
    stdout:{LINE 0}

# Run dependent text
Note there is an alias in wide use: 'run_dependent_text' is an alias for 'scrubbers' in the config file.