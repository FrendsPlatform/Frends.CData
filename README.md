 - [Frends.CData](#frends.sql)
   - [Installing](#installing)
   - [Contributing](#contributing)
   - [Documentation](#documentation)
     - [CData.ExecuteQuery](#sqlexecutequery) 
     - [CData.ExecuteProcedure](#sqlexecuteprocedure) 
     - [CData.BulkInsert](#sqlbulkinsert)
     - [CData.BatchOperation](#sqlbatchoperation) 
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
![BatchOperationExample.png](https://cloud.githubusercontent.com/assets/6636662/26483905/
3bb0d73c-41f8-11e7-95c9-fe554898f97f.png)

## List of CData drivers with a Task implementation

* AAS
* Access
* ActCRM
* ActiveDirectory
* ActOn
* Acumatica
* ADLS
* AdobeAnalytics
* Airtable
* Alfresco
* AmazonAthena
* AmazonDynamoDB
* AmazonMarketplace
* AmazonS3
* Anzo
* ApacheHBase
* ApacheHive
* ApacheImpala
* ApacheKafka
* ApachePhoenix
* API
* Asana
* AuthorizeNet
* Avalara
* AWSDataManagement
* AzureBlobDestination
* AzureDataCatalog
* AzureDataLakeStoreDestination
* AzureDataManagement
* AzureTables
* Base
* Basecamp
* BigCommerce
* Bing
* BingAds
* Box
* Btrieve
* Bugzilla
* BullhornCRM
* Businessbridge
* Cassandra
* CDS
* Cloudant
* CloudSign
* CockroachDB
* Confluence
* CosmosDB
* D365BusinessCentral
* D365FinOp
* D365Sales
* DataRobot
* DB2
* DigitalOcean
* DocuSign
* Dropbox
* DynamicsCRM
* DynamicsGP
* DynamicsNAV
* Ebay
* EdgarOnline
* Elasticsearch
* Email
* EpicorERP
* ESalesManager
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
* Garoon
* GitHub
* Gmail
* GMOMakeShop
* GoogleAds
* GoogleAdsManager
* GoogleAnalytics
* GoogleBigQuery
* GoogleCalendar
* GoogleCM
* GoogleContacts
* GoogleDataCatalog
* GoogleDirectory
* GoogleDrive
* GoogleSearch
* GoogleSheets
* GoogleSpanner
* Greenplum
* HarperDB
* HDFS
* Highrise
* HPCC
* HubSpot
* IBMCloudObjectStorage
* IBMCloudSQLQuery
* Instagram
* JIRA
* JiraServiceDesk
* JSON
* Kintone
* LDAP
* LinkedIn
* LinkedInAds
* Lohaco
* Magento
* MailChimp
* MariaDB
* Marketo
* MarkLogic
* MFExpense
* MFInvoice
* MicrosoftPlanner
* MicrosoftProject
* MongoDB
* MSTeams
* MYOB
* MySQL
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
* PayPal
* PCAAccounting
* PCASales
* Pinterest
* Ponparemall
* PostgreSQL
* Presto
* Qoo10
* Quandl
* QueryFederation
* QuickBase
* QuickBooks
* QuickBooksOnline
* QuickBooksPOS
* Reckon
* Redis
* Redshift
* Replicate
* REST
* RSS
* S3Destination
* Sage200
* Sage50UK
* SageBCAccounting
* SageIntacct
* Salesforce
* SalesforceChatter
* SalesforcePardot
* Sansan
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
* SendGrid
* SFEinsteinAnalytics
* SFMarketingCloud
* SFTP
* SharePoint
* ShipStation
* Shopify
* Slack
* Smaregi
* Smartsheet
* Snowflake
* SparkSQL
* Splunk
* SQL
* SQLite
* Square
* SSAS
* Streak
* Stripe
* SugarCRM
* SuiteCRM
* SurveyMonkey
* Sybase
* SybaseIQ
* Tally
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
* WooCommerce
* WordPress
* Wowma
* xBase
* XCart
* Xero
* XeroWorkflowMax
* XML
* YahooShopping
* YouTubeAnalytics
* Zendesk
* ZohoBooks

## License

This project is licensed under the MIT License - see the LICENSE file for details
