FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["src/Services/ASE.Carrinho.Api/ASE.Carrinho.Api.csproj", "ASE.Carrinho.Api/"]
RUN dotnet restore "src/Services/ASE.Carrinho.Api/ASE.Carrinho.Api.csproj"
COPY . .
WORKDIR "/src/ASE.Carrinho.Api"
RUN dotnet build "ASE.Carrinho.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ASE.Carrinho.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ASE.Carrinho.Api.dll"]
