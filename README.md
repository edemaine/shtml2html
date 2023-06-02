# shtml2html

Quick partial implementation of
[Apache's server-parsed HTML](https://httpd.apache.org/docs/current/mod/mod_include.html)
as a **static** converter to regular HTML.
You thus need to manually run the converter whenever the input/data changes.

## Installation

```sh
npm install
npm install -g coffeescript
```

(currently assumes `/usr/bin/coffee` exists)

## Usage

```sh
shtml2html filename.shtml
  # produces filename.html
```

## Supported Features

* `<!--#include virtual="path"-->` includes a relative path
* `<!--#config key="value"-->` where `key` is among:
  * `echomsg`: message for unsupported `#echo`
  * `errormsg` (not currently used)
  * `sizefmt` (not currently used)
  * `timefmt`: strftime format for `LAST_MODIFIED`
* `<!--#echo var="value"-->` where `value` is among:
  * `DOCUMENT_NAME`: name of `.html` output (not `.shtml` input)
  * `LAST_MODIFIED`: modified date of `.shtml` input (via `timefmt`)
