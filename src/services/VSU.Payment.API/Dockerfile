#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["src/services/VSU.Payment.API/VSU.Payment.API.csproj", "src/services/VSU.Payment.API/"]
RUN dotnet restore "src/services/VSU.Payment.API/VSU.Payment.API.csproj"
COPY . .
WORKDIR "/src/src/services/VSU.Payment.API"
RUN dotnet build "VSU.Payment.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "VSU.Payment.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "VSU.Payment.API.dll"]