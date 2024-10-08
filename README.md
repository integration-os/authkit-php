# authkit-php

Secure token generation for [IntegrationOS AuthKit](https://docs.integrationos.com/docs/authkit)
using [Composer](https://getcomposer.org/).

## Install

With composer:

```bash
composer require integrationos/authkit-php 
```

## Creating a token endpoint

You'll want to create an internal endpoint used to generate secure tokens for your frontend. You can do so by
adding code that looks like the below snippet. You can then call the file directly in the browser or using a tool like
curl or Postman by making a POST request to http://yourserver.com/endpoint.php.

```php
<?php  // file endpoint.php

require "vendor/autoload.php";

use IntegrationOS\AuthKitToken\AuthKitToken;

$authKitToken = new AuthKitToken("sk_live_12345");
$token = $authKitToken->create();

echo json_encode($token);
```

Or if you're using Laravel, you can define a route like below:

```php
<?php

use Illuminate\Support\Facades\Route;
use IntegrationOS\AuthKitToken\AuthKitToken;

Route::get('/authkit-token', function () {
    $authKitToken = new AuthKitToken("sk_live_12345");
	
    $token = $authKitToken->create();
    
    return $token;
});
```

You'll want to switch out the API Key for your own, which will later tell your frontend which integrations you'd like to
make available to your users.

If you pass an `identity` or `identityType` (`user`, `team`, or `organization`), you'll be able to query for all connections scoped to that identity. 
The identity is used to generate the unique [Connection Key](https://docs.integrationos.com/docs/setup) for the user once they successfully connect an account.

## Full Documentation

Please refer to the official [IntegrationOS AuthKit](https://docs.integrationos.com/docs/authkit) docs for a more
holistic understanding of IntegrationOS AuthKit.