# Vectorizer.AI.Api.AccountApi

All URIs are relative to *https://api.vectorizer.ai/api/v1*

| Method | HTTP request | Description |
|--------|--------------|-------------|
| [**GetAccountStatus**](AccountApi.md#getaccountstatus) | **GET** /account | Get account status |

<a id="getaccountstatus"></a>
# **GetAccountStatus**
> AccountStatusResponse GetAccountStatus ()

Get account status

Fetch the subscription state and remaining API credits for the authenticated account.

### Example
```csharp
using System.Collections.Generic;
using System.Diagnostics;
using Vectorizer.AI.Api;
using Vectorizer.AI.Client;
using Vectorizer.AI.Model;

namespace Example
{
    public class GetAccountStatusExample
    {
        public static void Main()
        {
            Configuration config = new Configuration();
            config.BasePath = "https://api.vectorizer.ai/api/v1";
            // Configure HTTP basic authorization: basicAuth
            config.Username = "YOUR_USERNAME";
            config.Password = "YOUR_PASSWORD";

            var apiInstance = new AccountApi(config);

            try
            {
                // Get account status
                AccountStatusResponse result = apiInstance.GetAccountStatus();
                Debug.WriteLine(result);
            }
            catch (ApiException  e)
            {
                Debug.Print("Exception when calling AccountApi.GetAccountStatus: " + e.Message);
                Debug.Print("Status Code: " + e.ErrorCode);
                Debug.Print(e.StackTrace);
            }
        }
    }
}
```

#### Using the GetAccountStatusWithHttpInfo variant
This returns an ApiResponse object which contains the response data, status code and headers.

```csharp
try
{
    // Get account status
    ApiResponse<AccountStatusResponse> response = apiInstance.GetAccountStatusWithHttpInfo();
    Debug.Write("Status Code: " + response.StatusCode);
    Debug.Write("Response Headers: " + response.Headers);
    Debug.Write("Response Body: " + response.Data);
}
catch (ApiException e)
{
    Debug.Print("Exception when calling AccountApi.GetAccountStatusWithHttpInfo: " + e.Message);
    Debug.Print("Status Code: " + e.ErrorCode);
    Debug.Print(e.StackTrace);
}
```

### Parameters
This endpoint does not need any parameter.
### Return type

[**AccountStatusResponse**](AccountStatusResponse.md)

### Authorization

[basicAuth](../README.md#basicAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Account status for the authenticated API credentials. |  -  |
| **400** | Invalid request parameters, image input, URL fetch, or Image Token. |  -  |
| **401** | Missing or invalid API credentials. |  * WWW-Authenticate - HTTP Basic authentication challenge returned with 401 responses. <br>  |
| **402** | The account does not have an API subscription, is past due, or is out of credits. |  -  |
| **413** | The uploaded image, fetched image, or requested PNG output is too large. |  -  |
| **429** | Rate limit exceeded. Back off before retrying. |  * Retry-After - Number of seconds to wait before retrying, when provided. <br>  |
| **500** | Unexpected internal error. |  -  |
| **503** | Temporary overload or internal processing timeout. Retry later. |  * Retry-After - Number of seconds to wait before retrying, when provided. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

