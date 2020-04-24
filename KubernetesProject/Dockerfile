FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["KubernetesProject/KubernetesProject.csproj", "KubernetesProject/"]

RUN dotnet restore "KubernetesProject/KubernetesProject.csproj"
COPY . .
WORKDIR "/src/KubernetesProject"
RUN dotnet build "KubernetesProject.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "KubernetesProject.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "KubernetesProject.dll"]