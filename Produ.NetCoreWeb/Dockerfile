FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["Produ.NetCoreWeb/Produ.NetCoreWeb.csproj", "Produ.NetCoreWeb/"]
RUN dotnet restore "Produ.NetCoreWeb/Produ.NetCoreWeb.csproj"
COPY . .
WORKDIR "/src/Produ.NetCoreWeb"
RUN dotnet build "Produ.NetCoreWeb.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Produ.NetCoreWeb.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Produ.NetCoreWeb.dll"]