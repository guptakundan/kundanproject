##Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
##For more information, please see https://aka.ms/containercompat
#
#FROM microsoft/dotnet:2.2-aspnetcore-runtime-nanoserver-1803 AS base
#WORKDIR /app
#EXPOSE 80
#
#FROM microsoft/dotnet:2.2-sdk-nanoserver-1803 AS build
#WORKDIR /src
#COPY ["MyProject/MyProject.csproj", "MyProject/"]
#RUN dotnet restore "MyProject/MyProject.csproj"
#COPY . .
#WORKDIR "/src/MyProject"
#RUN dotnet build "MyProject.csproj" -c Release -o /app
#
#FROM build AS publish
#RUN dotnet publish "MyProject.csproj" -c Release -o /app
#
#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app .
#ENTRYPOINT ["dotnet", "MyProject.dll"]

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-alpine AS build
WORKDIR /app

COPY *.csproj ./
RUN dotnet restore

COPY . ./
RUN dotnet publish --configuration Release --output out

FROM mcr.microsoft.com/dotnet/core/runtime:2.2-alpine
WORKDIR /app

COPY --from=build /app/out .

ENTRYPOINT ["dotnet", "MyProject.dll"]