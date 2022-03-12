#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["SuperHero.WebApi/SuperHero.WebApi.csproj", "SuperHero.WebApi/"]
RUN dotnet restore "SuperHero.WebApi/SuperHero.WebApi.csproj"
COPY . .
WORKDIR "/src/SuperHero.WebApi"
RUN dotnet build "SuperHero.WebApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SuperHero.WebApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SuperHero.WebApi.dll"]