# Build stage
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app

# Copy csproj and restore dependencies
COPY *.sln .
COPY BookEcommerce.Web/*.csproj ./BookEcommerce.Web/
RUN dotnet restore

# Copy the remaining source code
COPY . .

# Build and publish the app
RUN dotnet publish BookEcommerce.Web/BookEcommerce.Web.csproj -c Release -o out

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS runtime
WORKDIR /app
COPY --from=build /app/out ./

# Set the ASP.NET Core URL
ENV ASPNETCORE_URLS=http://+:80

# Expose port 80
EXPOSE 80

# Start the application
ENTRYPOINT ["dotnet", "BookEcommerce.Web.dll"]
