FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["src/Services/Notes Service/Notes.API/Notes.API.csproj", "src/Services/Notes Service/Notes.API/"]
COPY ["src/Common/MyDiary.API/MyDiary.API.csproj", "src/Common/MyDiary.API/"]
RUN dotnet restore "src/Services/Notes Service/Notes.API/Notes.API.csproj"
COPY . .
WORKDIR "/src/src/Services/Notes Service/Notes.API"
RUN dotnet build "Notes.API.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Notes.API.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Notes.API.dll"]