FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["MyMemeGallery/MyMemeGallery.csproj", "MyMemeGallery/"]
RUN dotnet restore "MyMemeGallery/MyMemeGallery.csproj"
COPY . .
WORKDIR "/src/MyMemeGallery"
RUN dotnet build "MyMemeGallery.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MyMemeGallery.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MyMemeGallery.dll"]
