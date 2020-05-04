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


--------------SOLID PRINCIPLES--------------------------
SOLID :

---------------------------------------- SRP ------------------------------------------------------
Practice PDD(Pain Driven Dev)

s: Each software should hv only 1 reason to change.

What is Rsponsibility?
Class should have:
>>Persistence
>>Logging
>>Validation
>>Business Logic

Tight Coupling can cause a class difficult to chnge.
Loosely Coupled : less dependent on each other and easy to modify.
>>Cohesion :class elemnts that belongs together are cohesive.
A class in which the methods don't use data of each other i.e: less cohesive.
or behaivour with one another.

Coupling : Its b/w 2 classes.


Responsibities and testibility:

Responsibilities have direct relation to testibility.
Tests become:
>Longer
>More Complex
>Brittle
>Coupled to implementation.

-> By applying SRP now rather then having implementation class methods delegates behaviour by using other class methods

-> SRP strive for high cohesion (dependent methods/behaviour should be together) and loose coupling (between two or more classes)

-> Keep classes small, focused, and testable

------------------------------------------- Open/ Closed Principle --------------------------------------------------------------
-> Software entites (classes, modules, functions etc.) should be open for extension, but closed for modification.

-> It should be possible to change the behaviour of a method without editing its source code.

-> Open to extension
	- New behaviour can be added in the future
	- Code that is closed to extension has fixed behaviour
-> Closed to modification
	- Changes to source or binary code are not required
	- The only way to change the behaviour of code that is closed to the extension is to change the code itself

-> Why should code be closed to the modification?
	- Less likely to introduce bugs in code we don't touch or redeploy
	- Fewer conditionals in code that is ooen to extension result in simpler code
-> Balance abstraction and concreteness

-> Abstraction adds complexity

-> How can you predict future changes?
	- Start concrete (method should do only one thing)
	- Modify the code the first time or two
	- By the third modification, consider making the code open to extension for that axis of change
-> Typical approaches to OCP?
	- Parameters : by pass parameters to functions/methods we can change behaviour
	- Inheritance : Many design patterns leverage facilicitate to diffrent type of inheritance, simple add new child with existing features
	  	(by making parent method as virtual and override in child classes to change behaviour)
	- Composition/Injection : By adding dependency injection we can change behaviour without changing code
	- Extension methods - By creating concrete extension methods

-> Perfer implementing new features in new classes
	- Design class to suit problem at hand
	- Nothing in current system depends on it
	- Can add behaviour without touching exiting code
	- Can follow SRP
	- Can be unit tested

-> Packages and Libraries follows OCP
	-> Closed for modification
		- consumer cannot changes package contents
	-> Closed for modification in other sense
		- Should not break consumers when new behaviour is added
	-> Open to extension
		- Consumer should be able to extend the package to suit their own needs

------------------------------------------- Liskov Substitution Principle --------------------------------------------------------------
-> Subtypes must be substitutable for their base types

-> Ensure base type invariants are enforces (means your all methods should be implemented)

-> Basic Object Oriented Design
	- Something IS-A something else
		- An eagle IS-A bird
	- Something HAS-A property
		- An address HAS-A city

-> LSP states that IS-A relationship is insufficient and should be replaced with IS-SUBSTITUTABLE-FOR

-> Detecting LSP voilatios in Your code?
	- If you are checking type with 'is' or 'as' in polymorhic code (means it should work with type or any subtype)
	- Null checks
	- NotImplementedException
-> LSP is a Subset of Polymorphism
	- Polymorphism IS-A relationship and LSP IS-SUBSTITUTABLE 

-> Tell, Don't ASk means:
	Data & Logic seperate vs Data and logic together
For ex we have Print Report class which has method PrintEmployee and PrintManager, so every time when employee comes, Report class check its type and on the basis it print report.
- Rather then Asking everytime, Tell to print report to Manager and Employee by adding print method in employee and manager class

------------------------------------------- Interface Segregation Principle --------------------------------------------------------------
-> Clients should not forced to depend on methods they don't use

-> Violating ISP results in classes that depend on things they don't need

-> Large interfeces means more dependencies mean more coupling

- More birttle code

-> Detecting ISP violations in your code?
	- Large interfaces
	- NotImplementedExceptions
	- Code uses just a small subset of a larger interface

-> By using multiple interfaces, create small small interfaces with cohesive functionality and add it to parent

-> Probably use Adapter pattern to solve this problem

-> ISP is related to LSP (there should not be any notimplementedexception) and highly dependent on Cohesion and SRP

-> Fixing ISP violations
	- Break up large interfaces into smaller ones (componse fat interfaces from smaller ones for backward compatibility)
	- To address large interface you don't control
		- Create a small, cohesive interface
		- Use the Adapter design pattern so your code can work with the Adapter
-> Prefer small, cohesive interfaces to large, expansive ones
-> Following ISP helps with SRP and LSP
-> Breakup large interfaces by using 
	- Interface inheritance
	- The Adapter design pattern






    
    
    
  
            
  
  
