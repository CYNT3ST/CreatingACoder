#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["CreatingACoder/CreatingACoder.csproj", "CreatingACoder/"]
RUN dotnet restore "CreatingACoder/CreatingACoder.csproj"
COPY . .
WORKDIR "/src/CreatingACoder"
RUN dotnet build "CreatingACoder.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CreatingACoder.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CreatingACoder.dll"]