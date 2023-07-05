# PHP Code example using [CURL](https://www.php.net/manual/en/ref.curl.php)


## Curl 7.34.0 or more recent ([Unless using Guzzle](#php-8-using-guzzle-for-making-http-requests))

```php
<?php

/**
 * Makes an API call using cURL.
 *
 * @param string $method The HTTP method (POST, PUT, GET).
 * @param string $url The API URL.
 * @param mixed $data The data to be sent with the request.
 * @return mixed The API response.
 * @throws Exception If the cURL request fails.
 */
function callAPI($method, $url, $data) {
    $curl = curl_init();

    // Set cURL options based on the HTTP method
    switch ($method) {
        case "POST":
            curl_setopt($curl, CURLOPT_POST, 1);
            if ($data)
                curl_setopt($curl, CURLOPT_POSTFIELDS, $data);
            break;
        case "PUT":
            curl_setopt($curl, CURLOPT_CUSTOMREQUEST, "PUT");
            if ($data)
                curl_setopt($curl, CURLOPT_POSTFIELDS, $data);
            break;
        default:
            if ($data)
                $url = sprintf("%s?%s", $url, http_build_query($data));
    }

    // Set common cURL options
    curl_setopt_array($curl, [
        CURLOPT_URL => $url,
        CURLOPT_HTTPHEADER => ['Content-Type: application/json'],
        CURLOPT_RETURNTRANSFER => true,
        CURLOPT_HTTPAUTH => CURLAUTH_BASIC
    ]);

    // Execute the cURL request
    $result = curl_exec($curl);

    // Check for cURL errors
    if ($result === false) {
        $error = curl_error($curl);
        curl_close($curl);
        throw new Exception("cURL Request Failed: $error");
    }

    curl_close($curl);

    return $result;
}

// Define the API endpoint URL
$url = 'https://maylancer.org/api/nuban/api.php';

// Set the API parameters
$params = [
    'account_number' => '{account_number}',
    'bank_code' => '{code}'
];

try {
    // Make the API call
    $get_data = callAPI('GET', $url, $params);

    // Decode the API response
    $response = json_decode($get_data, true);

    // Process the API response
    if (isset($response['account_name'])) {
        $name = explode(' ', $response['account_name']);
        $firstName = $name[0];
        $lastName = end($name);

        $data = [
            "firstname" => $firstName,
            "lastname" => $lastName,
            "account_name" => $response['account_name'],
            "account_number" => $response['account_number'],
            "bank_name" => $response['Bank_name'],
            "status" => 'success'
        ];
    } else {
        $errorMessage = 'Invalid account number entered, ' . $response['message'];

        $data = [
            "message" => $errorMessage,
            "status" => 'error'
        ];
    }

    // Output the result as JSON
    echo json_encode($data, JSON_PRETTY_PRINT);
} catch (Exception $e) {
    // Handle cURL exceptions
    $errorMessage = $e->getMessage();

    $data = [
        "message" => "API Request Error: $errorMessage",
        "status" => 'error'
    ];

    echo json_encode($data, JSON_PRETTY_PRINT);
}

?>

```


## PHP 8 version

```php
<?php

/**
 * Makes a cURL API call.
 *
 * @param string $method The HTTP method (POST, PUT, GET).
 * @param string $url The API URL.
 * @param mixed $data The data to be sent with the request.
 * @return mixed The API response.
 */
function callAPI(string $method, string $url, mixed $data): mixed {
   $curl = curl_init();
   match ($method) {
      "POST" => {
         curl_setopt($curl, CURLOPT_POST, 1);
         if ($data)
            curl_setopt($curl, CURLOPT_POSTFIELDS, $data);
      },
      "PUT" => {
         curl_setopt($curl, CURLOPT_CUSTOMREQUEST, "PUT");
         if ($data)
            curl_setopt($curl, CURLOPT_POSTFIELDS, $data);
      },
      default => {
         if ($data)
            $url = sprintf("%s?%s", $url, http_build_query($data));
      }
   };
   // OPTIONS:
   curl_setopt_array($curl, [
      CURLOPT_URL => $url,
      CURLOPT_HTTPHEADER => ['Content-Type: application/json'],
      CURLOPT_RETURNTRANSFER => 1,
      CURLOPT_HTTPAUTH => CURLAUTH_BASIC
   ]);
   // EXECUTE:
   $result = curl_exec($curl);
   if (!$result) {
      die("Connection Failure");
   }
   curl_close($curl);
   return $result;
}

// API endpoint URL
$url = 'https://maylancer.org/api/nuban/api.php';

// API parameters
$params = [
   'account_number' => '{account_number}',
   'bank_code' => '{code}'
];

// Make the API call
$get_data = callAPI('GET', $url, $params);

// Decode the API response
$response = json_decode($get_data, true);

// Process the API response
if (isset($response['account_name'])) {
   $name = explode(' ', $response['account_name']);
   $firstName = $name[0];
   $lastName = end($name);

   $data = [
      "firstname" => $firstName,
      "lastname" => $lastName,
      "account_name" => $response['account_name'],
      "account_number" => $response['account_number'],
      "bank_name" => $response['Bank_name'],
      "status" => 'success'
   ];
} else {
   $errorMessage = 'Invalid account number entered, ' . $response['message'];

   $data = [
      "message" => $errorMessage,
      "status" => 'error'
   ];
}

// Output the result as JSON
echo json_encode($data, JSON_PRETTY_PRINT);

?>

```


## PHP 8 using Guzzle for making HTTP requests: 

Make sure you have Composer installed on your system. If not, you can download and install it from the official Composer website: [Composer](https://getcomposer.org/)

Open your terminal or command prompt.

Navigate to your project directory.

Run the following command to require Guzzle and add it as a dependency to your project:

```bash 
composer require guzzlehttp/guzzle
```


Composer will fetch the latest version of Guzzle and its dependencies and add them to your project.

Once the installation is complete, you can start using Guzzle in your PHP code by including the Composer-generated autoloader at the top of your PHP file:


```php 
require_once 'vendor/autoload.php';
```

You can then proceed to use Guzzle to make HTTP requests. 

 ```php
use GuzzleHttp\Client;
use GuzzleHttp\Exception\RequestException;

try {
    $client = new Client();

    $queryParams = [
        'account_number' => '12345678910',
        'bank_code' => '421'
    ];

    $response = $client->get('https://maylancer.org/api/nuban/api.php', [
        'query' => $queryParams
    ]);

    $data = json_decode($response->getBody(), true);

    $accountName = $data['account_name'];
    $accountNumber = $data['account_number'];
    $bankCode = $data['bank_code'];
    $bankName = $data['Bank_name'];
    $status = $data['status'];
    $executionTime = $data['execution_time'];

    [$firstName, $lastName] = explode(' ', $accountName);

    echo "Account Name: $accountName" . PHP_EOL;
    echo "Account Number: $accountNumber" . PHP_EOL;
    echo "Bank Code: $bankCode" . PHP_EOL;
    echo "Bank Name: $bankName" . PHP_EOL;
    echo "Status: $status" . PHP_EOL;
    echo "Execution Time: $executionTime" . PHP_EOL;
    echo "First Name: $firstName" . PHP_EOL;
    echo "Last Name: $lastName" . PHP_EOL;
} catch (RequestException $e) {
    echo 'API Request Error: ' . $e->getMessage();
}


 ```