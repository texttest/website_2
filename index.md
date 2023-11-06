---
layout: homepage
title: TextTest
---

Full Texttest documentation is currently on this url: [http://texttest.sourceforge.net/](http://texttest.sourceforge.net/)

This site is intended to eventually replace that site with up-to-date relevant documentation and information about the [TextTest](https://github.com/texttest) framework. At some point it may be complete enough to replace the documentation currently hosted on sourceforge, but at the moment it's very much a work in progress.

# Getting Started with TextTest

TextTest and related tools are designed to both execute existing test cases and to help you to develop new test cases. If you only want to be able to execute existing test cases and report failures to a file, the command line tools are enough. On a development machine where you will be actively maintaining and creating test cases, you will need the full install including development tools.

## Command-line tools

The command-line tools enable you to run existing test cases and report test results. On Windows, we recommend you follow the [Windows installation instructions](getting_started/install_windows.html) instead, but you can still install TextTest as a Python package as described below if you prefer.

You will need a recent version of [Python](https://www.python.org/): 3.6 or higher. We also recommend [creating a virtual environment](https://docs.python.org/3/library/venv.html) to run TextTest in. When you have activated your virtual environment, use pip to install TextTest:

    python -m pip install texttest

You should now be able to [run tests on the command line](/how_to_guides/texttest_cli.html) and [run tests unattended](/how_to_guides/batch_mode.html). If you want to be able to create and maintain test cases, you will also need to install the development tools, as explained in the next section.

## Installing TextTest Development Tools

These tools include a graphical user interface for creating, updating and viewing test cases as well as examining and updating test results. Use the guide for your platform:

- [Windows](getting_started/install_windows.html)
- [Linux](getting_started/install_linux.html)
- [MacOS](getting_started/install_macos.html)

Once you have installed both the TextTest command-line tools and the development tools, you will be able to create, run and update test cases using a convenient graphical user interface.

## Next steps

- Follow the [Hello World](/tutorials/hello_world.html) tutorial

This documentation is organized according to the [Divio documentation system](https://documentation.divio.com/). There are four main sections: 

- [Tutorials](/tutorials): step-by-step instructions to get you started
- [How-To Guides](/how_to_guides): specific solutions to specific problems
- [Reference](/reference): Comprehensive lists of all that's possible
- [Articles](/articles): Opinions and perspectives on this style of testing
