#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["BlazorInputFileBug/BlazorInputFileBug.csproj", "BlazorInputFileBug/"]
RUN dotnet restore "BlazorInputFileBug/BlazorInputFileBug.csproj"
COPY . .
WORKDIR "/src/BlazorInputFileBug"
RUN dotnet build "BlazorInputFileBug.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BlazorInputFileBug.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BlazorInputFileBug.dll"]