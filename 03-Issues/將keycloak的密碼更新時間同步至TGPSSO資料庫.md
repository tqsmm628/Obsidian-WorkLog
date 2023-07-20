---
url: https://gitlab.transportdata.tw/gdb/sso/etl/backstage/-/issues/4
project: gdb/sso/etl/backstage
status: doing
type: gdb
---
#issue 
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
	- appsettings設定NLog
		```json
		"NLog": {
		    "autoReload": "false",
		    "throwExceptions": "true",
		    "internalLogLevel": "Off",
		    "extensions": {
		      "NLog.Extensions.Logging": {
		        "assembly": "NLog.Extensions.Logging"
		      }
		    },
		    "variables": {
		      "LogFileBasePath": "${basedir}/logs"
		    },
		    "targets": {
		      "UDP_Sender": {
		        "type": "Network",
		        "encoding": "utf-8",
		        "address": "udp://192.168.50.57:5043",
		        "layout": "${event-properties:item=JsonMessage}"
		      }
		    },
		    "rules": [
		      {
		        "logger": "*",
		        "levels": "Trace,Debug,Info,Warn,Error,Fatal",
		        "writeTo": "UDP_Sender"
		      }
		    ]
		  }
		```
	- Log的Model要繼承 InfraLogData
	- LoggerHelper的CreateLogger的LogType用自定義。
