FROM mcr.microsoft.com/dotnet/aspnet:6.0-alpine AS base
WORKDIR /App
EXPOSE 8080

ENV ASPNETCORE_URLS=http://*:8080

FROM mcr.microsoft.com/dotnet/sdk:6.0-alpine as build
WORKDIR /src
COPY . .

RUN dotnet restore "./zaliczenie.csproj"
COPY . .
WORKDIR /src/.
RUN dotnet build "zaliczenie.csproj" -c Release -o /App

FROM build AS publish
RUN dotnet publish "zaliczenie.csproj" -c Release -o /App

FROM base AS final
WORKDIR /App
COPY --from=publish /App .
ENTRYPOINT ["dotnet", "zaliczenie.dll"]