FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["Docker22Test/Docker22Test.csproj", "Docker22Test/"]
RUN dotnet restore "Docker22Test/Docker22Test.csproj"
COPY . .
WORKDIR "/src/Docker22Test"
RUN dotnet build "Docker22Test.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Docker22Test.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Docker22Test.dll"]