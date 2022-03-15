FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["HotelListing/HotelListing.csproj", "HotelListing/"]
RUN dotnet restore "HotelListing/HotelListing.csproj"
COPY . .
WORKDIR "/src/HotelListing"
RUN dotnet build "HotelListing.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "HotelListing.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HotelListing.dll"]
