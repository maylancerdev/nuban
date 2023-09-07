# Javascript Code


Using the browser [Fetch API](https://pypi.python.org/pypi/requests) and a [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) request:

```js
const fetchData = async () => {
    try {
        const response = await fetch('http://nubapi.test/api/verify?account_number=12345678910&bank_code=999992', {
            method: 'GET',
            headers: {
                'Content-Type': 'application/json',
                'Authorization': 'Bearer Your_Bearer_Token' // Replace with your actual Bearer token
            }
        });

        if (!response.ok) {
            throw new Error('Request failed');
        }

        const data = await response.json();
        console.log(data);
    } catch (error) {
        console.error(error);
    }
};

fetchData();

```


Please replace "Your_Bearer_Token" with your actual Bearer token. Also, make sure to replace 12345678910 and 421 with the actual account number and bank code you want to retrieve.