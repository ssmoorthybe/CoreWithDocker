FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["CoreWithDocker/CoreWithDocker.csproj", "CoreWithDocker/"]
RUN dotnet restore "CoreWithDocker/CoreWithDocker.csproj"
COPY . .
WORKDIR "/src/CoreWithDocker"
RUN dotnet build "CoreWithDocker.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "CoreWithDocker.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CoreWithDocker.dll"]