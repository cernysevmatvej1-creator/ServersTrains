# Базовый образ для сборки
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src

# Копируем файл проекта
COPY TraniServer/TraniServer.csproj TraniServer/
RUN dotnet restore "TraniServer/TraniServer.csproj"

# Копируем все остальные файлыDSASD
COPY TraniServer/. TraniServer/
WORKDIR /src/TraniServer
RUN dotnet publish -c Release -o /app/publish

# Финальный образ
FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS final
WORKDIR /app
EXPOSE 80
EXPOSE 443
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "TraniServer.dll"]