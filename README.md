# Chat using SignalR and .net core 3.1
Project that implement a basic chat using an existing SignalR Resource in
Azure.

The following files have the main changes about how to implement a basic chat
with SignalR:
-ChatHub.cs:
This has the implementation of two methods the BroadcastMessage and Echo.

-Startup.cs:
In the ConfigureServices method add the following code to link with the SignalR Resource using the endpoint that you can get when you create the resource at azure.
```
services.AddSignalR()
.AddAzureSignalR(options => options.Endpoints = new ServiceEndpoint[]
{
    new ServiceEndpoint("<Endpoint><AccesKey>", EndpointType.Primary, "region1"),
    new ServiceEndpoint("<Endpoint><AccesKey>", EndpointType.Secondary, "region2"),
});
```
In the Configure method add the following code:
```
app.UseEndpoints(endpoints =>
    {
        endpoints.MapHub<ChatHub>("/chat");
    });
```

-wwwroot/index.html
This file has the template for the frontend of the chat


More information in this [link](https://docs.microsoft.com/en-us/azure/azure-signalr/signalr-quickstart-dotnet-core#:~:text=To%20create%20an%20Azure%20SignalR,the%20results%2C%20and%20select%20Create.)
