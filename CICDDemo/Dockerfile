# Stage 1: Build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy the project file and restore dependencies
COPY ["CICDDemo/CICDDemo.csproj", "CICDDemo/"]
RUN dotnet restore "CICDDemo/CICDDemo.csproj"

# Copy everything else and build
COPY . .
WORKDIR "/src/CICDDemo"
RUN dotnet build "CICDDemo.csproj" -c Release -o /app/build

# Publish
FROM build AS publish
RUN dotnet publish "CICDDemo.csproj" -c Release -o /app/publish /p:UseAppHost=false

# Final image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CICDDemo.dll"]
