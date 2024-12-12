Serilog log to an SQL database.
Serilog supports many database but in this sample we will use MS Sql server.
#### How To:
- First, nuget install **Serilog.Sinks.MSSqlServer**.
###### Database
The database to sink the log must be separate and not the same as the one the app uses
- click on view tab and click on sql server object explorer.
- open the sql server and right-click on the database folder, and add new database.
- To get the connection string: right click on the created database, click properties, and copy connection string.
###### Then in appsettings register the sink:
```json
"Serilog": {
	"Using": [
		"Serilog.Sinks.MSSqlServer"
	],
	"MinimumLevel": "LogLevel", //dont forget to change this
	"WriteTo": [
		{
			"Name": "MSSqlServer",
			"Args": {
				"connectionString": "Data Source=...", //database connection string
				"tableName": "logs",
				"autoCreateSqlTable":  true 
					//autoCreateSqlTable will automatically create the "logs" table in the database-
					//and automatically populate it with columns and rows whenever a log is made
			}
		}
	]
}
```
