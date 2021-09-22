---
layout: how_to_guide
title: Run tests sequentially or in parallel
---

# Run tests sequentially instead of in parallel

By default TextTest runs your tests in parallel. Sometimes that's not what you want. 


## Solution 1: select "run sequentially" in the GUI
In the static GUI there is a checkbox under the "running" tab where you can select "run tests sequentially". This will apply to all test runs triggered while this checkbox is enabled.

## Solution 2: global configuration
If you want it to always run sequentially, add this line to your config file:

	config_module:default

Why this works is a little obscure to me. The documentation for this config entry is [here](http://texttest.sourceforge.net/index.php?page=documentation_4_0&n=writing_a_config_module#config_module).