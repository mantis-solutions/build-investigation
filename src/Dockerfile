FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build-dotnet
    WORKDIR /dotnet-builds

    #needed for TC output to be formed. Name does not matter but it should be set
    ENV TEAMCITY_PROJECT_NAME=QuickStartApp

    # get all sources into image and restore nuget packages
    COPY src/ .
    RUN dotnet restore

    # build and publish 
    RUN dotnet publish web/QuickStartApp.csproj -c Release -o ./.publish
    

# Create the runtime image.
FROM mcr.microsoft.com/dotnet/aspnet:8.0-alpine AS runtime
    COPY --from=build-dotnet /dotnet-builds/.publish ./

    ENTRYPOINT ["dotnet", "QuickStartApp.dll"]
