FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["NDMS/NDMS.csproj", "NDMS/"]
RUN dotnet restore "NDMS/NDMS.csproj"
COPY . .
WORKDIR "/src/NDMS"
RUN dotnet build "NDMS.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "NDMS.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "NDMS.dll"]