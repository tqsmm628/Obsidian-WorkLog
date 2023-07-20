---
url: https://gitlab.transportdata.tw/gdb/sso/etl/backstage/-/issues/4
---
#issue #doing #gdb
# [[2023-07-19]]

還差 logstash

# [[2023-07-20]]

- 使用東霖寫的元件，將資料透過[[NLog]]傳送到[[Logstash]]
	- 元件
		- [[InfraStack.Log]]
		- [[InfraStack.Log.Nlog]]
	- Startup注入
```csharp
LogManager.Configuration = new NLogLoggingConfiguration(Configuration.GetSection("NLog"));
services.AddSingleton<IInfraLogger, LoggerNLog>();
```
