FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["tictactoev2/tictactoev2.csproj", "tictactoev2/"]
RUN dotnet restore "tictactoev2/tictactoev2.csproj"
COPY . .
WORKDIR "/src/tictactoev2"
RUN dotnet build "tictactoev2.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "tictactoev2.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "tictactoev2.dll"]
