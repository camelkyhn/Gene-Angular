FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Gene.API/Gene.API.csproj", "Gene.API/"]
RUN dotnet restore "Gene.API/Gene.API.csproj"
COPY . .
WORKDIR "/src/Gene.API"
RUN dotnet build "Gene.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Gene.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Gene.API.dll"]
