FROM nginx AS base
EXPOSE 6495
EXPOSE 3574

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["ProyectoDummy.csproj", "/"]
RUN dotnet restore "/ProyectoDummy.csproj"

COPY . .
WORKDIR "/src"
RUN dotnet build "ProyectoDummy.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ProyectoDummy.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM  base AS final
WORKDIR /usr/share/nginx/html
COPY --from=publish /app/publish/wwwroot .
COPY  /nginx.conf /etc/nginx/nginx.conf