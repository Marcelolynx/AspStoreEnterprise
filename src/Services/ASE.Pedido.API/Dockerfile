FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["src/Services/ASE.Pedido.API/ASE.Pedido.API.csproj", "ASE.Pedido.API/"]
RUN dotnet restore "src/Services/ASE.Pedido.API/ASE.Pedido.API.csproj"
COPY . .
WORKDIR "/src/ASE.Pedido.API"
RUN dotnet build "ASE.Pedido.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ASE.Pedido.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ASE.Pedido.API.dll"]
