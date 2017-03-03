# NLog.Extensions.AzureStorage [![AppVeyor](https://img.shields.io/appveyor/ci/JDetmar/nlog-extensions-azurestorage.svg)](https://ci.appveyor.com/project/JDetmar/nlog-extensions-azurestorage) [![NuGet](https://img.shields.io/nuget/v/NLog.Extensions.AzureStorage.svg)](https://www.nuget.org/packages/NLog.Extensions.AzureStorage/)

![logo](logo64.png?raw=true)

NLog Target for Azure Blob and Table Storage.


## Blob Configuration

### Syntax
```xml
<targets>
  <target xsi:type="AzureBlobStorage"
          name="String"
          layout="Layout"
          blobName="Layout"
          connectionString="String"
          connectionStringKey="String"
          container="Layout" />
</targets>
```


### Parameters

_name_ - Name of the target.

_layout_ - Text to be rendered. [Layout](https://github.com/NLog/NLog/wiki/Layouts) Required. 

_blobName_ - BlobName. [Layout](https://github.com/NLog/NLog/wiki/Layouts)  

_connectionString_ - Azure storage connection string. Must provide either _connectionString_ or _connectionStringKey_.

_connectionStringKey_ - App key name of Azure storage connection string. Must provide either _connectionString_ or _connectionStringKey_.

_container_ - Azure blob container name. [Layout](https://github.com/NLog/NLog/wiki/Layouts)


## Table Configuration

### Syntax
```xml
<targets>
  <target xsi:type="AzureTableStorage"
          name="String"
          layout="Layout"
          connectionString="String"
          connectionStringKey="String"
          tableName="Layout" />
</targets>
```
### Parameters

_name_ - Name of the target.

_layout_ - Text to be rendered. [Layout](https://github.com/NLog/NLog/wiki/Layouts) Required. 

_connectionString_ - Azure storage connection string. Must provide either _connectionString_ or _connectionStringKey_.

_connectionStringKey_ - App key name of Azure storage connection string. Must provide either _connectionString_ or _connectionStringKey_.

_tableName_ - Azure table name. [Layout](https://github.com/NLog/NLog/wiki/Layouts)


## Sample Configuration

```xml
<targets async="true">
    <target type="AzureBlobStorage"
            name="AzureEmulator"
            layout="${longdate:universalTime=true} ${level:uppercase=true} - ${logger}: ${message} ${exception:format=tostring:innerFormat=tostring:maxInnerExceptionLevel=1000}"
            connectionString="UseDevelopmentStorage=true;"
            container="${level}"
            blobName="${date:universalTime=true:format=yyyy-MM-dd}/${date:universalTime=true:format=HH}.log" />
    <target type="AzureBlobStorage"
            name="Azure"
            layout="${longdate:universalTime=true} ${level:uppercase=true} - ${logger}: ${message} ${exception:format=tostring:innerFormat=tostring:maxInnerExceptionLevel=1000}"
            connectionStringKey="storageConnectionString"
            container="${machinename}"
            blobName="${logger}/${date:universalTime=true:format=yy-MM-dd}/${date:universalTime=true:format=mm}.log" />
    <target type="AzureTableStorage"
            name="AzureTable"
            connectionStringKey="storageConnectionString"
            layout="${longdate:universalTime=true} ${level:uppercase=true} - ${logger}: ${message} ${exception:format=tostring:innerFormat=tostring:maxInnerExceptionLevel=1000}"
            tableName="NlogTable" />
</targets>
```
