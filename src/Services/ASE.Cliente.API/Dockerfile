FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["src/Services/ASE.Cliente.API/ASE.Cliente.API.csproj", "ASE.Cliente.API/"]
RUN dotnet restore "src/Services/ASE.Cliente.API/ASE.Cliente.API.csproj"
COPY . .
WORKDIR "/src/ASE.Cliente.API"
RUN dotnet build "ASE.Cliente.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ASE.Cliente.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ASE.Cliente.API.dll"]
