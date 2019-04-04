FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["testapp/testapp.csproj", "testapp/"]
RUN dotnet restore "testapp/testapp.csproj"
COPY . .
WORKDIR "/src/testapp"
RUN dotnet build "testapp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "testapp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "testapp.dll"]