FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["WebApplicationOpenShiftTest/WebApplicationOpenShiftTest.csproj", "WebApplicationOpenShiftTest/"]
RUN dotnet restore "WebApplicationOpenShiftTest/WebApplicationOpenShiftTest.csproj"
COPY . .
WORKDIR "/src/WebApplicationOpenShiftTest"
RUN dotnet build "WebApplicationOpenShiftTest.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "WebApplicationOpenShiftTest.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApplicationOpenShiftTest.dll"]