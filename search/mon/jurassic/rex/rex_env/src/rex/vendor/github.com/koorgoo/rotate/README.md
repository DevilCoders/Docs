# rotate [![GoDoc][doc-img]][doc] [![Build Status][ci-img]][ci]

Rotation for `*os.File`.

## Installation

```
go get -u github.com/koorgoo/rotate
```

## Quick Start

```
f := rotate.MustOpen(name, rotate.Config{
  Bytes: rotate.MB,
  Count: 10,
})
defer f.Close()
```

See [examples][examples].

[doc-img]: https://godoc.org/github.com/koorgoo/rotate?status.svg
[doc]: https://godoc.org/github.com/koorgoo/rotate
[ci-img]: https://travis-ci.org/koorgoo/rotate.svg?branch=master
[ci]: https://travis-ci.org/koorgoo/rotate
[examples]: https://github.com/koorgoo/rotate/tree/master/example
