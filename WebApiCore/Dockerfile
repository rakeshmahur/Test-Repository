FROM microsoft/aspnetcore-build:2.0 AS build-env
WORKDIR /Build


# Copy csproj and restore as distinct layers
COPY . .
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM microsoft/aspnetcore:2.0
WORKDIR /app
COPY --from=build /build/out .

ENTRYPOINT ["dotnet", "WebApiCore.dll"]