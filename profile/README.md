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
use function Flow\ETL\DSL\lit;
use function Flow\ETL\DSL\ref;
use Flow\ETL\DSL\To;
use Flow\ETL\Flow;
use Flow\ETL\GroupBy\Aggregation;

require __DIR__ . '/vendor/autoload.php';

(new Flow())
    ->read(Parquet::from(__DIR__ . '/orders_flow.parquet'))
    ->select('created_at', 'total_price', 'discount')
    ->withEntry('created_at', ref('created_at')->toDate(\DateTime::RFC3339)->dateFormat('Y/m'))
    ->withEntry('revenue', ref('total_price')->minus(ref('discount')))
    ->select('created_at', 'revenue')
    ->groupBy('created_at')
    ->aggregate(Aggregation::sum(ref('revenue')))
    ->sortBy(ref('created_at')->desc())
    ->withEntry('daily_revenue', ref('revenue_sum')->round(lit(2)))
    ->drop('revenue_sum')
    ->withEntry('created_at', ref('created_at')->toDate('Y/m'))
    ->write(To::output(truncate: false))
    ->mode(SaveMode::Overwrite)
    ->write(Parquet::to(__DIR__ . '/daily_revenue.parquet'))
    ->run();
```

```console
$ php daily_revenue.php
+---------------------------+---------------+
|                created_at | daily_revenue |
+---------------------------+---------------+
| 2023-10-31T00:00:00+00:00 |     206669.74 |
| 2023-10-01T00:00:00+00:00 |     227647.47 |
| 2023-08-31T00:00:00+00:00 |     237027.31 |
| 2023-07-31T00:00:00+00:00 |     240111.05 |
| 2023-07-01T00:00:00+00:00 |     225536.35 |
| 2023-05-31T00:00:00+00:00 |     234624.74 |
| 2023-05-01T00:00:00+00:00 |     231472.05 |
| 2023-03-31T00:00:00+00:00 |     231697.36 |
| 2023-03-03T00:00:00+00:00 |     211048.97 |
| 2023-01-31T00:00:00+00:00 |     225539.81 |
+---------------------------+---------------+
10 rows
```

The reasons behind creating this project can be explained in few [tweets](https://twitter.com/norbert_tech/status/1484863793280786439?s=21). 
To get familiar with basic ETL Api, please look into [flow-php/etl repository](https://github.com/flow-php/etl), everything else is listed below. 

### [Usage Examples](https://github.com/flow-php/flow/tree/1.x/examples)

## Features

* constant memory consumption
* asynchronous data processing
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

## Asynchronous Processing

* [etl-adapter-amphp](https://github.com/flow-php/etl-adapter-amphp)
* [etl-adapter-reactphp](https://github.com/flow-php/etl-adapter-reactphp)

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

### Supported PHP versions

* 8.1 - ✅
* 8.2 - ✅

## Available Entry Types

* [array](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/ArrayEntry.phpp)
* [boolean](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/BooleanEntry.php)
* [collection](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/CollectionEntry.php)
* [datetime](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry//DateTimeEntry.php)
* [float](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/FloatEntry.php)
* [json](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/JsonEntry.php)
* [list](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/ListEntry.php)
* [integer](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/IntegerEntry.php)
* [null](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/NullEntry.php)
* [object](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/ObjectEntry.php)
* [string](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/StringEntry.php)
* [structure](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/StructureEntry.php)

## Transfomers

Flow ETL provides a rich set of official transfomers, please find them all in [flow-php/etl](https://github.com/flow-php/etl/#transformers) 
repository.

## Available Adapters: 

The role of adapter is usually to provide Extractors and Loaders, occasionally adapters might also bring some specific Transformers.

<table style="text-align:center">
<thead>
  <tr>
    <th>Name</th>
    <th>Extractor (read)</th>
    <th>Loader (write)</th>
  </tr>
</thead>
<tbody>
  <tr>
      <td><a href="https://github.com/flow-php/etl-adapter-doctrine">Doctrine - DB</a></td>
      <td>✅</td>
      <td>✅</td>
  </tr>
  <tr>
      <td><a href="https://github.com/flow-php/etl-adapter-elasticsearch">Elasticsearch</a></td>
      <td>N/A</td>
      <td>✅</td>
  </tr>
  <tr>
      <td><a href="https://github.com/flow-php/etl-adapter-text">Text</a></td>
      <td>✅</td>
      <td>✅</td>
  </tr>    
  <tr>
      <td><a href="https://github.com/flow-php/etl-adapter-csv">CSV</a></td>
      <td>✅</td>
      <td>✅</td>
  </tr>
  <tr>
      <td><a href="https://github.com/flow-php/etl-adapter-json">JSON</a></td>
      <td>✅</td>
      <td>✅</td>
  </tr>
  <tr>
      <td><a href="https://github.com/flow-php/etl-adapter-parquet">Parquet</a></td>
      <td>✅</td>
      <td>✅</td>
  </tr>
  <tr>
      <td><a href="https://github.com/flow-php/etl-adapter-avro">Avro</a></td>
      <td>✅</td>
      <td>✅</td>
  </tr> 
  <tr>
      <td><a href="https://github.com/flow-php/etl-adapter-streams">File Streams</a></td>
      <td>N/A</td>
      <td>N/A</td>
  </tr>        
  <tr>
      <td><a href="https://github.com/flow-php/etl-adapter-xml">XML</a></td>
      <td>✅</td>
      <td>N/A</td>
  </tr>
  <tr>
      <td><a href="https://github.com/flow-php/etl-adapter-http">HTTP</a></td>
      <td>✅</td>
      <td>N/A</td>
  </tr>
  <tr>
      <td><a href="#">Excel</a></td>
      <td>N/A</td>
      <td>N/A</td>
  </tr>
  <tr>
      <td><a href="https://github.com/flow-php/etl-adapter-logger">Logger</a></td>
      <td>🚫</td>
      <td>✅</td>
  </tr>
</tbody>
</table>

## Sponsors 

Flow PHP is sponsored by: 

- [Blackfire](https://blackfire.io/) - the best PHP profiling and monitoring tool! 
