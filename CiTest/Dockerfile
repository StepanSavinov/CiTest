FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["CiTest/CiTest.csproj", "CiTest/"]
RUN dotnet restore "CiTest/CiTest.csproj"
COPY . .
WORKDIR "/src/CiTest"
RUN dotnet build "CiTest.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CiTest.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CiTest.dll"]
