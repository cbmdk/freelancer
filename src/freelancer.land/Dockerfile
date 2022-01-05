#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["freelancer.land/freelancer.land.csproj", "freelancer.land/"]
RUN dotnet restore "freelancer.land/freelancer.land.csproj"
COPY . .
WORKDIR "/src/freelancer.land"
RUN dotnet build "freelancer.land.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "freelancer.land.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "freelancer.land.dll"]