FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Procurement_AzureCodeProject_Weather/Procurement_AzureCodeProject_Weather.csproj", "Procurement_AzureCodeProject_Weather/"]
RUN dotnet restore "Procurement_AzureCodeProject_Weather/Procurement_AzureCodeProject_Weather.csproj"
COPY . .
WORKDIR "/src/Procurement_AzureCodeProject_Weather"
RUN dotnet build "Procurement_AzureCodeProject_Weather.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Procurement_AzureCodeProject_Weather.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Procurement_AzureCodeProject_Weather.dll"]
