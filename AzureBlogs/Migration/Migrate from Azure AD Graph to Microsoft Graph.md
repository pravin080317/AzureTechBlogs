# Migrate from Azure AD Graph to Microsoft Graph:

<small>As a developer using Azure AD Graph, you may have heard that the service will be retired on June 30, 2022, and that you should migrate to Microsoft Graph. But what does that mean for you, and how do you make the switch? In this post, we'll provide an overview of the migration process and show you how to use Microsoft Graph to replace your Azure AD Graph calls.</small>

### Why is Azure AD Graph being retired?
<small>Azure AD Graph was created as a way to manage identities and access in Azure Active Directory. However, over time, Microsoft Graph has become the preferred way to interact with Microsoft 365 services, including Azure Active Directory. Microsoft Graph offers a unified API that provides access to a broad set of data, including users, groups, messages, files, and more. By using Microsoft Graph, developers can build apps that integrate with multiple Microsoft 365 services, using a single API endpoint and authentication flow.
</small>
### What's the difference between Azure AD Graph and Microsoft Graph?
<small>Azure AD Graph and Microsoft Graph both provide APIs for accessing Azure Active Directory, but there are some differences between the two. Here are some of the key distinctions:

Azure AD Graph only supports Azure Active Directory, while Microsoft Graph supports a wide range of Microsoft 365 services, including Azure Active Directory, Exchange Online, SharePoint, OneDrive, and Teams.
Microsoft Graph offers more functionality than Azure AD Graph, including support for managing device settings, creating and managing teams and channels, and accessing insights and analytics.
Microsoft Graph uses a modern authentication flow based on OAuth 2.0 and OpenID Connect, while Azure AD Graph uses an older authentication flow based on OAuth 2.0 and the Azure AD authentication endpoint.
Microsoft Graph provides a unified API endpoint, while Azure AD Graph requires separate API endpoints for different resource types.
How do I migrate from Azure AD Graph to Microsoft Graph?
The migration process from Azure AD Graph to Microsoft Graph involves three main steps:

Review your current Azure AD Graph usage and identify the APIs you need to replace with Microsoft Graph.
Update your app code to use Microsoft Graph instead of Azure AD Graph.
Test your app thoroughly to ensure that it works as expected with Microsoft Graph.
Let's take a closer look at each step.</small>

### 1. Review your current Azure AD Graph usage
<small>The first step in migrating from Azure AD Graph to Microsoft Graph is to review your current usage of Azure AD Graph and identify the APIs that you need to replace. You can use the Azure AD Graph Reporting API to get a report of the API usage for your tenant. The report will show you which APIs are being used, how often they are being called, and by which apps and users.

Once you have identified the APIs that you need to replace, you can review the Microsoft Graph documentation to find the equivalent APIs and learn how to use them.</small>

### 2. Update your app code to use Microsoft Graph
<small>The next step is to update your app code to use Microsoft Graph instead of Azure AD Graph. This will involve replacing your existing Azure AD Graph calls with equivalent Microsoft Graph calls. Here's an example of how to do this in C#:</small>

```
// Azure AD Graph code
var client = new ActiveDirectoryClient(new Uri("https://graph.windows.net/yourtenant.onmicrosoft.com"), async () => await GetTokenAsync());
var user = await client.Users.Where(u => u.ObjectId == "12345").ExecuteSingleAsync();
Console.WriteLine(user.DisplayName);

// Microsoft Graph code
var client = new GraphServiceClient(new DelegateAuthenticationProvider(async (requestMessage) =>
{
    var accessToken = await GetTokenAsync();
    requestMessage.Headers.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
}));
var user = await client.Users["12345"].Request().GetAsync();
Console.WriteLine(user.DisplayName);
```   

As you can see, the Microsoft Graph code is similar to the Azure AD Graph code, but with a few key differences:

- The API endpoint is different (`https://graph.windows.net` for Azure AD Graph vs. `https://graph.microsoft.com` for Microsoft Graph).
- The authentication flow is different (the `ActiveDirectoryClient` class in Azure AD Graph uses a callback function to get an access token, while the `GraphServiceClient` class in Microsoft Graph uses a delegate authentication provider).
- The API calls are slightly different (the Azure AD Graph code uses LINQ queries to filter and sort results, while the Microsoft Graph code uses fluent APIs to build requests).

You'll need to update all of your Azure AD Graph calls to use the equivalent Microsoft Graph calls, and make any necessary changes to the authentication flow and API endpoint.

### 3. Test your app thoroughly

The final step in the migration process is to test your app thoroughly to ensure that it works as expected with Microsoft Graph. You should test all of the scenarios that your app supports, including authentication, authorization, and data access. You should also test any custom code or integrations that you have built on top of Azure AD Graph.

To help with testing, Microsoft provides a Graph Explorer tool that allows you to explore the Microsoft Graph API and test your app's integration with it. You can also use the Microsoft Graph SDKs for various programming languages to simplify the integration process and reduce the risk of errors.

### Additional Resources
To help you with the migration process, Microsoft provides a variety of resources, including:

Microsoft Graph documentation: The Microsoft Graph documentation provides comprehensive guidance on using Microsoft Graph, including API reference documentation, tutorials, and code samples.

Azure AD Graph to Microsoft Graph migration guide: This guide provides an overview of the migration process and offers guidance on how to replace Azure AD Graph calls with equivalent Microsoft Graph calls.

Microsoft Graph training courses: Microsoft offers a variety of training courses for developers who want to learn how to use Microsoft Graph, including online courses, workshops, and certification programs.

Microsoft Graph community: The Microsoft Graph community is a great resource for developers who want to connect with other developers, get help with Microsoft Graph, and share their experiences and best practices.

## Conclusion

In summary, Azure AD Graph is being retired on June 30, 2022, and developers are encouraged to migrate to Microsoft Graph. Microsoft Graph provides a unified API for accessing Microsoft 365 services, including Azure Active Directory, and offers more functionality and a modern authentication flow. The migration process involves reviewing your current Azure AD Graph usage, updating your app code to use Microsoft Graph, and testing your app thoroughly. By following these steps, you can ensure a smooth transition to Microsoft Graph and continue to build great apps on the Microsoft 365 platform.

