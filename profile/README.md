![img](/profile/flow_php_banner_02_2022.png)

Flow is a PHP-based, strongly typed ETL (Extract, Transform, Load) and asynchronous data processing framework with low memory consumption thanks to its generator-based architecture.

[![Latest Stable Version](https://poser.pugx.org/flow-php/flow/v)](https://packagist.org/packages/flow-php/flow)
[![Latest Unstable Version](https://poser.pugx.org/flow-php/flow/v/unstable)](https://packagist.org/packages/flow-php/flow)
[![License](https://poser.pugx.org/flow-php/flow/license)](https://packagist.org/packages/flow-php/flow)
[![Test Suite](https://github.com/flow-php/flow/actions/workflows/test-suite.yml/badge.svg?branch=1.x)](https://github.com/flow-php/flow/actions/workflows/test-suite.yml)

- 📈 [Project Roadmap](https://github.com/orgs/flow-php/projects/1)
- 📜 [Documentation](https://github.com/flow-php/flow/blob/1.x/docs/introduction.md)
- 🛠️ [Contributing](CONTRIBUTING.md)
- 🚧 [Upgrading](UPGRADE.md)


> [!TIP]
> In case of any questions, feel free to join our <img src="https://cdn.prod.website-files.com/6257adef93867e50d84d30e2/636e0a69f118df70ad7828d4_icon_clyde_blurple_RGB.svg" width="16px" height="16px" alt="Discord"> [Discrod Server](https://discord.gg/5dNXfQyACW)

Supported PHP versions: [![PHP 8.1](https://img.shields.io/badge/php-~8.1-8892BF.svg)](https://php.net/) [![PHP 8.2](https://img.shields.io/badge/php-~8.2-8892BF.svg)](https://php.net/) [![PHP 8.3](https://img.shields.io/badge/php-~8.3-8892BF.svg)](https://php.net/)

---

## Usage Example

Thanks to its rich collection of adapters, Flow can read and write data between sources and destinations while applying defined transformations on the fly.

```php
<?php

declare(strict_types=1);

use function Flow\ETL\Adapter\Parquet\{from_parquet, to_parquet};
use function Flow\ETL\DSL\{data_frame, lit, ref, sum, to_output, overwrite};
use Flow\ETL\Filesystem\SaveMode;

require __DIR__ . '/vendor/autoload.php';

data_frame()
    ->read(from_parquet(__DIR__ . '/orders_flow.parquet'))
    ->select('created_at', 'total_price', 'discount')
    ->withEntry('created_at', ref('created_at')->cast('date')->dateFormat('Y/m'))
    ->withEntry('revenue', ref('total_price')->minus(ref('discount')))
    ->select('created_at', 'revenue')
    ->groupBy('created_at')
    ->aggregate(sum(ref('revenue')))
    ->sortBy(ref('created_at')->desc())
    ->withEntry('daily_revenue', ref('revenue_sum')->round(lit(2))->numberFormat(lit(2)))
    ->drop('revenue_sum')
    ->write(to_output(truncate: false))
    ->withEntry('created_at', ref('created_at')->toDate('Y/m'))
    ->saveMode(overwrite())
    ->write(to_parquet(__DIR__ . '/daily_revenue.parquet'))
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

## Sponsors 

Flow PHP is sponsored by: 

- [Blackfire](https://blackfire.io/) - the best PHP profiling and monitoring tool! 
