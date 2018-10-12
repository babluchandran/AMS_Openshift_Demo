FROM microsoft/dotnet:sdk AS build-env
WORKDIR /app

# copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# copy everything else and build
COPY . ./
ADD OPLDFiles /app
RUN dotnet publish -c Release -o out

# build runtime image
FROM microsoft/dotnet:aspnetcore-runtime
WORKDIR /app
#RUN chmod -R 777 /app/Logs
#RUN chmod -R 777 /app/
#RUN sudo chmod -R ugo+rw /app/OPLDFiles
#RUN sudo chmod -R ugo+rw /app/DIALSFiles
ADD OPLDFiles /app/OPLDFiles
RUN  chmod -R ugo+rw /app/OPLDFiles
ADD DIALSFiles /app/DIALSFiles
RUN  chmod -R ugo+rw /app/DIALSFiles
RUN mkdir /app/Logs
RUN chmod -R 777 /app/Logs
#RUN mkdir /app/Archive
COPY --from=build-env /app/out .
EXPOSE 8080/tcp
ENTRYPOINT ["dotnet", "AMSDemo.dll"]
