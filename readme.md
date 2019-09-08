# ms.js

A simple utility module which will help you implement time-based applications.

# Table of Contents

* [Behaviour](#Behaviour)
* [Input](#Input)
  * [Examples](#Examples)
  * [String input Units](#String input Units)
  * [Options](#Options)

## Behaviour

**The function will always return a `Time` Object.**

For example:
```js
const time = require('ms.js');
console.log(time(5200));
```
will return:
```js
{
    eternity: 0,
    aeon: 0,
    century: 0,
    decade: 0,
    year: 0,
    day: 0,
    hour: 0,
    minute: 0,
    second: 5,
    millisecond: 200,
    microsecond: 0,
    nanosecond: 0,
    
    ms: 5200,
    str: '5 seconds and 200 milliseconds'
}
```

Invoking the `toString` function will always return the `.str` value.
For example:
```js
const time = require('ms.js');
console.log(`Shutting down in ${time(5200)}`); // => 'Shutting down in 5 seconds and 200 milliseconds'
```

Invoking the `valueOf` function will always return the `.ms` value.
For example:
```js
const time = require('ms.js');
time(5200) + 300; // => 5500
```

## Input

Valid Input is always either a `Number` or a `String`!

### Examples
```js
const time = require('ms.js');

time(1000).str;                            // => '1 second'
time(1000 * 60).str;                       // => '1 minute'
time('2 hours').ms;                        // => 7200000
time('50y, 30h, 20m, 10s').str;            // => '5 decades, 1 day, 6 hours, 20 minutes and 10 seconds'
time('30 hours, 20 min10seconds5 0y').str; // => '5 decades, 1 day, 6 hours, 20 minutes and 10 seconds'
time(time('2 hours') + time(10000)).str;   // =>  '2 hours and 10 seconds'
time('-3 days').ms;                        // => -259200000
time('20').str;                            // => '20 minutes'
time(20).str;                              // => '20 milliseconds'
time(2.5).str;                             // => '2 milliseconds and 500 microseconds'
time('2.5 hours').str;                     // => '2 hours and 30 minutes'
time('minute').ms                          // => 60000
time(Infinity).str                         // => '1 eternity'
```
(assuming that all relevant values will be shown, see: "**Options**" section)

### String input Units

Unit Name | Definition
---|---
Eternity | An Infinite amount of time
Aeon | `3.1536e+19 ms` or 1 billion years
Millenium | `3.1536e+13 ms` or 1,000 years
Century | `3.1536e+12 ms` or 100 years
Generation | `1103760000000 ms` or 3 decades and 5 years
Decade | `3.1536e+11 ms` or 10 years
Megaminute | `60000000000 ms` or 1,000,000 minutes or about 1 year and 329 days
Year | `3.1536e+10 ms` or 365 days
Season | `7884086400 ms` or about 91 days and 6 hours
Month | `2628028800 ms` or about 30 days and 10 hours
Lunar Month | `2449440000 ms` or about 28 days and 8 hours
Fortnight | `1209600000 ms` or 14 days
Week | `604800000 ms` or 7 days
Day | `86400000 ms` or 24 hours
Hour | `3600000 ms` or 60 minutes
Moment | `90000 ms` or 1 minute and 30 seconds
Minute | `60000 ms` or 60 seconds
Instant | `8000 ms` or 8 seconds
Second | `1000 ms`
Millisecond | `1 ms`
Microsecond | `0.001 ms`
Nanosecond | `0.000001 ms` or 0.001 microseconds

### Options

Options are parsed in an Object as the 2nd parameter to the function.

Option Name | Purpose | Default
---|---|---
verbose | Whether or not to show the entire Unit name or to use a shortened name | `true`
relevant | How many relevant Units to display in the String | `2`
strict | Whether or not to limit the use of incomplete input for String input | `false`

**Examples:**
```js
const time = require('ms.js');

time(55555, {verbose: true}).str    // => '55 seconds and 555 milliseconds'
time(55555, {verbose: false}).str   // => '55s, 555ms'

time(55555555, {relevant: 2}).str   // => '15 hours and 25 minutes'
time(55555555, {relevant: 3}).str   // => '15 hours, 25 minutes and 55 seconds'
time(55555555, {relevant: 4}).str   // => '15 hours, 25 minutes, 55 seconds and 555 milliseconds'

time('minute', {strict: false}).str // => '1 minute'
time('1', {strict: false}).str      // => '1 minute'
time('minute', {strict: true}).str  //TypeError: Cannot read property 'str' of undefined
time('1', {strict: true}).str       //TypeError: Cannot read property 'str' of undefined


time('66666', {strict: false, verbose: false, relevant: 99}) // => 46d, 7h, 6m
```
