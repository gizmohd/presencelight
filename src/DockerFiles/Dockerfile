FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /source

# copy everything else and build app
COPY PresenceLight.Worker/. ./PresenceLight.Worker/
COPY PresenceLight.Core/. ./PresenceLight.Core/
WORKDIR /source/PresenceLight.Worker
RUN dotnet publish -c release -o /app

# final stage/image
FROM mcr.microsoft.com/dotnet/aspnet:5.0
EXPOSE 5000
EXPOSE 5001
WORKDIR /app
COPY --from=build /app ./
LABEL org.opencontainers.image.source=https://github.com/isaacrlevin/presencelight
ENTRYPOINT ["dotnet", "PresenceLight.dll"]
