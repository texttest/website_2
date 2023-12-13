---
layout: article
title: Testing a REST-API - Restful Booker Worked Example
---

# Testing a REST-API - Restful Booker Worked Example

by Emily Bache

_This article accompanies the video [Beyond Code Katas - Approval Testing a REST API](https://youtu.be/4ZYm-Vi2hI4)_.

Code katas are great for practicing your skills. By necessity though these are small problems, and your production code is on a completely different scale. In this article I want to show you a kind of code kata that’s a little bit larger. It’s a back-end service with a database, written in node.js. It has a REST API and is backed by a Mongo database. It's a little bit closer to a real world system than your average code kata. Let's look at a good way to get this code under control using TextTest and CaptureMock.

## The System under Test - Restful Booker
The code for [Restful Booker](https://github.com/texttest/restful-booker) is forked under the TextTest project on Github. It's a fork based on [Mark Winteringham's code](https://github.com/mwinteringham/restful-booker). Mark does workshops and trainings for testers, and he created this application to help teach good strategies for exploring and manual testing an API. Restful Booker is deliberately designed to be buggy, often in subtle ways. It's also designed with fairly comprehensive documentation so you can assess the value of that too.

I'm using this code slightly differently - my concern is how to write automated tests for this service that will be reliable, fast and comprehensive enough to support refactoring, and not too much work to create or maintain. I've used TextTest and CaptureMock in this role on a microservices production system I worked on previously, and I'm also drawing on the experiences of Geoff Bache testing several other service-based and microservices systems. So even though this is a toy example, I think it illustrates a viable approach.

## The work the video doesn't show
What's not shown in the video is all the preparation work we did to 'Sandbox' the Restful booker service, and to add the OpenAPI interface description to enable Swagger. The actual changes to application code were fairly minimal, but it was a reasonable amount of work to set up the test rig and other configuration files that TextTest uses. As I showed in the video though, once you've done that, it's relatively quick to create tests. This is typical - the 'Sandboxing' process for the large complex production systems Geoff and I have worked on has taken some weeks (even months) of expert attention. Once that is set up though, a much larger group of developers and testers (even less technical or manual testers) can create and maintain tests.

In this article I'd like to go into a little more detail about this sandboxing process for Restful booker so you can get a better idea of what it might involve for your similar production systems that have a REST API.

## Enabling Swagger
This may be something you've already added to your REST API. It's useful to have this as documentation, totally independently of how you're going to test the service. The basic principle is you create an Open API specification file for the API, either by hand or using a tool that can generate it from your sourcecode. For Restful Booker, Geoff set up Swagger with this [swagger.json](https://github.com/texttest/restful-booker/blob/main/swagger.json) configuration with help from [Swagger UI Express](https://www.npmjs.com/package/swagger-ui-express).

## Enabling CaptureMock to intercept Swagger calls
This is the only change to the actual application code, in [app.js](https://github.com/texttest/restful-booker/blob/main/app.js):

    let options = {};
    const capturemock = process.env.CAPTUREMOCK_SERVER;
    if (capturemock) {
        const requestInterceptorStr = "(req) => { req.url = req.url.replace(/http:..(127.0.0.1|localhost):[0-9]+/, '" + capturemock + "'); return req; }";
        options["swaggerOptions"] = {
            requestInterceptor: eval(requestInterceptorStr)
        };
    }
    app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerDocument, options));

The first and last lines would have been there anyway - they are enabling the swagger documentation to appear on the url `/api-docs`. The additional code checks for the environment variable `CAPTUREMOCK_SERVER` and does nothing if it is not set. The rest of this code is a little bit awkward to understand. It's setting an option to insert a `requestInterceptor` - a little piece of code that will be called whenever you use Swagger. This enables [CaptureMock](https://github.com/texttest/capturemock) to be a 'man in the middle' intercepting and processing all Swagger-generated traffic between the browser and the Restful Booker.

In the video demo you see the 'httpmock' files that detail this kind of traffic. [CaptureMock](https://github.com/texttest/capturemock) generates these files using this interception process.

## Configuring TextTest's Test Rig
Key to the sandboxing process is being able to start and run your entire application, including the database, from a command-line script. Normally you'd start Restful Booker using `npm start`, and TextTest could run that directly, but there is actually a bunch of other stuff that needs configuring too. Often it's convenient to write a Test Rig - an additional script that does some setup before doing the equivalent of 'npm start', and may do some extra processing of results at the end.

The Test Rig for Restful Booker is a Python script [test_rig.py](https://github.com/texttest/restful-booker/blob/main/integration_tests/test_rig.py). I show it briefly in the video. It makes use of the companion tools [DBText](https://github.com/texttest/dbtext) and [CaptureMock](https://github.com/texttest/capturemock). This is an overview of what it does: 

* Set up a fresh database populated with test data
* Start CaptureMock in either record or replay mode
* Start Restful Booker
* Execute the test if running in replay mode, otherwise use CaptureMock to record a new test
* Stop Restful Booker
* Gather database changes and write them to a file

This script is specifically written for the application being tested, and will be the same for all the tests in the test suite. Anything that should be different between test cases will be specified in text files. Any code that is generic or re-usable will be extracted into either TextTest itself or be part of DBText or CaptureMock.

## The config file - pulling everything together
The main configuration file I haven't discussed yet is [config.rb](https://github.com/texttest/restful-booker/blob/main/integration_tests/config.rb). The 'rb' extension might confuse you - it stands for 'Restful Booker', not Ruby! TextTest has a slightly unusual convention that it uses the file extension to designate which application is being configured for testing, not the type of the file.

This file is used by TextTest to find out everything it needs to know in order to run all your tests.

* 'executable' points out the test rig that it will run for each test case. 
* 'dbtext_database_path' points out the location of the text files to use to populate the database.
* 'import_config_file' tells it to import the configuration CaptureMock needs from [another config file](https://github.com/texttest/restful-booker/blob/main/integration_tests/capturemockrc.rb)
* 'run_dependent_text' is a collection of directives to scrub or filter specific aspects of the output before deciding whether the test has passed or not.

What else would you like to know? Please leave a comment on the video or the [TextTest-users mailing list](https://sourceforge.net/p/texttest/mailman/texttest-users/).





