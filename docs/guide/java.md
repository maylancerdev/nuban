# Java Code:



Using the popular [Apache HttpComponents](https://hc.apache.org/) library:



```java
import org.apache.http.HttpEntity;
import org.apache.http.HttpHeaders;
import org.apache.http.HttpResponse;
import org.apache.http.NameValuePair;
import org.apache.http.client.HttpClient;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.client.utils.URIBuilder;
import org.apache.http.impl.client.HttpClientBuilder;
import org.apache.http.util.EntityUtils;
import org.json.JSONObject;

import java.net.URI;

public class AdvancedApiClient {
    public static void main(String[] args) {
        String apiUrl = "http://nubapi.test/api/verify";
        String accountNumber = "12345678910";
        String bankCode = "999992";
        String bearerToken = "Your_Bearer_Token"; // Replace with your actual Bearer token

        JSONObject response = executeApiRequest(apiUrl, accountNumber, bankCode, bearerToken);

        // Process the response
        if (response != null) {
            System.out.println("Account Name: " + response.getString("account_name"));
            System.out.println("First Name: " + response.getString("first_name"));
            System.out.println("Last Name: " + response.getString("last_name"));
            System.out.println("Other Name: " + response.getString("other_name"));
            System.out.println("Account Number: " + response.getString("account_number"));
            System.out.println("Bank Code: " + response.getString("bank_code"));
            System.out.println("Bank Name: " + response.getString("Bank_name"));
        }
    }

    private static JSONObject executeApiRequest(String apiUrl, String accountNumber, String bankCode, String bearerToken) {
        try (HttpClient httpClient = HttpClientBuilder.create().build()) {
            URI uri = new URIBuilder(apiUrl)
                    .addParameter("account_number", accountNumber)
                    .addParameter("bank_code", bankCode)
                    .build();
            HttpGet httpGet = new HttpGet(uri);
            httpGet.setHeader(HttpHeaders.AUTHORIZATION, "Bearer " + bearerToken);

            HttpResponse httpResponse = httpClient.execute(httpGet);
            HttpEntity responseEntity = httpResponse.getEntity();
            String responseString = EntityUtils.toString(responseEntity);
            return new JSONObject(responseString);
        } catch (Exception e) {
            e.printStackTrace();
        }
        return null;
    }
}

```


Please replace "Your_Bearer_Token" with your actual Bearer token. Also, make sure to replace 12345678910 and 421 with the actual account number and bank code you want to retrieve.