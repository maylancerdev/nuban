# Python Code:



Using the popular [requests](https://pypi.python.org/pypi/requests) library:



```python
import requests

resp = requests.post('https://maylancer.org/api/nuban/api.php', {

  'account_number': '12345678910',
  'bank_code': '421',

})

print(resp.json())

```