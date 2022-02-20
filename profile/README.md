# Flow PHP 

Flow is a PHP based, strongly typed (on data but also on API level) ETL (Extract Transform Load) framework. 

The reasons behind creating this project can be explained in few [tweets](https://twitter.com/norbert_tech/status/1484863793280786439?s=21). 

By default ETL is a synchronouse, memory safe process. 
In some cases, it might become handy to process data asynchronously, Flow is not yet fully ready for it but we are doing good progress with [etl-async](https://github.com/flow-php/etl-async) abstraction and [reactphp adapter](https://github.com/flow-php/etl-async-adapter-reactphp).

To get familiar with basic ETL Api, please look into [flow-php/etl repository](https://github.com/flow-php/etl), everything else is listed below. 

### Building blocks

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

### Available Entry Types

* [Array](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/ArrayEntry.phpp)
* [Boolean](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/BooleanEntry.php)
* [Collection](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/CollectionEntry.php)
* [DateTime](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry//DateTimeEntry.php)
* [Float](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/FloatEntry.php)
* [Integer](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/IntegerEntry.php)
* [Null](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/NullEntry.php)
* [Object](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/ObjectEntry.php)
* [String](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/StringEntry.php)
* [Structure](https://github.com/flow-php/etl/blob/1.x/src/Flow/ETL/Row/Entry/StructureEntry.php)

### Transfomers

Flow ETL provides a rich set of official transfomers, please find them all in [flow-php/etl](https://github.com/flow-php/etl/#transformers) 
repository.

### Available Adapters: 

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

