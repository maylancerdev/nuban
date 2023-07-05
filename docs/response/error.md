# Error response 

Here's an illustration of an instance where incorrect account information has been provided:


```php
{
    "message": "Try again. Unable to get bank details",
    "status": "error"
}
```

Or when a required variable, such as the account number or bank code, is missing:


```php
{
    "message": "Only 10-digits account number is allowed",
    "status": "error"
}
```

If you are encountering the aforementioned message despite correctly specifying the variable, it is crucial to verify that you are sending the request appropriately as an HTTP POST request.