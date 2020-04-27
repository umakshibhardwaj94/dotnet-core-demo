# dotnet-core-demo
#Asp.NET Core Benefits n Features:
      1. Can be developed and run across different platforms like : Windows,Mac,Linux.
      2. Asp.Net only host by IIS but ASP.NET CORE can be hosted on :IIS,Apache,Docker,Self-host in your own process.
      3.One Unifies programming model fpr MVC and Web API : Both MVC and API Controller class inherit from the same Controller base             class and results IActionResult.
        >.IActionResult
          >> ViewResult >>JsonResult
       4.Built-in Support with Dependency Injection.
       5.Testability
       6.Open-Source and actively develop.
       7.Modular :> provides Modularity with Middleware Components.
                  >Both the request and response pipelines are composed using the middleware components
                  >Rich set of middleware components are provided out of the box.
                  >Custom Middleware Components can also be created.
       8.File or Folder references are no longer included in project file, but it will add in asp.net project.
 
 #AspNetCoreHostingModel
  >decides how the app should be hosted /InProcess or OutProcess
  >InProcess hosts the app inside of IIS worker process (w3wp.exe)
  >(Default one)OutOfProcess is hosting model forward web requests to a backend ASP.Net core running the kestrel server.
  
  #Significance of Program.cs or Main() method
    Question: Why do we have main() mmethod in Asp.Net core application?
    Answer : Because initially when the asp.net core application starts then it starts as Console application.
            Its an entry Point for the application.
    
    When Main() Method configures ASP.NET Core and starts it and at that point it becomes an ASP.NET core web application.
  
            
  
  
