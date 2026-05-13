FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build
WORKDIR /src

COPY ["BugLoggerApi/BugLoggerApi.csproj", "BugLoggerApi/"]
RUN dotnet restore "BugLoggerApi/BugLoggerApi.csproj"

# Copy everything from the root into /src
COPY . .
WORKDIR "/src/BugLoggerApi"
RUN dotnet publish "BugLoggerApi.csproj" -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:10.0 AS final
WORKDIR /app

COPY --from=build /app/publish .

ENV ASPNETCORE_URLS=http://+:8080
EXPOSE 8080

ENTRYPOINT ["dotnet", "BugLoggerApi.dll"]