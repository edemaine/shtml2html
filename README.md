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

## Supported Directives

* `<!--#include file="path"-->` includes a non-relative path
* `<!--#include virtual="path"-->` includes a relative path
  * Note: absolute paths are currently relative to the filesystem root.
    TODO: way to specify document root.
* `<!--#include virtual="path1" virtual="path2"-->` for multiple inclusions
* `<!--#flastmod file="path"-->`:
  modified date of non-relative path (via `timefmt`)
* `<!--#flastmod virtual="path"-->`:
  modified date of relative path (via `timefmt`)
* `<!--#fsize file="path"-->`: size of non-relative path (via `sizefmt`)
* `<!--#fsize virtual="path"-->`: size of relative path (via `sizefmt`)
* `<!--#config key="value"-->` where `key` is among:
  * `echomsg`: message for unsupported `#echo`
  * `errormsg`: error to include in the file when a directive fails
    (a more descriptive error message should also be printed to console)
  * `sizefmt`: format for `#fsize`, either "bytes" (default) or "abbrev"
  * `timefmt`: strftime format for `LAST_MODIFIED`
* `<!--#echo var="value"-->` where `value` is among:
  * `DOCUMENT_NAME`: name of `.html` output (not `.shtml` input)
  * `LAST_MODIFIED`: modified date of `.shtml` input (via `timefmt`)
* `<!--#comment ...-->` gets removed
