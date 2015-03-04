# KLogger: Simple Logging for PHP

Originally written by [Kenny Katzgrau](http://twitter.com/katzgrau), [Dan Horrigan](http://twitter.com/dhrrgn)
and updated by [Iulian Mironica] (http://twitter.com/iulianmironica)

## About

This class is an improved version of KLogger which I use in my projects and I maintain.
(KLogger is an easy-to-use 
[PSR-3](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-3-logger-interface.md)
compliant logging class for PHP).
It was meant to be a class that you could quickly include into a 
project and have working right away.

Improvements: 
- Stabilisation
- Added format functionality
- Placed all in one class
- Performance improvement

## Installation

### Composer

From the Command Line:

```
composer require iulianmironica/klogger:dev-master
```

In your `composer.json`:

``` json
{
    "require": {
        "iulianmironica/klogger": "dev-master"
    }
}
```

## Basic Usage

``` php
<?php

require 'vendor/autoload.php';

$users = [
    [
        'name' => 'Kenny Katzgrau',
        'username' => 'katzgrau',
    ],
    [
        'name' => 'Dan Horrigan',
        'username' => 'dhrrgn',
    ],
];

// New feature
$loggerSettings = [
    'level' => \IulianMironica\KLogger\Logger::DEBUG, // emergency, alert, critical, error, warning, notice, info, debug
    'timestamp' => 'm-d-Y G:i:s', // leave blank for none
    'format' => '%timestamp% %level% %class% %function% %message%', // output format - leave blank for none
    'directory' => /path/to/log/dir, // path to the log directory
    /* %timestamp%      - the timestamp declared above
     * %level%          - level declared above
     * %class%          - class name
     * %function%       - method/function name
     * %message%        - the message passed as param
     * %line%, %file%   - point to the parent file that triggered method/function
     */
];

$logger = new \IulianMironica\KLogger\Logger($loggerSettings);
$logger->info('Returned a million search results');
$logger->error('Oh dear.');
$logger->debug('Got these users from the Database.', $users);

// New feature - you can now debug your data without needing to pass a string as first param
$logger->debug($users);
```

### Output

```
02-19-2015 14:34:08 DEBUG Model\User getAll Got these users from the Database.
    0: array(
        'name' => 'Kenny Katzgrau',
        'username' => 'katzgrau',
    )
    1: array(
        'name' => 'Dan Horrigan',
        'username' => 'dhrrgn',
    )
02-19-2015 14:34:08 DEBUG Model\User getAll
    0: array(
        'name' => 'Kenny Katzgrau',
        'username' => 'katzgrau',
    )
    1: array(
        'name' => 'Dan Horrigan',
        'username' => 'dhrrgn',
    )
```

## Setting the Log Level Threshold

You can use the `\IulianMironica\KLogger\Logger` constants to set Log Level Threshold, so that
any messages below that level, will not be logged.

### Default Level

The default level is `DEBUG`, which means everything will be logged.

### Available Levels

``` php
<?php
use IulianMironica\KLogger\Logger;

// These are in order of highest priority to lowest.
\Logger::EMERGENCY;
\Logger::ALERT;
\Logger::CRITICAL;
\Logger::WARNING;
\Logger::NOTICE;
\Logger::INFO;
\Logger::DEBUG;
```

### Example

``` php
<?php

$loggerSettings = [
    'level' => \IulianMironica\KLogger\Logger::ERROR, // emergency, alert, critical, error, warning, notice, info, debug
    'timestamp' => 'm-d-Y G:i:s', // leave blank for none
    'format' => '%timestamp% %level% %class% %function% %message%', // output format - leave blank for none
    'directory' => /path/to/log/dir, // path to the log directory
    /* %timestamp%      - the timestamp declared above
     * %level%          - level declared above
     * %class%          - class name
     * %function%       - method/function name
     * %message%        - the message passed as param
     * %line%, %file%   - point to the parent file that triggered method/function
     */
];

$logger = new \IulianMironica\KLogger\Logger($loggerSettings);
$logger->error('Uh Oh!'); // Will be logged
$logger->info('Something Happened Here'); // Will be NOT logged
```

## Why use KLogger?

Why not? Just drop it in and go. If it saves you time and does what you need,
go for it! Take a line from the book of our C-code fathers: "`build` upon the
work of others".

## Who uses KLogger?

Klogger has been used in projects at:

    * The University of Iowa
    * The University of Laverne
    * The New Jersey Institute of Technology
    * Middlesex Hospital in NJ

Additionally, it's been used in numerous projects, both commercial and personal.

## Special Thanks

Special thanks to all contributors:

* [Dan Horrigan](http://twitter.com/dhrrgn)
* [Tim Kinnane](http://twitter.com/etherealtim)
* [Brian Fenton](http://github.com/fentie)
* [Cameron Will](https://github.com/cwill747)

## License

The MIT License

Copyright (c) 2008-2014 Kenny Katzgrau <katzgrau@gmail.com>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
