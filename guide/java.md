# Java Code:



Using the popular [Apache HttpComponents](https://hc.apache.org/) library:



```java
import org.apache.http.HttpEntity;
import org.apache.http.HttpResponse;
import org.apache.http.NameValuePair;
import org.apache.http.client.HttpClient;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.client.utils.URLEncodedUtils;
import org.apache.http.impl.client.HttpClientBuilder;
import org.apache.http.message.BasicNameValuePair;
import org.apache.http.util.EntityUtils;
import org.json.JSONObject;

import java.nio.charset.StandardCharsets;
import java.util.ArrayList;
import java.util.List;

public class AdvancedApiClient {
    public static void main(String[] args) {
        String apiUrl = "https://maylancer.org/api/nuban/api.php";
        String accountNumber = "12345678910";
        String bankCode = "421";

        JSONObject response = executeApiRequest(apiUrl, accountNumber, bankCode);

        // Process the response
        if (response != null) {
            System.out.println("Account Name: " + response.getString("account_name"));
            System.out.println("Account Number: " + response.getString("account_number"));
            System.out.println("Bank Code: " + response.getString("bank_code"));
            System.out.println("Bank Name: " + response.getString("Bank_name"));
            System.out.println("Status: " + response.getString("status"));
            System.out.println("Execution Time: " + response.getString("execution_time"));
        }
    }

    private static JSONObject executeApiRequest(String apiUrl, String accountNumber, String bankCode) {
        try (HttpClient httpClient = HttpClientBuilder.create().build()) {
            HttpPost httpPost = new HttpPost(apiUrl);
            List<NameValuePair> data = new ArrayList<>();
            data.add(new BasicNameValuePair("account_number", accountNumber));
            data.add(new BasicNameValuePair("bank_code", bankCode));
            httpPost.setEntity(new UrlEncodedFormEntity(data, StandardCharsets.UTF_8));

            HttpResponse httpResponse = httpClient.execute(httpPost);
            HttpEntity responseEntity = httpResponse.getEntity();
            String responseString = EntityUtils.toString(responseEntity, StandardCharsets.UTF_8);
            return new JSONObject(responseString);
        } catch (Exception e) {
            e.printStackTrace();
        }
        return null;
    }
}


```