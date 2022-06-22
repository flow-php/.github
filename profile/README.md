![img](/profile/flow_php_banner_02_2022.png)

Flow is a PHP based, strongly typed ETL (Extract Transform Load), asynchronous data processing library with constant memory consumption. 

## Usage

**Extract** from the Source, **Transform**, **Load** to the Sink. 

```php
<?php

use Flow\ETL\DSL\From;
use Flow\ETL\DSL\Transform;
use Flow\ETL\DSL\To;
use Flow\ETL\Flow;
use Flow\ETL\Memory\ArrayMemory;
use Flow\ETL\Row\Sort;
use Flow\ETL\Rows;

$array = new ArrayMemory();

(new Flow())
    ->read(From::rows(new Rows(...)))
    ->rows(Transform::keep(['id', 'name', 'status']))
    ->sortBy(Sort::desc('status'))
    ->write(To::memory($array);
```

The reasons behind creating this project can be explained in few [tweets](https://twitter.com/norbert_tech/status/1484863793280786439?s=21). 
To get familiar with basic ETL Api, please look into [flow-php/etl repository](https://github.com/flow-php/etl), everything else is listed below. 

### [Usage Examples](https://github.com/flow-php/etl-examples)

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
* Entry - Immutable, stronly typed object representing cell in a row. 
* **E**xtractor (Reader) - Memory safe, Data Source returning \Generator, yielding `Rows` to the `Pipeline`
* **T**ransformer - Data transformer receiving and returning `Rows` (in most cases transformer), one instance of `Rows` at once.  
* **L**oader (Writer) - Memory safe representation of Data Sink, responsibility of Loader is to write `Rows` into destination storage, one at time. 
* Pipeline - Interface representing ETL process, each received `Rows` instanced is pased through all `Pipes`, also responsible for error handling. 
* Pipe - Loader of Transformer instance existing in `Pipes` collection.  

### Supported PHP versions

* 8.1 - ✅

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
