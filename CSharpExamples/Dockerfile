FROM mcr.microsoft.com/dotnet/runtime:7.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["CSharpExamples/CSharpExamples.csproj", "CSharpExamples/"]
RUN dotnet restore "CSharpExamples/CSharpExamples.csproj"
COPY . .
WORKDIR "/src/CSharpExamples"
RUN dotnet build "CSharpExamples.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CSharpExamples.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CSharpExamples.dll"]
