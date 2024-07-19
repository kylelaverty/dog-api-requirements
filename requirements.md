# Dog API Microservice 

We need a microservice that is in a docker container that we can use to support interacting with the Dog Api via secured endpoint. We will be using the existing Dog Api and wrapping it behind our own Api. We want this new Api to use all of the industry standard best practices, unit testing, build pipelines and docker. 

We want our microservice to be designed so that the source of the dog Api, logins, logging system and di provider can be swapped out if we need to align with another organization or another business unit in the organization. 

## Data Sources
### Data Source: Dog API 

* https://dog.ceo/dog-api/ 
* https://dog.ceo/dog-api/documentation/ 

### Data Source: Logins and Auth 

* One of:
    * Json file 
    * DB file 
    * Csv file 

## Technology 

* Git 
* Dotnet 8
* FastEndpoints
* Docker 
* Azure Pipelines 
* Serilog 
* Seq
* XUnit 
    * FluentAssertions 
    * Bougus (Fake Data) 
* FluentValidation 
* IConfiguration 
    * Azure App Storage  
    * Json 
    * AppSettings 
* JWT 
* System.Text.Json 
    * All Json interactions 
    * Replaces Newtonsoft 
* Swagger 
* Split.io 

## Acceptance Criteria 
* ASP.NET API 
* In a Docker Image 
* Using Azure Pipeline for build 
* Authentication and Authorization using JWT 
* Secured Endpoints 
* Logging 
* Dependency Injection 
* Request Validation 
* Configuration 
* Unit Tests 
* Integration Tests 
* End-to-End Tests 
 
## Requirements 

* Code 
    * Live in GitHub
    * Contain readme files for each project and the entire solution to explain what is going on 
    * Use .gitignore file 
    * Use global usings
    * Have repo level code styles 
        * StyleCop 
    * Have repo level code lint 
        * SonarAnalyzer.CSharp 
    * Feature Flags 
        * Using: split.io 
    * Resources: 
        * https://dev.to/srmagura/c-linting-and-formatting-tools-in-2021-bna 
* Endpoints 
    * Auth.GenerateTokenAsync 
    * ListAllBreeds (Authentication & Authorization) 
        * Paging 
        * Searching 
    * RandomBreedImage (Authentication) 
    * RandomBreedImageByBreed (Authentication) 
        * Paging 
        * Filtering 
        * Count (x number of images) 
* API 
    * Using: FastEndpoints 
    * Developed using vertical slice architecture
    * Resources: 
        * https://fast-endpoints.com/
        * https://github.com/kylelaverty/learning-fast-endpoints
        * https://www.youtube.com/watch?v=caxS7806es0
        * https://www.youtube.com/watch?v=UkhZkK6f5Xw
* API Docs 
    * Use: Swagger 
    * Generate documentation for the endpoints 
* Request Validation 
    * Using: FluentValidation 
    * Validate incoming requests and return meaningful messages and status codes 
    * Resources: 
        * https://github.com/FluentValidation/FluentValidation  
* Auth and Auth 
    * Create a basic user storage solution 
    * SHAW256 hash of password 
    * Salt password 
    * Store secret in Azure Key Vault 
    * Try to integrate with IConfiguration 
    * Secure endpoints 
    * Most users are in the standard group, but the ListAllBreeds endpoint needs to be secured with an Admin group which a limited number of users are in 
* Configuration 
    * Using: Azure App Configuration 
    * Store things about the application like the log level 
    * Using Microsoft’s IConfiguration technology to overlay the cloud config with a local Json file to enable local building and testing 
        * This file should be excluded from the Docker image 
* Docker 
    * Site builds into an alpine (Linux) instance 
    * Runs as a dedicated user (not root) 
    * Clear out anything not needed to run service from final image layer 
    * Use .dockerignore file 
    * Resources: 
        * https://docs.docker.com/develop/develop-images/dockerfile_best-practices/
* Docker Compose
    * Create a docker-compose file to run the API and Seq
    * Resources: 
        * https://docs.docker.com/compose/
* Logging 
    * Using Serilog 
    * Structured Logging (Json) 
    * Using Seq for log management 
    * Resources: 
        * https://medium.com/@stavsofer/structured-logging-and-logs-management-asp-net-core-serilog-seq-61109f740696 
        * https://datalust.co/seq 
        * https://serilog.net/ 
* Dependency Injection 
    * Using Built in .NET Core DI 
    * Each class must not construct anything itself unless necessary 
    * Use of Interfaces 
    * Enables Unit Testing 
    * Resources: 
        * https://learn.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-8.0
* Tests 
    * Using XUnit 
    * Use Test Driver Development (TDD) for the unit tests
    * At least 75% unit test coverage 
        * Should be able to run without any external system 
    * Create Integration tests 
        * Should only use immediate system
            * Code within the bounds of the API
    * Create end-to-end tests 
        * Will interact with many external systems 
        * Run manually 
    * Resources: 
        * https://www.browserstack.com/guide/testing-pyramid-for-test-automation 
        * https://xunit.net/  
* Code Coverage 
    * Using Unit and Integration tests 
    * Formatted to show in the Azure Pipelines UI 
* Build Pipeline 
    * Azure Pipelines 
    * Outputs a docker image
    * Sets build # = Pipeline Run # 
    * Sets build configuration 
    * Code Coverage 
        * Create a code coverage report 
    * Runs 
        * PR created and each update to it 
            * Unit and integration tests 
        * Each merge to master 
            * Unit and integration tests 
        * Each night 
            * Unit and integration tests
            * End-to-end tests 