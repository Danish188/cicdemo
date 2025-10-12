# Stage 1: Build and publish the app
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy the project file and restore dependencies
COPY ["CICDDemo.csproj", "./"]
RUN dotnet restore "CICDDemo.csproj"

# Copy the rest of the project files
COPY . .

# Publish the application to /app/publish
RUN dotnet publish "CICDDemo.csproj" -c Release -o /app/publish /p:UseAppHost=false

# Stage 2: Final runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app

# Copy published output from build stage
COPY --from=build /app/publish .

# Expose port for your web API
EXPOSE 8080

# Start the application
ENTRYPOINT ["dotnet", "CICDDemo.dll"]
