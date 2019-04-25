FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["HelloWorldContainerDemo/HelloWorldService/HelloWorldService.csproj", "HelloWorldContainerDemo/HelloWorldService/"]
RUN dotnet restore "HelloWorldContainerDemo/HelloWorldService/HelloWorldService.csproj"
COPY . .
WORKDIR "/src/HelloWorldContainerDemo/HelloWorldService"
RUN dotnet build "HelloWorldService.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "HelloWorldService.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "HelloWorldService.dll"]