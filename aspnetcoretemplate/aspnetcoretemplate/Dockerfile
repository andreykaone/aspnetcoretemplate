FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 50511

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["aspnetcoretemplate.csproj", "aspnetcoretemplate/"]
RUN dotnet restore "aspnetcoretemplate/aspnetcoretemplate.csproj"
COPY . .
WORKDIR "/src/aspnetcoretemplate"
RUN dotnet build "aspnetcoretemplate.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "aspnetcoretemplate.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "aspnetcoretemplate.dll"]