<div align="center">

[![Flow PHP](/profile/flow_php_banner_01_2025.png)](https://flow-php.com)

Flow is a PHP-based, strongly typed data processing framework with a low memory footprint.

[Documentation](https://flow-php.com/documentation/) · [Quick Start](https://flow-php.com/documentation/quick-start/) · [Roadmap](https://github.com/orgs/flow-php/projects/1) · [Discord](https://discord.gg/5dNXfQyACW)

</div>

```bash
composer require flow-php/etl flow-php/etl-adapter-csv
```

```php
data_frame()
    ->read(from_csv(__DIR__ . '/orders.csv'))
    ->withColumn('revenue', ref('total_price')->minus(ref('discount')))
    ->groupBy(['created_at'])
    ->aggregate(sum(ref('revenue')))
    ->write(to_csv(__DIR__ . '/revenue.csv'))
    ->run();
```

## Author

Flow is created and maintained by [Norbert Orzechowicz](https://github.com/norberttech) and built in the open since day one.

## Why Flow

- **One API for every format**. Read and write CSV, JSON, XML, Parquet, Excel, Avro and databases. Change `to_csv()` to `to_parquet()` and the pipeline stays the same.
- **Bounded memory**. At the memory limit, sorts, joins and group-bys spill to disk. Large files do not crash the process.
- **Strict schemas**. Flow infers the schema or validates the one you declare. Corrupted records go to a file that you choose.
- **An optimizer**. Flow pushes filters and limits into the source. `explain()` shows each stage of the pipeline.
- **Pure PHP, faster with extensions**. Flow runs on every PHP host. Optional native extensions speed up the same pipeline and give identical results.
- **No install needed to try it**. The [playground](https://flow-php.com/playground/) runs Flow in your browser.

## Start here

All development happens in one repository: [`flow-php/flow`](https://github.com/flow-php/flow).
Open issues, discussions and pull requests there.

The other repositories in this organization are read-only copies of single packages.
Composer installs packages from them. They do not accept pull requests.

## Packages

Flow has more than 50 packages. Libraries, bridges and extensions do not depend on the core, so you can use each of them alone.

- Core: [`flow-php/etl`](https://github.com/flow-php/etl), the DataFrame
- Libraries: [`parquet`](https://github.com/flow-php/parquet), [`types`](https://github.com/flow-php/types), [`filesystem`](https://github.com/flow-php/filesystem), [`telemetry`](https://github.com/flow-php/telemetry), [`postgresql`](https://github.com/flow-php/postgresql)
- Adapters: CSV, JSON, XML, Parquet, Excel, PostgreSQL and more data sources for the DataFrame
- Bridges: connections to Symfony, PSR-3, OpenTelemetry and cloud filesystems
- Extensions: [`arrow-ext`](https://github.com/flow-php/arrow-ext), [`pg-query-ext`](https://github.com/flow-php/pg-query-ext), [`flow-php-ext`](https://github.com/flow-php/flow-php-ext)

[Packagist](https://packagist.org/packages/flow-php/) has the full list.

## Contribute

- Read the [contributing guide](https://flow-php.com/documentation/contributing/) first.
- Ask your questions on [Discord](https://discord.gg/5dNXfQyACW) before you start a large change.
- Use the [security policy](https://github.com/flow-php/flow/security/policy) to report a security problem.

## Sponsors

Flow is free and open source.
You can [sponsor the project](https://github.com/sponsors/flow-php) on GitHub.
The [sponsor page](https://flow-php.com/sponsor/) lists all sponsors.
