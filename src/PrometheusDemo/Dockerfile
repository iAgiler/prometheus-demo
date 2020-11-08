#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM registry.cn-shanghai.aliyuncs.com/samzhang/mcr-dotnet-core-aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM registry.cn-shanghai.aliyuncs.com/samzhang/mcr-dotnet-core-sdk:3.1-buster AS build
WORKDIR /src
COPY ["PrometheusDemo.csproj", ""]
RUN dotnet restore "./PrometheusDemo.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "PrometheusDemo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PrometheusDemo.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PrometheusDemo.dll"]