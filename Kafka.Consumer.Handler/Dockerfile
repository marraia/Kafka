FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["Kafka.Consumer.Handler/Kafka.Consumer.Handler.csproj", "Kafka.Consumer.Handler/"]
RUN dotnet restore "Kafka.Consumer.Handler/Kafka.Consumer.Handler.csproj"
COPY . .
WORKDIR "/src/Kafka.Consumer.Handler"
RUN dotnet build "Kafka.Consumer.Handler.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Kafka.Consumer.Handler.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Kafka.Consumer.Handler.dll"]