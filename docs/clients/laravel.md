# Laravel Nubapi Client 

View the Laravel client on GitHub at [https://github.com/donejeh/nuban-api](https://github.com/donejeh/nuban-api)

## Installation


To install, require the package from composer:
```
composer require donejeh/nuban
```


## Application Service Providers...
```
 Donejeh\Nuban\NubapiServiceProvider::class

```


## Configuration 

```cmd
php artisan vendor:publish --provider="Donejeh\Nuban\NubapiServiceProvider" --tag="config"
```


Once run, you should see a new nubapi.php file in your config folder, with contents that look like this:

```php 

<?php

// config for donejeh/nuban

return [


    // The Host of the API.
    'host' => env('NUB_API_HOST', 'https://nubapi.com/api'),


    /**
     * Your API Token from (https://nubapi.com/user/api-tokens)
     *
     */
    'api_token' => env('NUB_API_TOKEN', ''),



     'options' => [
            // Validate number on your server without making an APi request.
            'validate_number_locally' => true,

             //This timeout applies to client connections and determine when
             //The whole response must be read before it exceeded
             'request_timeout' => 5,

        ]



];


```


## APi Token
This is your API token from nubapi.com (nubapi is completely free for personal, commercial and open source projects.)




## API Usage

Make sure you obtain your API key and configure your API Token in your application, now you can now in your Laravel application controller add the following code:

```
use Donejeh\Nuban\Nubapi;


$nubanApi = app(NubanApi::class);
$response = $nubanApi->getAccountDetails('1056684123', '013');

print_r($response);


```


