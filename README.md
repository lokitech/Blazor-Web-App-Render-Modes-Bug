# Blazor Web App render mode interactive auto does not switch when navigating between pages

When using the default Blazor Web App template with interactivity set to auto and per page/component, first time visiting Counter page results in the page being rendered as **InteractiveServer** which is completely fine, after navigating to Home or to Weather page and then back to Counter, it is rendered in **InteractiveWasm** which is also great.

The problem occurs when I transfer the Weather page to Client project and set it to **InteractiveAuto**. After running the application and navigating to Counter or Weather page, the initial load happens in **InteractiveServer** which is also fine, but no matter how many times I navigate between Counter and Weather pages, it never makes a switch to **InteractiveWasm** as it does in the case when I navigate to Home and then back to Counter.

I would expect that after the WASM files are downloaded, the application would make a switch to **InteractiveWasm** when navigating between **InteractiveAuto** pages. As it does when I navigate from Counter to Home and back to Counter. 

When navigating from Counter to Home a POST request is made to https://localhost/_blazor/disconnect with circuitId as payload which disconnects the WebSocket. 
![image](https://github.com/dotnet/aspnetcore/assets/24671023/e6ad0836-a61e-483d-8a0f-9575879ab8cc)
So when navigating back to the Counter page a GET request is made for blazor-hotreload.js which apparently switches the application from **InteractiveServer** to **InteractiveWasm**.
![image](https://github.com/dotnet/aspnetcore/assets/24671023/e02dd9cb-e609-4f88-b74a-aa4b0bd5117c)

So as far I can see, the functionality is there, is there a way to force the switch to **InteractiveWasm** when navigating from one **InteractiveAuto** to another **InteractiveAuto** page after the WASM files are downloaded?
