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

import axios

   axios.get('https://maylancer.org/api/nuban/api.php', {
     params: {
       account_number: '12345678910',
       bank_code: '421'
     }
   })
     .then((response) => {
       const { account_name, account_number, bank_code, bank_name, status, execution_time } = response.data;
       console.log(account_name);
       console.log(account_number);
       console.log(bank_code);
       console.log(bank_name);
       console.log(status);
       console.log(execution_time);

       // Here are some useful code to get user first and last name
       let names = account_name.replace(/\s{2,}/g, ' ').split(' ');
       let firstName = names[0];
       let lastName = names[1];
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
  url: 'https://maylancer.org/api/nuban/api.php',
  method: 'GET',
  data: {
    account_number: '12345678910',
    bank_code: '421'
  },
  success: (response) => {
    console.log(response.account_name);
    console.log(response.account_number);
    console.log(response.bank_code);
    console.log(response.bank_name);
    console.log(response.status);
    console.log(response.execution_time);

    // Here are some useful code to get user first and last name
    let names = response.account_name.replace(/\s{2,}/g, ' ').split(' ');
    let firstName = names[0];
    let lastName = names[1];
  },
  error: (xhr, status, error) => {
    console.error(`An error occurred: ${error}`);
  }
});

```


::: tip
Please make sure you provided the request parameters (account_number and bank_code) as an object in the params property
:::
