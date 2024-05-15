#FROM msimons/aspnetcore-build AS build
#WORKDIR /code 
#COPY . . 
#RUN dotnet restore 
#RUN dotnet publish --output /output --configuration Release

#FROM mcr.microsoft.com/dotnet/aspnet 
#COPY --from=build /output /app
#WORKDIR /app
#ENTRYPOINT [ "dotnet", "AspCoreOnDocker.dll" ]

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build-env
WORKDIR /App

# Copy everything
COPY . ./
# Restore as distinct layers
RUN dotnet restore
# Build and publish a release
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /App
COPY --from=build-env /App/out .
ENTRYPOINT ["dotnet", "AspCoreOnDocker.dll"]