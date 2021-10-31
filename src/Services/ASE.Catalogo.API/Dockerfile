FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["src/Services/ASE.Catalogo.API/ASE.Catalogo.API.csproj", "ASE.Catalogo.API/"]
RUN dotnet restore "src/Services/ASE.Catalogo.API/ASE.Catalogo.API.csproj"
COPY . .
WORKDIR "/src/ASE.Catalogo.API"
RUN dotnet build "ASE.Catalogo.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ASE.Catalogo.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ASE.Catalogo.API.dll"]
