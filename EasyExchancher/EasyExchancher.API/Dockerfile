#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["EasyExchancher.API/EasyExchancher.API.csproj", "EasyExchancher.API/"]
RUN dotnet restore "EasyExchancher.API/EasyExchancher.API.csproj"
COPY . .
WORKDIR "/src/EasyExchancher.API"
RUN dotnet build "EasyExchancher.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "EasyExchancher.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "EasyExchancher.API.dll"]