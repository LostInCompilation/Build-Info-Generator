# Build Info Generator

## Description

**Note: This file will be updated in the next days.**

A simple tool to auto generate a header file containing the current build number and the current build date and time.
The generated header file can simply be added and included in any of your projects. It will be automatically updated every time you build your project.

See [instructions](#Instructions) below for usage.

## Features
- Build number counter
- Optional time and date of build
- Full Unicode support for paths / filenames
- c
  - cc
  - cd
- e


## Instructions

Instr.

## Sample file

~~~{.cpp}
/********************************************************************/
/*                                                                  */
/*                 Generated by Build Info Generator                */
/*                                                                  */
/*  All modifications to this file                                  */
/*  will be replaced on next run.                                   */
/********************************************************************/

#pragma once

// To disable updates to this file, set "BUILD_INFO_GENERATOR_PAUSE" to "1".
#define BUILD_INFO_GENERATOR_PAUSE 0

// Generated info
#define BUILD_INFO_GENERATOR_BUILD_NUMBER 0

#define BUILD_INFO_GENERATOR_DAY 15
#define BUILD_INFO_GENERATOR_MONTH 08
#define BUILD_INFO_GENERATOR_YEAR 2021

#define BUILD_INFO_GENERATOR_HOUR 06
#define BUILD_INFO_GENERATOR_MINUTE 10
#define BUILD_INFO_GENERATOR_SECOND 06

/********************** End of generated file **********************/
~~~
