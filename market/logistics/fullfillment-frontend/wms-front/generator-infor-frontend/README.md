# generator-infor-frontend [![NPM version][npm-image]][npm-url] [![Build Status][travis-image]][travis-url] [![Dependency Status][daviddm-image]][daviddm-url]
> Creates a basic code for Kotlin/Spring backend from JSON

## Installation

First, install [Yeoman](http://yeoman.io) and generator-infor-frontend using [npm](https://www.npmjs.com/) (we assume you have pre-installed [node.js](https://nodejs.org/)).

```bash
npm install -g yo
npm install -g generator-infor
```

Then generate your new project:

```bash
yo infor
```

## Usage

Generator has 3 modes to create code in Kotlin, Java or both.

JSON parameters:

| Parameter | Description |
|-----------|-------------|
| ```title``` | Name of the project (defines the naming of entities) |
| ```tablename``` | Name of the DB table |
| ```fields``` | Fields of the result DTO. Has the following properties:<ul><li>```name``` - field's name</li><li>```type``` - field's type. Can be any string, but only Int, Double, Float, Long and String are handled automatically</li><li>```import``` - class import for custom type</li><li>```isPrimary``` - boolean value indicating if the field is a primary key</li></ul> |


[npm-image]: https://badge.fury.io/js/generator-infor-frontend.svg
[npm-url]: https://npmjs.org/package/generator-infor-frontend
[travis-image]: https://travis-ci.com/yandex/generator-infor-frontend.svg?branch=master
[travis-url]: https://travis-ci.com/yandex/generator-infor-frontend
[daviddm-image]: https://david-dm.org/yandex/generator-infor-frontend.svg?theme=shields.io
[daviddm-url]: https://david-dm.org/yandex/generator-infor-frontend
