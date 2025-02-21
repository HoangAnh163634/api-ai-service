FROM mcr.microsoft.com/dotnet/aspnet:8.0-preview AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:8.0-preview AS build
WORKDIR /src
COPY ["api-ai-service/api-ai-service.csproj", "./"]
RUN dotnet restore "api-ai-service.csproj"

COPY api-ai-service/ .  
RUN dotnet build "api-ai-service.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "api-ai-service.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "api-ai-service.dll"]
