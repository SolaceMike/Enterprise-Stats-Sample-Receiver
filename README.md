Solace Enterprise Stats Receiver Framework REAMDE
====================

This README contains instructions on how to install, configure, and use the
Solace stats-receiver client framework to receive stats published by 
StatsPump and store them in a time-series database. 

Things you'll need:

* [Java JDK 1.7 or above](http://www.oracle.com/technetwork/java/javase/overview/index.html)

## Overview

The receiver framework, consists of a simple Solace client to receive and 
parse stat messages published by StatsPump, and and interface for a 
user-defined plugin to store the parsed metrics in a time-series database. 
The receiver framework uses a plugin based design to allow received metrics 
to be stored in any database, such as InfluxDB time-series database.

A sample built-in plugin is provided, for testing purposes, to output the 
received stat messages on the console.

> NOTE: In the current version of the receiver framework, only message types 
published by StatsPump using the SDTFactory class are parsed. Any other message
type, such as message containing JSON payloads, are ignored and discarded.

## Installation

Simply extract the Enterprise-Stats-Sample-Receiver-master.zip package:

    unzip Enterprise-Stats-Sample-Receiver-master.zip

## Building the sample

The build uses Gradle. Simple execute the assemble target by executing the 
following command:

   gradlew assemble

## Usage

To run the Solace stats-receiver execute from the root folder of the built package:

    cd build/build
    ./bin/stats-receiver --config config/sampleReceiver.properties

OR for Windows based platforms:

    cd build\build
    .\bin\stats-receiver.bat --config config/sampleReceiver.properties
    
> NOTE: when starting up the stats-receiver, it will wait for up to 2 minutes 
to receive the BROADCAST messages from the StatsPump to know what the topic 
formats look like, and what are the indexable attributes. Upon receiving this
broadcast message the receiver will start delivering messages to the configured
plugin.

## Logging support

The stats-receiver uses Apache SLF4J logging framework as a simple facade or
abstraction for various logging frameworks. By default the Apache Log4J2 
framework is used as the implementation to output logs to a file or on the
console. All logs by default are generated in the logs/ directory in a file
called: stats-receiver.log

The configuration for Log4J is provided in the config/ directory. Edit the
log4j2.properties file to make any changes to the logging levels or output
file name & location.

## License

Copyright 2016-2017 Solace Corporation. All rights reserved.

http://www.solace.com

This source is distributed under the terms and conditions of any contract or
contracts between Solace Corporation ("Solace") and you or your company. If
there are no contracts in place use of this source is not authorized. No
support is provided and no distribution, sharing with others or re-use of 
this source is authorized unless specifically stated in the contracts 
referred to above.

This software is custom built to specifications provided by you, and is 
provided under a paid service engagement or statement of work signed between
you and Solace. This product is provided as is and is not supported by 
Solace unless such support is provided for under an agreement signed between
you and Solace.
