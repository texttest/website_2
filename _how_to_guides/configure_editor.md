---
layout: how_to_guide
title: Configure Default Editor and Diff tool
---

# Configure Default Editor and Diff tool

When you double-click on a file in the TextTest GUI it opens it for you in an editor. The default is emacs, which might not suit everyone. This article explains how to configure which editor and diff tool TextTest opens.

TextTest has a config file for each application that is tested. This file is stored together with the test cases it configures. You can put configuration preferences for editors in that file as well, but it's not recommended. These preferences are usually personal, not shared by everyone who develops the same test suite. What you want to edit is your personal config file. By default it's at this location:

	~/.texttest/config

If that file doesn't exist, create it. Once it's created, you can also find it in the TextTest gui on the 'config' tab, listed under 'Personal config files'.

The most common entries that people want to set are the editor and diff tool. For example, to set them to gedit and meld:

	[view_program]
	default:gedit

	[diff_program]
	default:meld

You can write any program there instead of gedit or meld that is on your $PATH. The 'view_program' is what will open when you double click on most files in the TextTest GUI. The 'diff_program' is used to show you test failure diffs.



