#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["src/services/VSU.Catalogue.API/VSU.Catalogue.API.csproj", "src/services/VSU.Catalogue.API/"]
RUN dotnet restore "src/services/VSU.Catalogue.API/VSU.Catalogue.API.csproj"
COPY . .
WORKDIR "/src/src/services/VSU.Catalogue.API"
RUN dotnet build "VSU.Catalogue.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "VSU.Catalogue.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "VSU.Catalogue.API.dll"]