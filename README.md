# Azure Storage PHP

[![Latest Version on Packagist](https://img.shields.io/packagist/v/azure-oss/storage.svg)](https://packagist.org/packages/azure-oss/storage)
[![Packagist Downloads](https://img.shields.io/packagist/dt/azure-oss/storage)](https://packagist.org/packages/azure-oss/storage)

Community-driven PHP SDKs for Azure, because Microsoft won't.

In November 2023, Microsoft officially archived their [Azure SDK for PHP](https://github.com/Azure/azure-sdk-for-php) and stopped maintaining PHP integrations for most Azure services. No migration path, no replacement — just a repository marked read-only.

We picked up where they left off.

<img src="https://azure-oss.github.io/img/logo.svg" width="150" alt="Screenshot">

## Documentation

You can read the documentation [here](https://azure-oss.github.io).

## Install

```shell
composer require azure-oss/storage
```

## Quickstart

```php
<?php

use AzureOss\Storage\Blob\BlobServiceClient;
use AzureOss\Storage\Blob\Models\UploadBlobOptions;

$service = BlobServiceClient::fromConnectionString(
    getenv('AZURE_STORAGE_CONNECTION_STRING')
);

$container = $service->getContainerClient('quickstart');
$container->createIfNotExists();

$blob = $container->getBlobClient('hello.txt');

$blob->upload(
    'Hello from Azure-OSS',
    new UploadBlobOptions(contentType: 'text/plain')
);

$download = $blob->downloadStreaming();
$content = $download->content->getContents();

echo $content.PHP_EOL; // Hello from Azure-OSS

foreach ($container->getBlobs() as $item) {
    echo $item->name.PHP_EOL;
}

// Optional cleanup
$blob->deleteIfExists();
// $container->deleteIfExists();
```

## License

This project is released under the MIT License. See [LICENSE](https://github.com/Azure-OSS/azure-storage-php-monorepo/blob/02759360186be8d2d04bd1e9b2aba3839b6d39dc/LICENSE) for details.

