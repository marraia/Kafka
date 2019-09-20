FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["Kafka.Producer.API/Kafka.Producer.API.csproj", "Kafka.Producer.API/"]
RUN dotnet restore "Kafka.Producer.API/Kafka.Producer.API.csproj"
COPY . .
WORKDIR "/src/Kafka.Producer.API"
RUN dotnet build "Kafka.Producer.API.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Kafka.Producer.API.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Kafka.Producer.API.dll"]