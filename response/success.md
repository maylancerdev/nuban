# Response:


The `/api.php` endpoint will respond with JSON:


| response | meaning |
| ------ | ------ |
| success | Whether the account was successfully lookup (true/false). |
| account_number | Lookup account number |
| account_name  | Bank account full name |
| Bank_name | Bank name |
| bank_code | Unique bank code identifier |
| requests | Request type (Paid/Free) |
| execution_time | Total lookup execution time |



An example of a account successfully lookup:


```JSON
{
    "account_number": "123567890",
    "account_name": "CHIDUBEM IJENDU",
    "Bank_name": "Bowen Microfinance Bank",
    "bank_code": "50931",
    "requests": "Free",
    "execution_time": "0.09 secs",
    "status": "Account number resolved"
}

```
