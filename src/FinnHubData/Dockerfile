# Use .NET SDK for building the project
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copy only the project file to restore dependencies
COPY ["FinnHubData.API.csproj", "./"]

# Restore dependencies
RUN dotnet restore

# Copy everything and build
COPY . .  
RUN dotnet publish -c Release -o /publish  

# Use the ASP.NET Core runtime for execution
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /publish .

# Expose port 8080 (Render requires this)
EXPOSE 8080
ENV ASPNETCORE_URLS=http://+:8080

# Start the application
ENTRYPOINT ["dotnet", "FinnHubData.API.dll"]
