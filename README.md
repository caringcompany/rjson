# RJSON

[![Build Status](https://travis-ci.org/mantyr/rjson.svg?branch=master&v=2)][build_status]
[![GoDoc](https://godoc.org/github.com/mantyr/rjson?status.png)][godoc]
[![Go Report Card](https://goreportcard.com/badge/github.com/mantyr/rjson?v=4)][goreport]
[![Software License](https://img.shields.io/badge/license-BSD-brightgreen.svg)](LICENSE)

Package rjson implements a backwardly compatible version of JSON with the aim of making it easier for humans to read and write.

The data model is exactly that of JSON's and this package implements all the marshalling and unmarshalling operations supported by the standard library's json package.

The three principal differences are:

    - Quotes may be omitted for some object key values (see below).
    - Commas are automatically inserted when a newline is encountered after a value (but not an object key).
    - Commas are optional at the end of an array or object.

The quotes around an object key may be omitted if the key matches the following regular expression:

    [a-zA-Z][a-zA-Z0-9\-_]*

This rule will be relaxed in the future to allow unicode characters, probably following the same rules as Go's identifiers, and probably a few more non-alphabetical characters.


## Installation

    $ go get github.com/mantyr/rjson

## Example

    package main

    import (
        "fmt"
        "github.com/mantyr/rjson"
    )

    func main() {
        data := []byte(`{
            middle : {
                src: "pictures/product/123.jpg",
                place : "#preview-img",
                title: "title"
            }
        }`)

        var v struct {
            Middle struct {
                Src string
                Place string
                Title string
            }
        }
        err := rjson.Unmarshal(data, &v)
        fmt.Println(v)   // print {{pictures/product/123.jpg #preview-img title}}
        fmt.Println(err) // print <nil>
    }
## Author

Roger Peppe <roger.peppe@canonical.com>


[build_status]: https://travis-ci.org/mantyr/rjson
[godoc]:        http://godoc.org/github.com/mantyr/rjson
[goreport]:     https://goreportcard.com/report/github.com/mantyr/rjson
