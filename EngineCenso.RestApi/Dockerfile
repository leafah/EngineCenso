FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY EngineCenso.RestApi/EngineCenso.RestApi.csproj EngineCenso.RestApi/
RUN dotnet restore EngineCenso.RestApi/EngineCenso.RestApi.csproj
COPY . .
WORKDIR /src/EngineCenso.RestApi
RUN dotnet build EngineCenso.RestApi.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish EngineCenso.RestApi.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "EngineCenso.RestApi.dll"]
