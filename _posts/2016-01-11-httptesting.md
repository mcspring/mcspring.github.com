---
layout: post
title: "httptesting"
tagline: HTTP testing framework for golang
description: ""
category: tutorial
tags: [go, golang, gogo, mock]
prettify: true
---
{% include JB/setup %}

## What's httptesting?

httptesting 是一个 golang HTTP 客户端测试框架，方便面向 API 的单元测试，尤其针对 JSON API 添加特殊支持。

[![Build Status](https://travis-ci.org/dolab/httptesting.svg?branch=master&style=flat)](https://travis-ci.org/dolab/httptesting)

## Installation

```bash
$ go get github.com/dolab/httptesting
```

## Getting Started

```go
package main

import (
    "net/http"
    "testing"

    "github.com/dolab/httptesting"
)

func Test_Client(t *testing.T) {
    host := "https://example.com"
    test := httptesting.New(host, true)

    test.Get("/")

    // verify http response status
    test.AssertOK()

    // verify http response body
    test.AssertNotEmpty()
}

func Test_ClientWithCustomRequest(t *testing.T) {
    r, _ := http.NewRequest("HEAD", "https://example.com", nil)
    r.Header.Add("X-Custom-Header", "custom-header")

    test := httptesting.New("", true)
    test.NewRequest(r)

    // verify http response status
    test.AssertOK()

    // verify http response body
    test.AssertEmpty()
}
```

### Advantage Usage

```go
package main

import (
	"testing"
)

func Test_RequestClient(t *testing.T) {
    host := "https://example.com"
    test := httptesting.New(host, true)

	request := test.New(t)
	request.WithHeader("X-Mock-Client", "httptesting")

    // assume server response with following json data:
    // {"user":{"name":"httptesting","age":3},"addresses":[{"name":"china"},{"name":"USA"}]}
	request.Get("/api/json", nil)

    // verify http response status
	request.AssertOK()

    // verify http response header
    request.AssertHeader("X-Mock-Client", "httptesting")

    // verify http response body with json format
	request.AssertContainsJSON("user.name", "httptesting")

    // for array
    request.AssertContainsJSON("addresses.1.name", "USA")
    request.AssertNotContainsJSON("addresses.2.name")

    // use regexp for custom matcher
    request.AssertMatch("user.*")
}
```
