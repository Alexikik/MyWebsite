FROM mcr.microsoft.com/dotnet/sdk:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Server/MyWebsite.Server.csproj", "Server/"]
RUN dotnet restore "Server/MyWebsite.Server.csproj"
COPY . .
WORKDIR "/src/Server"
RUN dotnet build "MyWebsite.Server.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MyWebsite.Server.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MyWebsite.Server.dll"]
