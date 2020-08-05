FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY WebApp_Core_docker/WebApp_Core_docker.csproj WebApp_Core_docker/
RUN dotnet restore WebApp_Core_docker/WebApp_Core_docker.csproj
COPY . .
WORKDIR /src/WebApp_Core_docker
RUN dotnet build WebApp_Core_docker.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish WebApp_Core_docker.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApp_Core_docker.dll"]
