FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["corepg/corepg.csproj", "corepg/"]
RUN dotnet restore "corepg/corepg.csproj"
COPY . .
WORKDIR "/src/corepg"
RUN dotnet build "corepg.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "corepg.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "corepg.dll"]