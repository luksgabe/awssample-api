FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["./AwsApiSample.Api.csproj", "AwsApiSample.Api/"]
RUN dotnet restore "AwsApiSample.Api/AwsApiSample.Api.csproj"
COPY . .
WORKDIR "/src/AwsApiSample.Api"
RUN dotnet build "AwsApiSample.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AwsApiSample.Api.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AwsApiSample.Api.dll"]
