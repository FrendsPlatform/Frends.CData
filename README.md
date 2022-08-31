 - [Frends.CData](#frends.sql)
   - [Installing](#installing)
   - [Contributing](#contributing)
   - [Documentation](#documentation)
     - [CData.ExecuteQuery](#cdataexecutequery) 
     - [CData.ExecuteProcedure](#cdataexecuteprocedure) 
     - [CData.BatchOperation](#cdatabatchoperation) 
     - [List of supported CData drivers](#list-of-cdata-drivers-with-a-task-implementation)
   - [License](#license)

# Frends.CData
FRENDS CData Tasks provide a way of querying different services with SQL queries utilizing the drivers made by [CData Software](https://www.cdata.com/)

## Installing
FRENDS CData Tasks are currently distributed separately as they are purchased and delivered separately from the frends platform, please contact sales@frends.com

## Contributing
It is not possible to contribute to the Frends CData Tasks

## Documentation

The CData Tasks act as a thin layer between the ADO.NET provider [drivers provided by CData](https://www.cdata.com/drivers/). Individual documentation for a single CData driver can be found on their [online help files](http://cdn.cdata.com/help/)

All CData Task libraries are created from the same template and share the same structure with three Tasks:

* ExecuteQuery
* BatchOperation
* ExecuteProcedure

Different drivers may have some limitations regarding what operations are possible. Also it should be noted that extensive testing by the frends team has not been done for all of the Tasks because of the sheer amount of CData drivers available.

### CData.ExecuteQuery
#### Input 
| Property          | Type                              | Description                                             | Example                                   |
|-------------------|-----------------------------------|---------------------------------------------------------|-------------------------------------------|
| Query             | string                            | The query that will be executed to the database.        | `select Name,Age from MyTable where AGE = @Age` 
| Parameters        | Array{Name: string, Value: string} | A array of parameters to be appended to the query.     | `Name = Age, Value = 42`
| Connection String | string                            | Connection String to be used to connect to the database.| `Server=myServerAddress;Database=myDataBase;User Id=myUsername;Password=myPassword;`


#### Options
| Property               | Type                 | Description                                                |
|------------------------|----------------------|------------------------------------------------------------|
| Command Timeout        | int                  | Timeout in seconds to be used for the query. 60 seconds by default. |
| Sql Transaction Isolation Level | SqlTransationIsolationLevel | Transactions specify an isolation level that defines the degree to which one transaction must be isolated from resource or data modifications made by other transactions. Possible values are: Default, None, Serializable, ReadUncommitted, ReadCommitted, RepeatableRead, Snapshot. Additional documentation https://msdn.microsoft.com/en-us/library/ms378149(v=sql.110).aspx |

#### Result
JToken. JObject[]

Example result
```
[ 
 {
  "Name": "Foo",
  "Age": 42
 },
 {
  "Name": "Adam",
  "Age": 42
 }
]
```
```
The second name 'Adam' can be now be accessed by #result[1].Name in the process parameter editor.

```


### CData.ExecuteProcedure
#### Input
| Property          | Type                              | Description                                             | Example                                   |
|-------------------|-----------------------------------|---------------------------------------------------------|-------------------------------------------|
| Execute           | string                            | The stored procedure that will be executed.             | `SpGetResultsByAge @Age` 
| Parameters        | Array{Name: string, Value: string} | A array of parameters to be appended to the query.     | `Name = Age, Value = 42`
| Connection String | string                            | Connection String to be used to connect to the database.| `Server=myServerAddress;Database=myDataBase;User Id=myUsername;Password=myPassword;`

#### Options
| Property               | Type                 | Description                                                |
|------------------------|----------------------|------------------------------------------------------------|
| Command Timeout        | int                  | Timeout in seconds to be used for the query. 60 seconds by default. |
| Sql Transaction Isolation Level | SqlTransationIsolationLevel | Transactions specify an isolation level that defines the degree to which one transaction must be isolated from resource or data modifications made by other transactions. Possible values are: Default, None, Serializable, ReadUncommitted, ReadCommitted, RepeatableRead, Snapshot. Additional documentation https://msdn.microsoft.com/en-us/library/ms378149(v=sql.110).aspx |

#### Result
JToken. JObject[]

Example result
```
[ 
 {
  "Name": "Foo",
  "Age": 42
 },
 {
  "Name": "Adam",
  "Age": 42
 }
]
```
```
The second name 'Adam' can be now be accessed by #result[1].Name in the process parameter editor.

```

### CData.BatchOperation
#### Input
| Property          | Type                              | Description                                             | Example                                   |
|-------------------|-----------------------------------|---------------------------------------------------------|-------------------------------------------|
| Query             | string                            | The query that will be executed to the database.        | `insert into MyTable(ID,NAME) VALUES (@Id, @FirstName)` 
| Input Json        | string                            | A Json Array of objects that has their properties mapped to the parameters in the Query      | `[{"Id":10, "FirstName": "Foo"},{"Id":15, "FirstName": "Bar"}]`
| Connection String | string                            | Connection String to be used to connect to the database.| `Server=myServerAddress;Database=myDataBase;User Id=myUsername;Password=myPassword;`


#### Options
| Property               | Type                 | Description                                                |
|------------------------|----------------------|------------------------------------------------------------|
| Command Timeout Seconds       | int                  | Timeout in seconds to be used for the query. 60 seconds by default. |
| Sql Transaction Isolation Level | SqlTransationIsolationLevel | Transactions specify an isolation level that defines the degree to which one transaction must be isolated from resource or data modifications made by other transactions. Possible values are: Default, None, Serializable, ReadUncommitted, ReadCommitted, RepeatableRead, Snapshot. Additional documentation https://msdn.microsoft.com/en-us/library/ms378149(v=sql.110).aspx | 

#### Result
Integer - Number of affected rows

#### Example usage
![BatchOperationExample.png](/batchoperation-example.png)

## List of CData drivers with a Task implementation

* AAS
* Access
* ActCRM
* ActiveDirectory
* ActOn
* Acumatica
* ADLS
* AdobeAnalytics
* ADP
* Airtable
* Alfresco
* AmazonAthena
* AmazonDynamoDB
* AmazonMarketplace
* AmazonS3
* ApacheCouchDB
* ApacheHBase
* ApacheHive
* ApacheImpala
* ApacheKafka
* ApachePhoenix
* API
* Asana
* AuthorizeNet
* Autify
* Avalara
* Avro
* AWSCostExplorer
* AzureDataCatalog
* AzureDevOps
* AzureResourceManagement
* AzureSynapse
* AzureTables
* Basecamp
* BigCommerce
* Bing
* BingAds
* Box
* Btrieve
* Bugzilla
* BullhornCRM
* Cassandra
* CDS
* Cloudant
* CockroachDB
* Confluence
* CosmosDB
* Couchbase
* CSV
* D365BusinessCentral
* D365FinOp
* D365Sales
* Databricks
* DataRobot
* DB2
* DigitalOcean
* DocuSign
* Domino
* Dropbox
* DynamicsCRM
* DynamicsGP
* DynamicsNAV
* Ebay
* EbayAnalytics
* EdgarOnline
* Elasticsearch
* Email
* EnterpriseDB
* EpicorERP
* Evernote
* ExactOnline
* Excel
* ExcelOnline
* ExcelServices
* Exchange
* Facebook
* FacebookAds
* FedEx
* FinancialEdgeNXT
* FinancialForce
* FreshBooks
* FreshDesk
* FTP
* GitHub
* Gmail
* GoogleAds
* GoogleAdsManager
* GoogleAnalytics
* GoogleBigQuery
* GoogleCalendar
* GoogleCloudStorage
* GoogleCM
* GoogleContacts
* GoogleDataCatalog
* GoogleDirectory
* GoogleDrive
* GoogleSearch
* GoogleSheets
* GoogleSpanner
* GraphQL
* Greenplum
* HDFS
* Highrise
* HPCC
* HubSpot
* IBMCloudObjectStorage
* IBMCloudSQLQuery
* Informix
* Instagram
* JIRA
* JiraServiceDesk
* JSON
* Kintone
* LDAP
* LinkedIn
* LinkedInAds
* Magento
* MailChimp
* MariaDB
* Marketo
* MarkLogic
* MicrosoftPlanner
* MicrosoftProject
* MongoDB
* MSTeams
* MYOB
* MySQL
* NetSuite
* OData
* Odoo
* Office365
* OneDrive
* OneNote
* OpenExchangeRates
* OracleEloqua
* OracleOci
* OracleSalesCloud
* Parquet
* Paylocity
* PayPal
* Pinterest
* PostgreSQL
* PowerBIXMLA
* Presto
* Quandl
* QuickBase
* QuickBooks
* QuickBooksOnline
* QuickBooksPOS
* RaiserEdgeNXT
* Reckon
* Redis
* Redshift
* REST
* RSS
* Sage50UK
* Sage200
* Sage300
* SageBCAccounting
* SageIntacct
* Salesforce
* SalesforceChatter
* SalesforcePardot
* SAPBusinessObjectsBI
* SAPBusinessOne
* SAPBusinessOneDI
* SAPByDesign
* SAPConcur
* SAPERP
* SAPFieldglass
* SAPGateway
* SAPHANA
* SAPHanaXSA
* SAPHybrisC4C
* SAPSuccessFactors
* SASDataSets
* SASXpt
* SendGrid
* ServiceNow
* SFMarketingCloud
* SFTP
* SharePoint
* ShipStation
* Shopify
* SingleStore
* Slack
* Smartsheet
* SnapchatAds
* Snowflake
* SparkSQL
* Splunk
* Square
* SSAS
* Streak
* Stripe
* SugarCRM
* SuiteCRM
* SurveyMonkey
* Sybase
* SybaseIQ
* TableauCRM
* Tally
* TaxJar
* Teradata
* Trello
* TSheets
* Twilio
* Twitter
* TwitterAds
* UPS
* USPS
* VeevaVault
* Wasabi
* WaveFinancial
* WooCommerce
* WordPress
* Workday
* xBase
* XCart
* Xero
* XeroWorkflowMax
* XML
* YouTubeAnalytics
* Zendesk
* ZohoBooks
* ZohoCRM
* Zuora

## License

This project is licensed under the MIT License - see the LICENSE file for details
