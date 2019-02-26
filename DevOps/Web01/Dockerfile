FROM microsoft/dotnet:2.1-aspnetcore-runtime-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk-stretch AS build
WORKDIR /src
COPY ["Web01/Web01.csproj", "Web01/"]
RUN dotnet restore "Web01/Web01.csproj"
COPY . .
WORKDIR "/src/Web01"
RUN dotnet build "Web01.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Web01.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Web01.dll"]