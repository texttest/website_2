---
layout: how_to_guide
title: Configure Default Editor and Diff tool
---

# Configure Default Editor and Diff tool

When you double-click on a file in the TextTest GUI it opens it for you in an editor. The default is emacs, which might not suit everyone. This article explains how to configure which editor and diff tool TextTest opens.

Update the settings in your personal config file. By default it's at this location:

	~/.texttest/config

If that file doesn't exist, create it. Once it's created, you can also find it in the TextTest GUI on the 'Config' tab, listed under 'Personal Files'. Note: you will probably need to restart texttest before it will detect your new config file


The most common entries that people want to set are the editor and diff tool. For example, to set them to `sublime_text` and `meld`:

	[view_program]
	default:sublime_text

	[diff_program]
	default:meld

You can write any program there instead of gedit or meld that is on your $PATH. The 'view_program' is what will open when you double click on most files in the TextTest GUI. The 'diff_program' is used to show you test failure diffs.


This personal config file is not meant to be checked into version control, it's just for you. TextTest also has a config file for each application that is tested. This file is stored together with the test cases it configures, and should be checked in. You can put configuration preferences for editors in that file as well, but it's not recommended. These preferences are usually personal, and not shared by everyone who develops the same test suite.



