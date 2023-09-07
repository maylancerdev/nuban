# Error response 

Here's an illustration of an instance where incorrect account information has been provided:


```php
{
    "status": false,
    "message": "Account information not available, Please try again or verify the submitted details."
}
```

Or when a required variable, such as the account number or bank code, is missing:


```php
{
    "success": false,
    "message": {
        "account_number": [
            "The account number field must have at least 10 digits."
        ]
    }
}
```

If you are encountering the aforementioned message despite correctly specifying the variable, it is crucial to verify that you are sending the request appropriately as an HTTP POST request.