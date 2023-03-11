FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["PokerConnect.Backend.Api/PokerConnect.Backend.Api.csproj", "PokerConnect.Backend.Api/"]
RUN dotnet restore "PokerConnect.Backend.Api/PokerConnect.Backend.Api.csproj"
COPY . .
WORKDIR "/src/PokerConnect.Backend.Api"
RUN dotnet build "PokerConnect.Backend.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PokerConnect.Backend.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PokerConnect.Backend.Api.dll"]
