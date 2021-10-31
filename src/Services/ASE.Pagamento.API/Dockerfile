FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["src/Services/ASE.Pagamento.API/ASE.Pagamento.API.csproj", "ASE.Pagamento.API/"]
RUN dotnet restore "src/Services/ASE.Pagamento.API/ASE.Pagamento.API.csproj"
COPY . .
WORKDIR "/src/ASE.Pagamento.API"
RUN dotnet build "ASE.Pagamento.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ASE.Pagamento.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ASE.Pagamento.API.dll"]
