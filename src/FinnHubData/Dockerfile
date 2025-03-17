# Use official .NET SDK image for building the project
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copy project files and restore dependencies
COPY *.sln ./
COPY src/FinnHubData/*.csproj ./src/FinnHubData/
RUN dotnet restore ./src/FinnHubData/FinnHubData.API.csproj

# Copy the rest of the application and build it
COPY . .
RUN dotnet publish ./src/FinnHubData/FinnHubData.API.csproj -c Release -o /publish

# Use the official ASP.NET Core runtime image for execution
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /publish .

# Expose port 8080 (Render runs containers on 8080)
EXPOSE 8080
ENV ASPNETCORE_URLS=http://+:8080

# Start the application
ENTRYPOINT ["dotnet", "FinnHubData.API.dll"]
