# Use the official ASP.NET Core runtime as a parent image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
 
# Use the SDK image to build the app
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["MicroServiceB.csproj", "./"]
RUN dotnet restore "./MicroServiceB.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "MicroServiceB.csproj" -c Release -o /app/build
 
FROM build AS publish
RUN dotnet publish "MicroServiceB.csproj" -c Release -o /app/publish
 
# Use the runtime image to run the app
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MicroServiceB.dll"]