FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Static-api/Static-api.csproj", "Static-api/"]
RUN dotnet restore "Static-api/Static-api.csproj"
COPY . .
WORKDIR "/src/Static-api"
RUN dotnet build "Static-api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Static-api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Static-api.dll"]
