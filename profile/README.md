![img](/profile/flow_php_banner_02_2022.png)

Flow is a PHP based, strongly typed ETL (Extract Transform Load), asynchronous data processing library with constant memory consumption. 

## Usage

**Extract** from the Source, **Transform**, **Load** to the Sink. 

## Usage

```php
<?php

declare(strict_types=1);

use Flow\ETL\DSL\Parquet;
use Flow\ETL\Filesystem\SaveMode;
use function Flow\ETL\DSL\{lit, ref, sum};
use Flow\ETL\DSL\To;
use Flow\ETL\Flow;

require __DIR__ . '/vendor/autoload.php';

(new Flow())
    ->read(Parquet::from(__FLOW_DATA__ . '/orders_flow.parquet'))
    ->select('created_at', 'total_price', 'discount')
    ->withEntry('created_at', ref('created_at')->toDate(\DateTime::RFC3339)->dateFormat('Y/m'))
    ->withEntry('revenue', ref('total_price')->minus(ref('discount')))
    ->select('created_at', 'revenue')
    ->groupBy('created_at')
    ->aggregate(sum(ref('revenue')))
    ->sortBy(ref('created_at')->desc())
    ->withEntry('daily_revenue', ref('revenue_sum')->round(lit(2))->numberFormat(lit(2)))
    ->drop('revenue_sum')
    ->write(To::output(truncate: false))
    ->mode(SaveMode::Overwrite)
    ->withEntry('created_at', ref('created_at')->toDate('Y/m'))
    ->write(Parquet::to(__FLOW_OUTPUT__ . '/daily_revenue.parquet'))
    ->run();
```

```console
$ php daily_revenue.php
+------------+---------------+
| created_at | daily_revenue |
+------------+---------------+
|    2023/10 |    206,669.74 |
|    2023/09 |    227,647.47 |
|    2023/08 |    237,027.31 |
|    2023/07 |    240,111.05 |
|    2023/06 |    225,536.35 |
|    2023/05 |    234,624.74 |
|    2023/04 |    231,472.05 |
|    2023/03 |    231,697.36 |
|    2023/02 |    211,048.97 |
|    2023/01 |    225,539.81 |
+------------+---------------+
10 rows
```

The reasons behind creating this project can be explained in few [tweets](https://twitter.com/norbert_tech/status/1484863793280786439?s=21). 
To get familiar with basic ETL Api, please look into [flow-php/etl repository](https://github.com/flow-php/etl), everything else is listed below. 

### [Usage Examples](https://github.com/flow-php/flow/tree/1.x/examples)

## Features

* constant memory consumption
* caching
* reading from any data source
* writing to any data source
* rich collection of data transformation functions
* grouping & aggregating
* remote files processing 
* joins
* sorting 
* displaying datasets as ASCII table
* validation against schema

## Building blocks

* DataFrame - Lazy data processing frame. 
* Rows - Immutable colllection of `Row` objects. 
* Row - Immutable, strongly typed collection of `Entry` objects. 
* Entry - Immutable, strongly typed object representing cell in a row. 
* **E**xtractor (Reader) - Memory safe, Data Source returning \Generator, yielding `Rows` to the `Pipeline`
* **T**ransformer - Data transformer receiving and returning `Rows` (in most cases transformer), one instance of `Rows` at once.  
* **L**oader (Writer) - Memory safe representation of Data Sink, responsibility of Loader is to write `Rows` into destination storage, one at time. 
* Pipeline - Interface representing ETL process, each received `Rows` instanced is pased through all `Pipes`, also responsible for error handling. 
* Pipe - Loader of Transformer instance existing in `Pipes` collection.
* Function - transformation that might happen on a single row, single entry, rows or group of rows

### Supported PHP versions

* 8.1 - ✅
* 8.2 - ✅

## Available Data Types

* [array](https://github.com/flow-php/flow/tree/1.x/src/core/etl/src/Flow/ETL/Row/Entry/ArrayEntry.phpp)
* [boolean](https://github.com/flow-php/flow/tree/1.x/src/core/etl/src/Flow/ETL/Row/Entry/BooleanEntry.php)
* [datetime](https://github.com/flow-php/flow/tree/1.x/src/core/etl/src/Flow/ETL/Row/Entry/DateTimeEntry.php)
* [enum](https://github.com/flow-php/flow/tree/1.x/src/core/etl/src/Flow/ETL/Row/Entry/EnumEntry.php)
* [float](https://github.com/flow-php/flow/tree/1.x/src/core/etl/src/Flow/ETL/Row/Entry/FloatEntry.php)
* [integer](https://github.com/flow-php/flow/tree/1.x/src/core/etl/src/Flow/ETL/Row/Entry/IntegerEntry.php)
* [json](https://github.com/flow-php/flow/tree/1.x/src/core/etl/src/Flow/ETL/Row/Entry/JsonEntry.php)
* [list](https://github.com/flow-php/flow/tree/1.x/src/core/etl/src/Flow/ETL/Row/Entry/ListEntry.php)
* [map](https://github.com/flow-php/flow/tree/1.x/src/core/etl/src/Flow/ETL/Row/Entry/MapEntry.php)
* [null](https://github.com/flow-php/flow/tree/1.x/src/core/etl/src/Flow/ETL/Row/Entry/NullEntry.php)
* [object](https://github.com/flow-php/flow/tree/1.x/src/core/etl/src/Flow/ETL/Row/Entry/ObjectEntry.php)
* [string](https://github.com/flow-php/flow/tree/1.x/src/core/etl/src/Flow/ETL/Row/Entry/StringEntry.php)
* [structure](https://github.com/flow-php/flow/tree/1.x/src/core/etl/src/Flow/ETL/Row/Entry/StructureEntry.php)
* [uuid](https://github.com/flow-php/flow/tree/1.x/src/core/etl/src/Flow/ETL/Row/Entry/UuidEntry.php)
* [xml](https://github.com/flow-php/flow/tree/1.x/src/core/etl/src/Flow/ETL/Row/EntryXmlEntry.php)
* [xml_node](https://github.com/flow-php/flow/tree/1.x/src/core/etl/src/Flow/ETL/Row/Entry/XmlNodeEntry.php)

## Available Adapter

- [ETL](src/core/etl/README.md)
- Adapters
    - [avro](https://github.com/flow-php/flow/tree/1.x/src/adapter/etl-adapter-avro/README.md)
    - [chartjs](https://github.com/flow-php/flow/tree/1.x/src/adapter/etl-adapter-chartjs/README.md)
    - [csv](https://github.com/flow-php/flow/tree/1.x/src/adapter/etl-adapter-csv/README.md)
    - [doctrine](https://github.com/flow-php/flow/tree/1.x/src/adapter/etl-adapter-doctrine/README.md)
    - [elasticsearch](https://github.com/flow-php/flow/tree/1.x/src/adapter/etl-adapter-elasticsearch/README.md)
    - [filesystem](https://github.com/flow-php/flow/tree/1.x/src/adapter/etl-adapter-filesystem/README.md)
    - [google sheet](https://github.com/flow-php/flow/tree/1.x/src/adapter/etl-adapter-google-sheet/README.md)
    - [http](https://github.com/flow-php/flow/tree/1.x/src/adapter/etl-adapter-http/README.md)
    - [json](https://github.com/flow-php/flow/tree/1.x/src/adapter/etl-adapter-json/README.md)
    - [logger](https://github.com/flow-php/flow/tree/1.x/src/adapter/etl-adapter-logger/README.md)
    - [meilisearch](https://github.com/flow-php/flow/tree/1.x/src/adapter/etl-adapter-meilisearch/README.md)
    - [parquet](https://github.com/flow-php/flow/tree/1.x/src/adapter/etl-adapter-parquet/README.md)
    - [text](https://github.com/flow-php/flow/tree/1.x/src/adapter/etl-adapter-text/README.md)
    - [xml](https://github.com/flow-php/flow/tree/1.x/src/adapter/etl-adapter-xml/README.md)
- Libraries
    - [array-dot](https://github.com/flow-php/flow/tree/1.x/src/lib/array-dot/README.md)
    - [doctrine-dbal-bulk](https://github.com/flow-php/flow/tree/1.x/src/lib/doctrine-dbal-bulk/README.md)
    - [dremel](https://github.com/flow-php/flow/tree/1.x/src/lib/dremel/README.md)
    - [parquet](https://github.com/flow-php/flow/tree/1.x/src/lib/parquet/README.md)
    - [parquet-viewer](https://github.com/flow-php/flow/tree/1.x/src/lib/parquet-viewer/README.md)
    - [snappy](https://github.com/flow-php/flow/tree/1.x/src/lib/snappy/README.md)

## Transformation Functions

Flow ETL provides a rich set of official functions to transform data, please find them all in [flow-php/etl](https://github.com/flow-php/flow/tree/1.x/src/core/etl/src/Flow/ETL/Function) 
repository.

## Sponsors 

Flow PHP is sponsored by: 

- [Blackfire](https://blackfire.io/) - the best PHP profiling and monitoring tool! 
