[![npm](https://img.shields.io/npm/v/entity-baker.svg)](https://www.npmjs.com/package/entity-baker)
[![npm](https://img.shields.io/npm/dt/entity-baker.svg?label=npm%20downloads)](https://www.npmjs.com/package/entity-baker)

# node-entity-baker

[Node.js](https://nodejs.org) application / library, which generates simple and powerful entity classes for [ORM](https://en.wikipedia.org/wiki/Object-relational_mapping) systems, like [Doctrine](http://www.doctrine-project.org) and/or [Entity Framework](https://docs.microsoft.com/en-us/ef/), wriiten in [TypeScript](https://www.typescriptlang.org).

## Installation

As command line tool:

```bash
npm install -g entity-baker
```

As module:

```bash
npm install --save entity-baker
```

## Usage

First create a `entities.json` file inside your working directory (can also be in XML or YAML format, s. [examples folder](https://github.com/mkloubert/node-entity-baker/tree/master/examples)):

```json
{
    "namespace": "MarcelJoachimKloubert.Database",

    "entities": {
        "Log": {
            "table": "logs",

            "columns": {
                "id": {
                    "id": true,
                    "auto": true,
                    "type": "int32"
                },
                
                "level": {
                    "null": true,
                    "type": "int16"
                },
                
                "message": "string",
                "tag": {
                    "null": true,
                    "type": "string"
                },
                
                "context": {
                    "null": true,
                    "type": "json"
                }
            }
        }
    }
}
```

### From command line

```bash
# run it from your working directory
entity-baker --doctrine --entity-framework --entity-framework-core
```

### As module

JavaScript

```javascript
var EntityBaker = require('entity-baker');
```

TypeScript

```typescript
import * as EntityBaker from 'entity-baker';
```

#### compile

```javascript
var fs = require('fs');

var entityFile = JSON.parse(
    fs.readFileSync('./entities.json', 'utf8')
);

EntityBaker.compile({
    cwd: '/path/to/working/directory',
    file: entityFile,
    outDir: '/path/to/output/directory',
       target: 1,  // Doctrine
    // target: 2  // Entity Framework
    // target: 3  // Entity Framework Core

    callbacks: {
        onBeforeGenerateClass: function(className, target) {
        },

        onClassGenerated: function(err, className, target) {
        }
    }
}).then(function() {
    // files generated
}, function (err) {
    // error while generating files
});
```

## Data types

Type | [Doctrine]() | [Entity Framework]()
------------ | ------------- | -------------
`bigint` | [bigint](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#bigint) | [System.Int64](https://msdn.microsoft.com/en-us/library/system.int64(v=vs.110).aspx) |
`bin` | [binary](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#binary) | [System.Byte\[\]](https://msdn.microsoft.com/en-us/library/system.byte(v=vs.110).aspx) |
`binary` | [binary](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#binary) | [System.Byte\[\]](https://msdn.microsoft.com/en-us/library/system.byte(v=vs.110).aspx) |
`blob` | [blob](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#blob) | [System.Byte\[\]](https://msdn.microsoft.com/en-us/library/system.byte(v=vs.110).aspx) |
`bool` | [boolean](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#boolean) | [System.Boolean](https://msdn.microsoft.com/en-us/library/system.boolean(v=vs.110).aspx) |
`boolean` | [boolean](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#boolean) | [System.Boolean](https://msdn.microsoft.com/en-us/library/system.boolean(v=vs.110).aspx) |
`date` | [date](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#date) | [System.Int64](https://msdn.microsoft.com/en-us/library/system.datetime(v=vs.110).aspx) |
`datetime` | [datetime](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#datetime) | [System.Int64](https://msdn.microsoft.com/en-us/library/system.datetime(v=vs.110).aspx) |
`datetimetz` | [datetimetz](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#datetimetz) | [System.DateTimeOffset](https://msdn.microsoft.com/en-us/library/system.datetimeoffset(v=vs.110).aspx) |
`decimal` | [decimal](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#decimal) | [System.Decimal](https://msdn.microsoft.com/en-us/library/system.decimal(v=vs.110).aspx) |
`float` | [float](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#float) | [System.Single](https://msdn.microsoft.com/en-us/library/system.single(v=vs.110).aspx) |
`guid` | [guid](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#guid) | [System.Guid](https://msdn.microsoft.com/en-us/library/system.guid(v=vs.110).aspx) |
`int` | [integer](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#integer) | [System.Int32](https://msdn.microsoft.com/en-us/library/system.int32(v=vs.110).aspx) |
`int16` | [smallint](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#smallint) | [System.Int16](https://msdn.microsoft.com/en-us/library/system.int16(v=vs.110).aspx) |
`int32` | [integer](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#integer) | [System.Int32](https://msdn.microsoft.com/en-us/library/system.int32(v=vs.110).aspx) |
`int64` | [bigint](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#bigint) | [System.Int64](https://msdn.microsoft.com/en-us/library/system.int64(v=vs.110).aspx) |
`integer` | [integer](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#integer) | [System.Int32](https://msdn.microsoft.com/en-us/library/system.int32(v=vs.110).aspx) |
`json` | [json](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#json) | [dynamic](https://msdn.microsoft.com/en-us/library/system.object(v=vs.110).aspx) |
`smallint` | [smallint](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#smallint) | [System.Int16](https://msdn.microsoft.com/en-us/library/system.int16(v=vs.110).aspx) |
`str` | [string](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#string) | [System.String](https://msdn.microsoft.com/en-us/library/system.string(v=vs.110).aspx) |
`string` | [string](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#string) | [System.String](https://msdn.microsoft.com/en-us/library/system.string(v=vs.110).aspx) |
`text` | [text](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#text) | [System.String](https://msdn.microsoft.com/en-us/library/system.string(v=vs.110).aspx) |
`time` | [time](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#time) | [System.TimeSpan](https://msdn.microsoft.com/en-us/library/system.timespan(v=vs.110).aspx) |
`uint16` | [smallint](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#smallint) | [System.UInt16](https://msdn.microsoft.com/en-us/library/system.uint16(v=vs.110).aspx) |
`uint32` | [integer](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#integer) | [System.UInt32](https://msdn.microsoft.com/en-us/library/system.uint32(v=vs.110).aspx) |
`uint64` | [bigint](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#bigint) | [System.UInt64](https://msdn.microsoft.com/en-us/library/system.uint64(v=vs.110).aspx) |
`uuid` | [guid](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#guid) | [System.Guid](https://msdn.microsoft.com/en-us/library/system.guid(v=vs.110).aspx) |

If you do not define a data type, it set to

* `int32`, if the column is a primary key, or...
* `string`, if nothing else matches

## Support and contribute [[&uarr;](#table-of-contents)]

If you like the module, you can support the project by sending a [donation via PayPal](https://paypal.me/MarcelKloubert) to [me](https://github.com/mkloubert).

To contribute, you can [open an issue](https://github.com/mkloubert/node-entity-baker/issues) and/or fork this repository.

To work with the code:

* clone [this repository](https://github.com/mkloubert/node-entity-baker)
* create and change to a new branch, like `git checkout -b my_new_feature`
* run `npm install` from your project folder
* edit and debug in your favorite editor, like [Visual Studio Code](https://code.visualstudio.com)
* commit your changes to your new branch and sync it with your forked GitHub repo
* make a [pull request](https://github.com/mkloubert/node-entity-baker/pulls)

The API documentation can be found [here](https://mkloubert.github.io/node-entity-baker/).
