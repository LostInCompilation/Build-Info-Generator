# Build Info Generator


## Contents

- [Description](#description)
- [Features](#features)
- [Download](#download)
- [How to use it](#how-to-use-it)
  - [Command line interface](#command-line-interface)
    - [Usage](#usage)
    - [Example](#example)
  - [Integrating in Visual Studio](#integrating-in-visual-studio)
- [Generated example file](#generated-example-file)

*See also: [License (zlib)](LICENSE.md)*


## Description

A simple command line tool with a permissive license (zlib) to auto generate a header file containing an incrementing build number and the current build time and date.
It can be easily integrated into almost any IDE, which supports custom build events (a command/program that gets called from the IDE before/during compilation).
The generated header file can simply be added and included in any of your projects. It will be automatically updated every time you build your project.
It exists because I don't like to bloat VisualStudio with lots of plugins which will eat resources when I don't need them.
So a small program **which only gets called** when the build process in the IDE actually starts is much more convinient.

In the future constexpr globals will be supported besides macros.

See [instructions](#how-to-use-it) below for usage and how to include the tool in your Visual Studio project.


## Features

- Simple command line tool to integrate in your IDE's build process
- Build number counter
- Optional time and date of build
- Full Unicode support for paths / filenames
- Generated file is UTF-8 encoded, optionally with BOM (See [Command line interface: /bom](#command-line-interface))
- Can be paused with BUILD_INFO_GENERATOR_PAUSE macro ([show example file](#generated-example-file))
- No need to build it yourself, compiled executable for Windows (x64) can be found [here](x64/Release/BuildInfoGenerator.exe)


## Download

You can download a prebuilt executable [here (x64, Windows)](x64/Release/BuildInfoGenerator.exe).

Needs the Visual Studio 2019 C++ runtime (vc_redist.x64.exe). Get it [from Microsoft](https://support.microsoft.com/en-us/topic/the-latest-supported-visual-c-downloads-2647da03-1eea-4433-9aff-95f26a218cc0).
If you have Visual Studio 2015 or newer installed, you don't need to install the Visual Studio C++ runtime.


## How to use it


### Command line interface


#### Usage

~~~
Usage:
    BuildInfoGenerator [/h | /help] | ([/time] [/bom] [/reset] /out "file")

Options:
    /h, /help        Display this help message.
    /time            Write build time and date to generated file.
    /reset           Reset the generated file and set the build number
                     back to zero.
    /bom             Write UTF-8 BOM to output file.
    /out "file"      Specify the output file (relative or absolute).
~~~


#### Example

To update or generate the file "C:\MyProject\BuildInfo.h" with an incrementing build number
and the build time and date, see command below.<br>
If the file already exists, it's build number will be increased by one and time and date will be updated. Otherwise a new file with build number 0 and current time will be generated.

~~~
BuildInfoGenerator.exe /time /out "C:\MyProject\BuildInfo.h"
~~~

The output file will be UTF-8 encoded, no matter if it contains a BOM or not. To write an UTF-8 BOM
to the beginning of the output file (recommended), add the "/bom" argument [(see command line interface usage above)](#usage)


### Integrating in Visual Studio

Simply add a Pre-Build-Command (you can use the above example command) to your project:

> Right click on your project -> Properties -> Build Events -> Pre-Build Events -> Paste the command into "Command line".

Do not forget to put the executable path and output file path into quotation marks if your path contains whitespaces:
~~~
"C:\A path\with\white spaces\BuildInfoGenerator.exe" /out "..\source code\BuildInfo.h"
~~~


## Generated example file

~~~cpp
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
#define BUILD_INFO_GENERATOR_BUILD_NUMBER 42

#define BUILD_INFO_GENERATOR_DAY 17
#define BUILD_INFO_GENERATOR_MONTH 08
#define BUILD_INFO_GENERATOR_YEAR 2021
#define BUILD_INFO_GENERATOR_DATE_STR "17.08.2021"

#define BUILD_INFO_GENERATOR_HOUR 06
#define BUILD_INFO_GENERATOR_MINUTE 47
#define BUILD_INFO_GENERATOR_SECOND 26

#define BUILD_INFO_GENERATOR_TIME_STR "06:47:26"

/********************** End of generated file **********************/
~~~
