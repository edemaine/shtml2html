# shtml2html

Quick partial implementation of
[Apache's server-parsed HTML](https://httpd.apache.org/docs/current/mod/mod_include.html)
as a **static** converter to regular HTML.
You thus need to manually run the converter whenever the input/data changes.

## Installation

```sh
npm install -g @edemaine/shtml2html
```

## Usage

```sh
shtml2html filename.shtml    # produces filename.html
shtml2html *.shtml           # produces *.html
```

## Supported Features

* `<!--#include file="path"-->` includes a non-relative path
* `<!--#include virtual="path"-->` includes a relative path
  * Note: absolute paths are currently relative to the filesystem root.
    TODO: way to specify document root.
* `<!--#config key="value"-->` where `key` is among:
  * `echomsg`: message for unsupported `#echo`
  * `errormsg` (not currently used)
  * `sizefmt` (not currently used)
  * `timefmt`: strftime format for `LAST_MODIFIED`
* `<!--#echo var="value"-->` where `value` is among:
  * `DOCUMENT_NAME`: name of `.html` output (not `.shtml` input)
  * `LAST_MODIFIED`: modified date of `.shtml` input (via `timefmt`)
