# PinkfireBundle

Symfony bundle to integrate support of [Pinkfire](https://github.com/pinkfire/pinkfire).

Pinkfire is a great tool to help debugging SOA (Service Oriented Architecture) by centralizing logs.

## Requirements

* Symfony 2.3.x

## Documentation

### Install with composer

```
composer.phar require "pinkfire/pinkfire-bundle"
```

### Update your app/AppKernel.php

``` php
<?php
    //...
    if (in_array($this->getEnvironment(), array('dev', 'test'))) {
        //...
        $bundles[] = new Pinkfire\PinkfireBundle\PinkfireBundle();
    }
```

### Update your config (app/config/config_dev.yml)

``` yaml
pinkfire:
    application : "my-application" # required
    host: "localhost"              # Optional
    port: 3000                     # Optional
```

If you want to forward logs from monolog

``` yaml
monolog:
    handlers:
        pinkfire:
            type: service
            id: pinkfire.monolog_handler
```

# Use

You can use the the service `pinkfire.client` like this:

```php
// ...
$client = $this->get('pinkfire.client');
$client->push('my_path', 'my_channel', 'my_message', 'info', ['my_context' => 'context'], ['link_1' => 'https://github.com/pinkfire/PinkfireBundle']);
```
