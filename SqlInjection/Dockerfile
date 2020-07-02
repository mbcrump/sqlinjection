FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-stretch-slim AS base
WORKDIR /app
EXPOSE 5000

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-stretch AS build
WORKDIR /src
COPY ["SqlInjection/SqlInjection.csproj", "SqlInjection/"]
RUN dotnet restore "SqlInjection/SqlInjection.csproj"
COPY . .
WORKDIR "/src/SqlInjection"
RUN dotnet build "SqlInjection.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "SqlInjection.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "SqlInjection.dll"]
