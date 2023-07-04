# Javascript Code


Using the browser [Fetch API](https://pypi.python.org/pypi/requests) and a [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) request:

```js
const fetchData = async () => {
  try {
    const response = await fetch('https://maylancer.org/api/nuban/api.php', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        account_number: '12345678910',
        bank_code: '421'
      })
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