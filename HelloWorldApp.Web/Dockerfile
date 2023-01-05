FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env

WORKDIR /app
# Copy everything
COPY . ./

# Restore as distinct layerss
RUN dotnet restore 

# Build and publish a release
RUN dotnet publish -c Release -o /app/publish

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:6.0
EXPOSE 80
ARG envtype
ENV ASPNETCORE_ENVIRONMENT $envtype

WORKDIR /app
COPY --from=build-env /app/publish .
ENTRYPOINT ["dotnet", "HelloWorldApp.Web.dll"]




