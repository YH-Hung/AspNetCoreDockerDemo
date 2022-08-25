FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY *.fsproj ./
RUN dotnet restore "DockerSwitch.RestApi.fsproj"
COPY . .
RUN dotnet build "DockerSwitch.RestApi.fsproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DockerSwitch.RestApi.fsproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DockerSwitch.RestApi.dll"]
