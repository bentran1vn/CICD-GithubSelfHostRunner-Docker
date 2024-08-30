FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
USER $APP_UID
WORKDIR /app
EXPOSE 8080

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["CICD-DockerRunner.API/CICD-DockerRunner.API.csproj", "CICD-DockerRunner.API/"]
RUN dotnet restore "CICD-DockerRunner.API/CICD-DockerRunner.API.csproj"
COPY . .
WORKDIR "/src/CICD-DockerRunner.API"
RUN dotnet build "CICD-DockerRunner.API.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "CICD-DockerRunner.API.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CICD-DockerRunner.API.dll"]
