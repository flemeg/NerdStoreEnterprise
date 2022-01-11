#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["src/services/NES.Carrinho.API/NES.Carrinho.API.csproj", "src/services/NES.Carrinho.API/"]
RUN dotnet restore "src/services/NES.Carrinho.API/NES.Carrinho.API.csproj"
COPY . .
WORKDIR "/src/src/services/NES.Carrinho.API"
RUN dotnet build "NES.Carrinho.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "NES.Carrinho.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "NES.Carrinho.API.dll"]