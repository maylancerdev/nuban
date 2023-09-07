# jQuery

## jQuery code example using Axios



Installing Axios

npm:

```
$ npm install axios
```

The Bower package manager:
```
$ bower install axios
```

Or a content delivery network:
```
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

Code example:


```javascript

import axios from 'axios';

axios.get('http://nubapi.test/api/verify', {
    headers: {
        'Authorization': 'Bearer Your_Bearer_Token' // Replace with your actual Bearer token
    },
    params: {
        account_number: '12345678910',
        bank_code: '999992'
    }
})
    .then((response) => {
        const { account_name, first_name, last_name, other_name, account_number, bank_code, Bank_name } = response.data;
        console.log(account_name);
        console.log(first_name);
        console.log(last_name);
        console.log(other_name);
        console.log(account_number);
        console.log(bank_code);
        console.log(Bank_name);
    })
    .catch((error) => {
        console.error('An error occurred:', error);
    });


```




## Jquery code example using Ajax


Download jQuery: Visit the official [jQuery website](https://jquery.com/) and download the latest version of jQuery. You have the option to choose the production version or the development version



Code example using jQuery's $.ajax() function to make an HTTP GET request: 

```javascript 
$.ajax({
    url: 'http://nubapi.test/api/verify',
    method: 'GET',
    headers: {
        'Authorization': 'Bearer Your_Bearer_Token' // Replace with your actual Bearer token
    },
    data: {
        account_number: '12345678910',
        bank_code: '999992'
    },
    success: (response) => {
        console.log(response.account_name);
        console.log(response.first_name);
        console.log(response.last_name);
        console.log(response.other_name);
        console.log(response.account_number);
        console.log(response.bank_code);
        console.log(response.Bank_name);
    },
    error: (xhr, status, error) => {
        console.error(`An error occurred: ${error}`);
    }
});


```


Please replace "Your_Bearer_Token" with your actual Bearer token. Also, make sure to replace 12345678910 and 999992 with the actual account number and bank code you want to retrieve.
