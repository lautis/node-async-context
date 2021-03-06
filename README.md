[![Build Status](https://api.travis-ci.org/gms1/node-async-context.svg?branch=master)](https://travis-ci.org/gms1/node-async-context)
[![npm version](https://badge.fury.io/js/asyncctx.svg)](https://badge.fury.io/js/asyncctx)
[![Dependency Status](https://david-dm.org/gms1/node-async-context.svg)](https://david-dm.org/gms1/node-async-context)
[![devDependency Status](https://david-dm.org/gms1/node-async-context/dev-status.svg)](https://david-dm.org/gms1/node-async-context#info=devDependencies)
[![Known Vulnerabilities](https://snyk.io/test/github/gms1/node-async-context/badge.svg)](https://snyk.io/test/github/gms1/node-async-context)
[![Greenkeeper badge](https://badges.greenkeeper.io/gms1/node-async-context.svg)](https://greenkeeper.io/)

# node-async-context (asyncctx)

This module allows you to create an asynchronous execution context for JavaScript or TypeScript

> NOTE: This module is based on [async_hooks](https://github.com/nodejs/node/blob/master/doc/api/async_hooks.md) an experimental built-in node.js module introduced in v8.0.0

> NOTE: Your contribution is highly welcome!

## Introduction

To give you an idea of how **asyncctx** is supposed to be used:
 

```TypeScript

import { ContinuationLocalStorage } from 'asyncctx';

class MyLocalStorage {
  value: number;
}

let cls = new ContinuationLocalStorage<MyLocalStorage>();
cls.setRootContext({ value: 1});

process.nextTick(() => {
  let curr1 = cls.getContext(); // value is 1
  cls.setContext({ value: 2});  // value should be 2 in the current execution context and below
  process.nextTick(() => {
    let curr2 = cls.getContext(); // value is 2
    cls.setContext({ value: 3});  // value should be 3 in the current execution context and below
    process.nextTick(() => {
      let curr3 = cls.getContext(); // value is 3
    });
  });
  process.nextTick(() => {
    let curr4 = cls.getContext(); // value is 2
  });
});

```

## License

**node-async-context (asyncctx)** is licensed under the MIT License:
[LICENSE](./LICENSE)

## Release Notes

| Release   | Notes                                                                                                                            |
|-----------|----------------------------------------------------------------------------------------------------------------------------------|
| 1.0.02    | maintenance release                                                                                                              |
| 1.0.01    | added support for older nodejs versions (4,6,7) using internal copy of async-hook@1.7.1                                          |
| 1.0.00    | is now based on 'async_hooks' (a built-in nodejs v8.0 module)                                                                    |
| 0.0.06    | maintenance releases                                                                                                             |
| 0.0.05    | async-hook 1.7.1                                                                                                                 |
| 0.0.01-04 | initial version                                                                                                                  |

## Downloads

[![NPM](https://nodei.co/npm/asyncctx.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/asyncctx)
