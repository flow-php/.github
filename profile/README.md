# Flow PHP 

Flow is a PHP based, strongly typed ETL (Extract Transform Load) data processing library. 

## Usage

**Extract** from the Source, **Transform**, **Load** to the Sink. 

```php
<?php 

ETL::extract($extractor)
    ->transform($transformer1)
    ->transform($transformer2)
    ->transform($transformer3)
    ->load($loader)
    ->run();
```

The reasons behind creating this project can be explained in few [tweets](https://twitter.com/norbert_tech/status/1484863793280786439?s=21). 
To get familiar with basic ETL Api, please look into [flow-php/etl repository](https://github.com/flow-php/etl), everything else is listed below. 

## Asynchronous Processing

* [etl-async](https://github.com/flow-php/etl-async)
  * [etl-async-adapter-reactphp](https://github.com/flow-php/etl-async-adapter-reactphp)

## Building blocks

* Rows - Immutable colllection of `Row` objects. 
* Row - Immutable, strongly typed collection of `Entry` objects. 
* Entry - Immutable, stronly typed object representing cell in a row. 
* **E**xtractor - Memory safe, Data Source returning \Generator, yielding `Rows` to the `Pipeline`
* **T**ransformer - Data transformer receiving and returning `Rows` (in most cases transformer), one instance of `Rows` at once.  
* **L**oader - Memory safe representation of Data Sink, responsibility of Loader is to write `Rows` into destination storage, one at time. 
* Pipeline - Interface representing ETL process, each received `Rows` instanced is pased through all `Pipes`, also responsible for error handling. 
* Pipe - Loader of Transformer instance existing in `Pipes` collection.  

### Supported PHP versions

* 7.4 - ✅
* 8.0 - ✅
* 8.1 - ⚙ (work in progress)

## Available Entry Types

* [array](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/ArrayEntry.phpp)
* [boolean](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/BooleanEntry.php)
* [collection](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/CollectionEntry.php)
* [datetime](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry//DateTimeEntry.php)
* [float](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/FloatEntry.php)
* [json](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/JsonEntry.php)
* [integer](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/IntegerEntry.php)
* [null](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/NullEntry.php)
* [object](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/ObjectEntry.php)
* [string](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/StringEntry.php)
* [structure](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/StructureEntry.php)
* [xml](https://github.com/flow-php/etl-adapter-xml/blob/1.x/src/Flow/ETL/Row/Entry/XMLEntry.php)

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

