# Python Code:



Using the popular [requests](https://pypi.python.org/pypi/requests) library:



```python
import requests

headers = {
    'Authorization': 'Bearer Your_Bearer_Token',  # Replace with your actual Bearer token
}

params = {
    'account_number': '12345678910',
    'bank_code': '999992',
}

response = requests.get('http://nubapi.test/api/verify', headers=headers, params=params)

data = response.json()

print(f"Account Name: {data['account_name']}")
print(f"First Name: {data['first_name']}")
print(f"Last Name: {data['last_name']}")
print(f"Other Name: {data['other_name']}")
print(f"Account Number: {data['account_number']}")
print(f"Bank Code: {data['bank_code']}")
print(f"Bank Name: {data['Bank_name']}")


```


Please replace "Your_Bearer_Token" with your actual Bearer token. Also, make sure to replace 12345678910 and 999992 with the actual account number and bank code you want to retrieve.