# Build stage
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app

# Copy the solution and the UserAPI project files
COPY *.sln .
COPY BooksEcommerce.Services.UserAPI/*.csproj ./BooksEcommerce.Services.UserAPI/

# Restore dependencies
RUN dotnet restore

# Copy the remaining source code for UserAPI
COPY BooksEcommerce.Services.UserAPI/. ./BooksEcommerce.Services.UserAPI/

# Build and publish the UserAPI project
RUN dotnet publish BooksEcommerce.Services.UserAPI/BooksEcommerce.Services.UserAPI.csproj -c Release -o out

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS runtime
WORKDIR /app
COPY --from=build /app/out ./

# Set the ASP.NET Core URL
ENV ASPNETCORE_URLS=http://+:80

# Expose port 80
EXPOSE 80

# Start the UserAPI application
ENTRYPOINT ["dotnet", "BooksEcommerce.Services.UserAPI.dll"]