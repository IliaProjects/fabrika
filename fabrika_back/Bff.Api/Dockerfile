FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src

COPY ["Bff.Api/Bff.Api.csproj", "Bff.Api/"]
COPY ["Bff.Core/Bff.Core.csproj", "Bff.Core/"]
RUN dotnet restore "Bff.Api/Bff.Api.csproj"

COPY . .
WORKDIR /src/Bff.Api
RUN dotnet publish "Bff.Api.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS final
WORKDIR /app
ENV ASPNETCORE_URLS=http://+:8080
EXPOSE 8080
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "Bff.Api.dll"]
