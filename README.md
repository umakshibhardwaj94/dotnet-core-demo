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
    
    InProcess Hosting delivers significantly higher request throughput than OutProcess hosting.
Inprocess hosting use w3wp process to host app on IIS server.

In/OutofProcess hosting: 
>>2 Web Servers - Internal and External Web Server.
>>The internal web server is Kestrel
>>External can be IIS,Nginx or Apache.

KESTREL:
>>Cross- Server Web Server for ASP.Net core.
>>Kestrel can be used,by itself as an edge server.
>>The Process used to host the app is dotnet.exe.

Internet <--Http-->{Kestrel[dotnet.exe(Application)]}

a).Kesrel can be used as the internet facing web server.
b).Kestrel cab be used in combination with a reverse proxy.

Configuration in asp.net:
>>Files(appsettings.json,appsettings.{Environment}.json)
>>User Secrets
>>Environment variables
>>Command Line arguments 

NOTE: If user will write the configuration setting using CLI then it would be on priority and will override already written config settings.

Middleware in ASP.NET Core:
>>Process Request and Response pipeline.
		------------------------------------->
		---[Logging]--[StaticFiles]--[MVC]
		<------------------------------------
>>May simply pass the request to next middleware
>>may process and then pass the request to next Middleware
>>May handle the Request and short-circuit the pipeline.
>>May process the outgoing Response.
>>Middlewares are executed in the order they are added.

Terminal Middleware:
A middleware that doesnot call the next middleware in pipeline. So it handles the request and send reverse response so do not get the chance to execute next middleware.

Static Files:
>>By default, asp.net core is unable to serve static files like html,images etc.
>>Default directory for static files is wwwroot
>>To serve static files, use UseStaticFiles() middleware,if required.
>>To serve default files,use UseDefaultFiles() middleware, if required.
>>UseDefaultFiles() must be registered before UseStaticFiles().

Developer Exception Page:
>>To enable plug in UseDeveloperExceptionPage middleware in the pipeline.
>>Must be lugged in the pipeline as early as possible.
>>Contains stack trace,Query String,Cookies and Headers.
>>For customizing, use DeveloperExceptionPageOptions object.

Development Environments

[Development]   [Staging]   [Production]

>>ASPNETCORE_ENVIRONMENT variable sets the Runtime Environment in launchsettings.json file.
>>Hosting Environment Default value is : Production
>>On dev machine we sets the value in launchsettings.json
>>On Staging or Production machine we set in the operating system.
>>Use IHostingEnvironment service to access the runtime env.
>>In addition to standard env(Development,Staging,production), 
	custom env(UAT,QA etc) are also supported.

What is MVC?
MVC is an architectural design pattern for implementing User Interface Layer of an application
>>Model: set of classes that represent data + the logic to manage that data.
>>View : contains the display logic to present the model data
provided to it by the Controller
>>Controller : Hnadles the http request,work with the model, and selects a view to render that model.

Setup MVC in ASP.NET Core

>>Add the MVC Services to the Dependency Injection Container.
>>Add MVC middleware to the Request Pipeline.

ASP.NET Core AddMvc vs AddMvcCore:

>>AddMvcCore() method only adds the core MVC services
>>AddMvc() method adds all the required MVC services.
>>AddMvc() method calls AddMvcCore() method internally.

Model in ASP.NET Core MVC
>>Model is set of classes that represent Data+Manage Data.

Dependency Injection In Asp.Net Core:

>>To Register with Dependency Injection Container
	*AddSingleton():instance create only once within whole application.
	*AddTransient() :instance created each time when requested
	*AddScoped() :instance created once per request within the scope.
>>Benefits of DI
	*Loosely Coupled
	*Easy Unit Testing.

Controller in ASP.NET in MVC

>>Handles the incoming http request
>>Builds the model AND
>>Returns the Model data to the caller if we are building 
an API OR.
>>Select a View and pass the model data to the view.
>>The View then generates the required HTML to present the data






    
    
    
  
            
  
  
