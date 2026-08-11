![img](/profile/flow_php_banner_01_2025.png)

Flow is a PHP-based, strongly typed ETL (Extract, Transform, Load) data processing framework with ultra low memory consumption created by [Norbert Orzechowicz](https://github.com/norberttech).  
Our mission is to unify and standardize data processing approach in PHP by providing a set of tools that simplify reading, writing and transforming data on the fly between various data sources.

[![Latest Stable Version](https://poser.pugx.org/flow-php/flow/v)](https://packagist.org/packages/flow-php/flow)
[![Latest Unstable Version](https://poser.pugx.org/flow-php/flow/v/unstable)](https://packagist.org/packages/flow-php/flow)
[![License](https://poser.pugx.org/flow-php/flow/license)](https://packagist.org/packages/flow-php/flow)
[![Test Suite](https://github.com/flow-php/flow/actions/workflows/test-suite.yml/badge.svg?branch=1.x)](https://github.com/flow-php/flow/actions/workflows/test-suite.yml)

- 📈 [Project Roadmap](https://github.com/orgs/flow-php/projects/1)
- 📜 [Documentation](https://flow-php.com/documentation/)
- 🛠️ [Contributing](https://flow-php.com/documentation/contributing/)
- 🚧 [Upgrading](https://flow-php.com/documentation/upgrading/)


> [!TIP]
> In case of any questions, feel free to join our <img src="https://cdn.prod.website-files.com/6257adef93867e50d84d30e2/636e0a69f118df70ad7828d4_icon_clyde_blurple_RGB.svg" width="16px" height="16px" alt="Discord"> [Discord Server](https://discord.gg/5dNXfQyACW)

Supported PHP versions: ![PHP Version Require](https://poser.pugx.org/flow-php/flow/require/php)

---

## Sponsors 

Please find all our sponsors at https://flow-php.com/sponsor/

## Framework

Flow is developed as a mono repository for better developer experience, we maintain more than 50 packages at this point! 
Packages are divided into few groups: 

* `Core` - [`flow-php/etl`](https://packagist.org/packages/flow-php/etl)
* `Lib` - standalone independent libraries like [`flow-php/types`](https://packagist.org/packages/flow-php/types), [`flow-php/parquet`](https://packagist.org/packages/flow-php/parquet), [`flow-php/telemetry`](https://packagist.org/packages/flow-php/telemetry) or [`flow-php/filesystem`](https://packagist.org/packages/flow-php/filesystem)
* `Bridge` - connectors between frameworks/packages like [`flow-php/flow-php/psr3-telemetry-bridge`](https://packagist.org/packages/flow-php/psr3-telemetry-bridge), [`flow-php/telemetry-otlp-bridge`](https://packagist.org/packages/flow-php/telemetry-otlp-bridge)
* `Adapter` - Adapters for DataFrame that brings support for different data source/sinks [`flow-php/etl-adapter-xml`](https://packagist.org/packages/flow-php/etl-adapter-xml), [`flow-php/etl-adapter-csv`](https://packagist.org/packages/flow-php/etl-adapter-csv), [`flow-php/etl-adapter-postgresql`](https://packagist.org/packages/flow-php/etl-adapter-postgresql)
* `Extension` - [`flow-php/pg-query-ext`](https://packagist.org/packages/flow-php/pg-query-ext), [`flow-php/arrow-ext)`](https://packagist.org/packages/flow-php/arrow-ext), [`flow-php/flow-php-ex`](https://packagist.org/packages/flow-php/flow-php-ext) 

All our packages are built with minimum dependencies philosophy, libraries and bridges but also extension are fully independent from Core and Adapters. 
This means that you can use them even if you don't have a use case for whole Data Frame. 

## Usage Examples

The most up-to-date examples are available at https://flow-php.com

<details open>
<summary><strong>Data Reading</strong></summary>

- [Array](https://flow-php.com/data_frame/data_reading/array/#example)
- [CSV](https://flow-php.com/data_frame/data_reading/csv/#example)
- [Data Frame](https://flow-php.com/data_frame/data_reading/data_frame/#example)
- [Database](https://flow-php.com/data_frame/data_reading/database/#example)
- [Excel](https://flow-php.com/data_frame/data_reading/excel/#example)
- [Floe](https://flow-php.com/data_frame/data_reading/floe/#example)
- [HTTP](https://flow-php.com/data_frame/data_reading/http/#example)
- [JSON](https://flow-php.com/data_frame/data_reading/json/#example)
- [JSON Lines](https://flow-php.com/data_frame/data_reading/jsonl/#example)
- [Parquet](https://flow-php.com/data_frame/data_reading/parquet/#example)
- [Sequence Date](https://flow-php.com/data_frame/data_reading/sequence_date/#example)
- [Sequence Date Recurrences](https://flow-php.com/data_frame/data_reading/sequence_date_recurrences/#example)
- [Sequence Number](https://flow-php.com/data_frame/data_reading/sequence_number/#example)
- [XML](https://flow-php.com/data_frame/data_reading/xml/#example)

</details>

<details>
<summary><strong>Data Writing</strong></summary>

- [Array](https://flow-php.com/data_frame/data_writing/array/#example)
- [CSV](https://flow-php.com/data_frame/data_writing/csv/#example)
- [Database](https://flow-php.com/data_frame/data_writing/database/#example)
- [Database Delete](https://flow-php.com/data_frame/data_writing/database_delete/#example)
- [Database Upsert](https://flow-php.com/data_frame/data_writing/database_upsert/#example)
- [Excel](https://flow-php.com/data_frame/data_writing/excel/#example)
- [Floe](https://flow-php.com/data_frame/data_writing/floe/#example)
- [JSON Lines](https://flow-php.com/data_frame/data_writing/jsonl/#example)
- [Overwrite](https://flow-php.com/data_frame/data_writing/overwrite/#example)
- [Parquet](https://flow-php.com/data_frame/data_writing/parquet/#example)
- [Text](https://flow-php.com/data_frame/data_writing/text/#example)
- [XML](https://flow-php.com/data_frame/data_writing/xml/#example)

</details>

<details>
<summary><strong>DataFrame</strong></summary>

- [Batch By](https://flow-php.com/data_frame/batch_by/#example)
- Batch Size
  - [Collect](https://flow-php.com/data_frame/batch_size/collect/#example)
  - [Constant Size](https://flow-php.com/data_frame/batch_size/constant_size/#example)
- [Cache](https://flow-php.com/data_frame/cache/#example)
- Columns
  - [Create](https://flow-php.com/data_frame/columns/create/#example)
  - [Rename](https://flow-php.com/data_frame/columns/rename/#example)
  - [Rename Map](https://flow-php.com/data_frame/columns/rename_map/#example)
  - [Rename Replace](https://flow-php.com/data_frame/columns/rename_replace/#example)
  - [Rename Style](https://flow-php.com/data_frame/columns/rename_style/#example)
  - [Reorder](https://flow-php.com/data_frame/columns/reorder/#example)
- Transformations
  - [Custom](https://flow-php.com/data_frame/transformations/custom/#example)
  - [Select](https://flow-php.com/data_frame/transformations/select/#example)

</details>

<details>
<summary><strong>Transformations</strong></summary>

- Array
  - [Expand](https://flow-php.com/transformations/array/expand/#example)
  - [Unpack](https://flow-php.com/transformations/array/unpack/#example)
- [Call](https://flow-php.com/transformations/call/#example)
- Filtering
  - [Basic](https://flow-php.com/transformations/filtering/basic/#example)
  - [Divide](https://flow-php.com/transformations/filtering/divide/#example)
  - [Mod](https://flow-php.com/transformations/filtering/mod/#example)
- [Literals](https://flow-php.com/transformations/literals/#example)
- [Match](https://flow-php.com/transformations/match/#example)
- [Math](https://flow-php.com/transformations/math/#example)
- [Size](https://flow-php.com/transformations/size/#example)
- [Sort](https://flow-php.com/transformations/sort/#example)
- When
  - [Basic](https://flow-php.com/transformations/when/basic/#example)
  - [Else When](https://flow-php.com/transformations/when/else_when/#example)
  - [Null](https://flow-php.com/transformations/when/null/#example)
  - [Odd](https://flow-php.com/transformations/when/odd/#example)

</details>

<details>
<summary><strong>Joins</strong></summary>

- [Join](https://flow-php.com/join/join/#example)
- [Join Each](https://flow-php.com/join/join_each/#example)

</details>

<details>
<summary><strong>Aggregations</strong></summary>

- Grouping
  - [Group By](https://flow-php.com/aggregations/grouping/group_by/#example)
  - [Group By Sum](https://flow-php.com/aggregations/grouping/group_by_sum/#example)
- Aggregating Functions
  - [Average](https://flow-php.com/aggregations/aggregating_functions/average/#example)
  - [First](https://flow-php.com/aggregations/aggregating_functions/first/#example)
  - [Last](https://flow-php.com/aggregations/aggregating_functions/last/#example)
  - [Max](https://flow-php.com/aggregations/aggregating_functions/max/#example)
  - [Min](https://flow-php.com/aggregations/aggregating_functions/min/#example)
  - [Sum](https://flow-php.com/aggregations/aggregating_functions/sum/#example)
- Window Functions
  - [Dense Rank](https://flow-php.com/aggregations/window_functions/dense_rank/#example)
  - [Rank](https://flow-php.com/aggregations/window_functions/rank/#example)
  - [Row Number](https://flow-php.com/aggregations/window_functions/row_number/#example)

</details>

<details>
<summary><strong>Partitioning</strong></summary>

- [Partition Placeholders](https://flow-php.com/partitioning/partition_placeholders/#example)
- [Partition Pruning](https://flow-php.com/partitioning/partition_pruning/#example)
- [Path Partitions](https://flow-php.com/partitioning/path_partitions/#example)
- Partitioning
  - [Append](https://flow-php.com/partitioning/partitioning/append/#example)
  - [Exception If Exists](https://flow-php.com/partitioning/partitioning/exception_if_exists/#example)
  - [Ignore](https://flow-php.com/partitioning/partitioning/ignore/#example)
  - [Overwrite](https://flow-php.com/partitioning/partitioning/overwrite/#example)
- Reading
  - [Basic](https://flow-php.com/partitioning/reading/basic/#example)
  - [After Append](https://flow-php.com/partitioning/reading/after_append/#example)
  - [After Overwrite](https://flow-php.com/partitioning/reading/after_overwrite/#example)

</details>

<details>
<summary><strong>Schema</strong></summary>

- [Apply](https://flow-php.com/schema/apply/#example)
- [Display](https://flow-php.com/schema/display/#example)
- [Inferring](https://flow-php.com/schema/inferring/#example)
- [Validate](https://flow-php.com/schema/validate/#example)

</details>

<details>
<summary><strong>Filesystem</strong></summary>

- [Azure](https://flow-php.com/filesystem/azure/#example)
- [Local](https://flow-php.com/filesystem/local/#example)
- [S3](https://flow-php.com/filesystem/s3/#example)
- [Stdout](https://flow-php.com/filesystem/stdout/#example)

</details>

<details>
<summary><strong>Types</strong></summary>

- Assertions
  - [Array](https://flow-php.com/types/assertions/array/#example)
  - [Callable](https://flow-php.com/types/assertions/callable/#example)
  - [Class String](https://flow-php.com/types/assertions/class_string/#example)
  - [Constrained](https://flow-php.com/types/assertions/constrained/#example)
  - [Date](https://flow-php.com/types/assertions/date/#example)
  - [DateTime](https://flow-php.com/types/assertions/datetime/#example)
  - [Enum](https://flow-php.com/types/assertions/enum/#example)
  - [HTML](https://flow-php.com/types/assertions/html/#example)
  - [Instance Of](https://flow-php.com/types/assertions/instance_of/#example)
  - [Intersection](https://flow-php.com/types/assertions/intersection/#example)
  - [JSON](https://flow-php.com/types/assertions/json/#example)
  - [List](https://flow-php.com/types/assertions/list/#example)
  - [Literal](https://flow-php.com/types/assertions/literal/#example)
  - [Map](https://flow-php.com/types/assertions/map/#example)
  - [Mixed](https://flow-php.com/types/assertions/mixed/#example)
  - [Object](https://flow-php.com/types/assertions/object/#example)
  - [Optional](https://flow-php.com/types/assertions/optional/#example)
  - [Resource](https://flow-php.com/types/assertions/resource/#example)
  - [Scalar](https://flow-php.com/types/assertions/scalar/#example)
  - [Structure](https://flow-php.com/types/assertions/structure/#example)
  - [Time](https://flow-php.com/types/assertions/time/#example)
  - [Time Zone](https://flow-php.com/types/assertions/time_zone/#example)
  - [Union](https://flow-php.com/types/assertions/union/#example)
  - [UUID](https://flow-php.com/types/assertions/uuid/#example)
  - [XML](https://flow-php.com/types/assertions/xml/#example)
- Casting
  - [Array](https://flow-php.com/types/casting/array/#example)
  - [Boolean](https://flow-php.com/types/casting/boolean/#example)
  - [Callable](https://flow-php.com/types/casting/callable/#example)
  - [Class String](https://flow-php.com/types/casting/class_string/#example)
  - [Constrained](https://flow-php.com/types/casting/constrained/#example)
  - [Date](https://flow-php.com/types/casting/date/#example)
  - [DateTime](https://flow-php.com/types/casting/datetime/#example)
  - [Enum](https://flow-php.com/types/casting/enum/#example)
  - [HTML](https://flow-php.com/types/casting/html/#example)
  - [Instance Of](https://flow-php.com/types/casting/instance_of/#example)
  - [Intersection](https://flow-php.com/types/casting/intersection/#example)
  - [JSON](https://flow-php.com/types/casting/json/#example)
  - [List](https://flow-php.com/types/casting/list/#example)
  - [Literal](https://flow-php.com/types/casting/literal/#example)
  - [Map](https://flow-php.com/types/casting/map/#example)
  - [Mixed](https://flow-php.com/types/casting/mixed/#example)
  - [Object](https://flow-php.com/types/casting/object/#example)
  - [Optional](https://flow-php.com/types/casting/optional/#example)
  - [Resource](https://flow-php.com/types/casting/resource/#example)
  - [Scalar](https://flow-php.com/types/casting/scalar/#example)
  - [Structure](https://flow-php.com/types/casting/structure/#example)
  - [Time](https://flow-php.com/types/casting/time/#example)
  - [Time Zone](https://flow-php.com/types/casting/time_zone/#example)
  - [Union](https://flow-php.com/types/casting/union/#example)
  - [UUID](https://flow-php.com/types/casting/uuid/#example)
  - [XML](https://flow-php.com/types/casting/xml/#example)
- Validation
  - [Array](https://flow-php.com/types/validation/array/#example)
  - [Boolean](https://flow-php.com/types/validation/boolean/#example)
  - [Callable](https://flow-php.com/types/validation/callable/#example)
  - [Class String](https://flow-php.com/types/validation/class_string/#example)
  - [Constrained](https://flow-php.com/types/validation/constrained/#example)
  - [Date](https://flow-php.com/types/validation/date/#example)
  - [DateTime](https://flow-php.com/types/validation/datetime/#example)
  - [Enum](https://flow-php.com/types/validation/enum/#example)
  - [HTML](https://flow-php.com/types/validation/html/#example)
  - [Instance Of](https://flow-php.com/types/validation/instance_of/#example)
  - [Intersection](https://flow-php.com/types/validation/intersection/#example)
  - [JSON](https://flow-php.com/types/validation/json/#example)
  - [List](https://flow-php.com/types/validation/list/#example)
  - [Literal](https://flow-php.com/types/validation/literal/#example)
  - [Map](https://flow-php.com/types/validation/map/#example)
  - [Mixed](https://flow-php.com/types/validation/mixed/#example)
  - [Object](https://flow-php.com/types/validation/object/#example)
  - [Optional](https://flow-php.com/types/validation/optional/#example)
  - [Resource](https://flow-php.com/types/validation/resource/#example)
  - [Scalar](https://flow-php.com/types/validation/scalar/#example)
  - [Structure](https://flow-php.com/types/validation/structure/#example)
  - [Time](https://flow-php.com/types/validation/time/#example)
  - [Time Zone](https://flow-php.com/types/validation/time_zone/#example)
  - [Union](https://flow-php.com/types/validation/union/#example)
  - [UUID](https://flow-php.com/types/validation/uuid/#example)
  - [XML](https://flow-php.com/types/validation/xml/#example)

</details>

<details>
<summary><strong>Telemetry</strong></summary>

- [Combined](https://flow-php.com/telemetry/combined/#example)
- [Logger](https://flow-php.com/telemetry/logger/#example)
- [Meter](https://flow-php.com/telemetry/meter/#example)
- [Propagator](https://flow-php.com/telemetry/propagator/#example)
- [Resource](https://flow-php.com/telemetry/resource/#example)
- [Tracer](https://flow-php.com/telemetry/tracer/#example)

</details>
