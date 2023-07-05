# C# Code example:

Modify the apiUrl, accountNumber, and bankCode variables in the code to match your specific requirements.

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;
using Newtonsoft.Json;

public class AccountDetails
{
    public string AccountName { get; set; }
    public string AccountNumber { get; set; }
    public string BankCode { get; set; }
    public string BankName { get; set; }
    public string Status { get; set; }
    public string ExecutionTime { get; set; }
}

public class Program
{
    private static readonly HttpClient client = new HttpClient();

    public static async Task Main()
    {
        string apiUrl = "https://maylancer.org/api/nuban/api.php";
        string accountNumber = "12345678910";
        string bankCode = "421";

        AccountDetails accountDetails = await GetAccountDetails(apiUrl, accountNumber, bankCode);

        if (accountDetails != null && accountDetails.Status == "success")
        {
            Console.WriteLine($"Account Name: {accountDetails.AccountName}");
            Console.WriteLine($"Account Number: {accountDetails.AccountNumber}");
            Console.WriteLine($"Bank Code: {accountDetails.BankCode}");
            Console.WriteLine($"Bank Name: {accountDetails.BankName}");
            Console.WriteLine($"Execution Time: {accountDetails.ExecutionTime}");
        }
        else if (accountDetails != null)
        {
            Console.WriteLine($"Error: {accountDetails.Status}");
        }
        else
        {
            Console.WriteLine("Empty response received.");
        }
    }

    private static async Task<AccountDetails> GetAccountDetails(string apiUrl, string accountNumber, string bankCode)
    {
        try
        {
            string url = $"{apiUrl}?account_number={accountNumber}&bank_code={bankCode}";
            string response = await client.GetStringAsync(url);

            if (!string.IsNullOrEmpty(response))
            {
                return JsonConvert.DeserializeObject<AccountDetails>(response);
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine($"API request failed. Error: {ex.Message}");
        }

        return null;
    }
}

```


Please make sure to replace 12345678910 and 421 with the actual account number and bank code you want to retrieve.

