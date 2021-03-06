## mobile-json-wire-protocol

[![NPM version](http://img.shields.io/npm/v/mobile-json-wire-protocol.svg)](https://npmjs.org/package/mobile-json-wire-protocol)
[![Downloads](http://img.shields.io/npm/dm/mobile-json-wire-protocol.svg)](https://npmjs.org/package/mobile-json-wire-protocol)
[![Dependency Status](https://david-dm.org/appium/node-mobile-json-wire-protocol/master.svg)](https://david-dm.org/appium/node-mobile-json-wire-protocol/master)
[![devDependency Status](https://david-dm.org/appium/node-mobile-json-wire-protocol/master/dev-status.svg)](https://david-dm.org/appium/appium-adb/2.0#info=devDependencies)

[![Build Status](https://travis-ci.org/appium/node-mobile-json-wire-protocol.svg?branch=master)](https://travis-ci.org/appium/node-mobile-json-wire-protocol)
[![Coverage Status](https://coveralls.io/repos/appium/node-mobile-json-wire-protocol/badge.svg?branch=master)](https://coveralls.io/r/appium/node-mobile-json-wire-protocol?branch=master)


An abstraction of the Mobile JSON Wire Protocol ([spec](https://github.com/SeleniumHQ/mobile-spec/blob/master/spec-draft.md)) with Appium extensions (as specified [here](http://www.w3.org/TR/webdriver/#protocol-extensions)).


### Endpoints in the protocol

The Mobile JSON Wire Protocol package gives access to a number of endpoints documented [here](docs/protocol-methods.md).


### MobileJsonWireProtocol

The basic class, subclassed by drivers that will use the protocol.


### routeConfiguringFunction (driver)

This function gives drivers access to the protocol routes. It returns a function that itself will take an [Express](http://expressjs.com/) application.


### isSessionCommand (command)

Checks if the `command` needs to have a session associated with it.


### ALL_COMMANDS

An array of all the commands that will be dispatched to by the Mobile JSON Wire Proxy endpoints.


### NO_SESSION_ID_COMMANDS

An array of commands that do not need a session associated with them.


### Errors

This package exports a number of classes and methods related to Selenium error handling. There are error classes for each Selenium error type (see [here](https://code.google.com/p/selenium/wiki/JsonWireProtocol#Response_Status_Codes), as well as the context errors in the [mobile spec](https://github.com/SeleniumHQ/mobile-spec/blob/master/spec-draft.md#webviews-and-other-contexts)). The list of errors, and their meanings, can be found [here](docs/errors.md).

There are, in addition, two helper methods for dealing with errors

`isErrorType (err, type)`

- checks if the `err` object is a Mobile JSON Wire Protocol error of a particular type
- arguments
  - `err` - the error object to test
  - `type` - the error class to test against
- usage
  ```js
  import { errors, isErrorType } from 'mobile-json-wire-protocol';

  try {
    // do some stuff...
  } catch (err) {
    if (isErrorType(err, errors.InvalidCookieDomainError)) {
      // process...
    }
  }
  ```

`errorFromCode (code, message)`

- retrieve the appropriate error for an error code, with the supplied message.
- arguments
  - `code` - the integer error code for a Mobile JSON Wire Protocol error
  - `message` - the message to be encapsulated in the error
- usage
  ```js
  import { errors, errorFromCode } from 'mobile-json-wire-protocol';

  let error = errorFromCode(6, 'an error has occurred');

  console.log(error instanceof errors.NoSuchDriverError);
  // => true

  console.log(error.message === 'an error has occurred');
  // => true
  ```
