---
title: Test Harness Instructions
folder: developer_pages
permalink: test_harness_instructions.html
---

## Test Harness Instructions

The test harness is suite of utilities that combine to automatically configure, compile, and test Tramonto and then gather and report the results so that they can be viewed online.

### Running the Test Harness Locally

#### CTest (Tramonto 5.0 and later)

Set the following options in your cmake configuration:

    -DTramonto_TEST_HARNESS_DEFAULT_PROCESSES=8 \  
    -DBUILD_TESTING=ON \

Setting the default number of processes is optional. After compiling, to run the test harness, type:

    ctest -L LABEL -j NUM_PROCS
    

Where LABEL is one of Sanity, Checkin, Continuous, Nightly, or Occasional, and NUM_PROCS is the number of processes to use (note that if the default or hard-coded number of process for a test is greater than NUM_PROCS, the test will still be run, but no other tests will be run concurrently). The suites of tests that can be run (LABELs) are defined as follows:

*   **Sanity**: Fast running tests (generally less than 2s) that a user should run after compiling Tramonto. Sanity tests should not use hard-coded process counts greater than 2\. This set of tests is currently the most robust in terms of run time consistentcy and processor count changes.
*   **Checkin**: Fast running tests (generally less than 20s) that represent the minimum set of tests a developer should run prior to checkin in code changes. Checkin tests should not use hard-coded process counts greater than 4\. This suite of tests also includes all tests run as part of the Sanity suite.
*   **Continuous**: Short and medium length tests (geneally less than 2 minutes) that is run by the automated continuous integration testing and can be run by developers prior to committing significant code changes. Continuous tests should not use hard-coded process counts greater than 8\. This suite of tests also includes all tests run as part of the Checkin suite.
*   **Nightly**: Short, medium, and long running tests (generally less than 1 hour) that are run for nightly testing, and can be run by developers prior to committing significant code changes. This suite of tests also includes all testsrun as part of the Continuous suite.
*   **Occasional**: NOT CURRENTLY USED. This suite of tests includes very long running tests (generally longer than 1 hour), and does NOT include the tests run as part of other defined suites.

#### Deprecated (Tramonto 4.0 and earlier)

1.  To run the test harness locally, first you will need Tramonto itself, either by way of the CVS repository or a released tarball.
2.  Descend into TRAMONTO_ROOT/test/harness/invoke-configures/. In this directory, you'll need to place an invoke-configure script that is appropriate for your machine and environment.
3.  Ascend back up to TRAMONTO_ROOT/test/harness/. Here you'll need to edit the file 'config' and add a section for your "run" of the test harness. See the existing runs in config for examples. The form of a run section is generally as follows:  

    RUN (the-name-of-your-run) {      
        BUILD-LABEL = your-build-label;
        BUILD-DIR = the-name-to-use-for-the-build-directory;
        INVOKE-CONFIGURE = your-invoke-configure;
        TEST-CATEGORY = FRAMEWORK;
        MAX-PROC = 16;
        MPI-START = lamboot;
        MPI-PING = mpitask;
        MPI-STOP = lamhalt;
        TTR-DIR = /path/to/TramontoTestResults;
        SSG-USERNAME = yourusername;   
    }

The build label is simply a label for identifying this build or type of build on the website. 
The build directory will be created in TRAMONTO_ROOT if it doesn't already exist and will be blown away and recreated if it does. 
The invoke configure is the name of the invoke configure you created in the previous step. 
Currently, FRAMEWORK is the only test category implemented. 
The max-proc value actually sets the number of processors to use when invoking Tramonto. 
If your machine uses an MPI system that requires booting, provide the appropriate information in the MPI-* values. 
If you will be reporting the results to software.sandia.gov, you need to have a local copy of the TramontoTestResults repository checked out.
Do this using the command 'cvs checkout -l TramontoTestResults'--note the -l which just checks out and empty repository without checking out all previously-reported test harness results data. 
Give the path to this repository in TTR-DIR. If reporting to software.sandia.gov, you will also need to provide your username on that machine. 
For the reporting to work, you may also need to set up key-based SSH authentication or be prepared to enter your password a number of times. 
You can also optionally provide a custom make command with MAKE-COMMAND and a custom mpi invocation command with MPI-GO.

4.  After saving your changes to 'config', simply invoke 'runharness' from /TRAMONTO_ROOT/test/harness, passing it the name of your run (the part between the parentheses in the previous step), and the path to TRAMONTO_ROOT. For example: "./runharness --tramonto-dir=/home/user/Tramonto --build-name=the-name-of-your-run" There are a few other options you can pass to runharness. View these by running "./runharness --help". If you do not want the results reported to software.sandia.gov, pass --no-report. If you do not want Tramonto to be update via cvs before being tested, pass --no-update.
5.  When the test harness has finished running, descend into TRAMONTO_ROOT/test/harness/results/. Here you will find a number of text files containing information about and output from the various stages of configuring, building, and testing.

You can also run individual components of the test harness separately. You will find these utilities under TRAMONTO_ROOT/test/utilities/ and can find more information about them by invoking them with the --help option.

***

<a href="http://www.sandia.gov/general/privacy-security/index.html">Privacy and Security</a>  


