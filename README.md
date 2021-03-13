# Introduction 
The intention of this document is to analyse and to evaluate current options and scenarios for blockchain analytics. 
Practical scenario for this evaluation was the requirement of the YAM DAO to support the [degenerative.finance](https://degenerative.finance/) subproject with a DeFi dashboard. The dashboard was designed to visualize specific measures for observing the development and success of the project and DeFi products. 
For developing the dashboard, three scenarios and technologies were briefly evaluated: 
* [The Graph](https://thegraph.com/)
* [Dune Analytics](https://duneanalytics.com/)
* [Google BigQuery Ethereum dataset](https://cloud.google.com/blog/products/data-analytics/ethereum-bigquery-public-dataset-smart-contract-analytics)
# DeFi Dashboard solution evaluation 
In this next section the developer experience and evaluation criteria for selecting the dashboard solution will be described. 

## The Graph 
The Graph is positioned as indexing protocol to build and publish APIs. These indexed and published APIs are referred as Subgraph. A wide variety of hosted and community provided Subgraphs for a significant amount of Blochchain and Defi projects are available [here](https://thegraph.com/explorer/).

Technical backbone of a graph-node is a [PostgreSQL database]( https://github.com/graphprotocol/graph-node#quick-start).

The developments in the projects GithHub are licensed under the Apache Open-Source license. 
The first implementation attempts was started with The Graph, but were later discontinued and replaced with Dune Analytics. 
The decision to discontinue the Subgraph development was based on the following considerations and findings. 

### Ramp-Up time and developer background 
Even if the procedure is well [documented]( https://thegraph.com/docs/define-a-subgraph#create-a-subgraph-project), setting up a SubGraph requires a minimum of Solidity developer skills and setting up a developer IDE.  

The clear advantage here is the scalable self-service approach, in case the developers have the required technological background. 


For this evaluation it was possible to setup and index a SubGraph, unfortunately the indexed data was incomplete. Due to missing or unknown debug or logging options, it was not possible to identify the reason for the incomplete indexing. 
 

 
### GraphQL as query language for analytical dashboards 
Interface for querying the SubGraphs is the API query language GraphQL, which not [positioned](https://graphql.org/faq/#is-graphql-a-database-language-like-sql) as an advanced analytics data query language like SQL is. 
That’s why using a SubGraph and the GraphQL query language would not have been a suitable solution for creating a Dashboard.  

The dashboard requirements were advanced analytical functions comparable to what modern SQL databases provide. The required advanced analytical functions are for example window- or median-functions. 

![TheGraphIndexing1](https://github.com/YET-Another-Github-Account/Blockchain-Analytics/blob/main/images/TheGraph1.png?raw=true)
*Incomplete YAMV3 Subgraph Indexing*
### Documentation and community support  
The project documentation and available community content are enterprise software grade. 
Unfortunately the community support within the Discord channel left questions about the incomplete indexing unanswered and was not supportive as required to efficiently continue and finish the evaluation. 

This evaluation of the responsiveness on Discord might be a temporal and subjective experience. 
### Summary The Graph evaluation 
The active GitHub indicates a strong adoption of The Graph for creating APIs that serve dApps. For this dashboard evaluation a query language that provides advanced analytical functions is mandatory. By design GraphQL doesn’t provide these rich analytical functions like SQL does. 

Therefore The Graph wasn’t probably the right architectural choice from the beginning on and serves a different scenario which is API and dApp creation. 

![TheGraphIndexing2](https://github.com/YET-Another-Github-Account/Blockchain-Analytics/blob/main/images/TheGraph2.png?raw=true)
*Subgraph Indexing Logs*

Out of scope in this evaluation were overall The Graph concepts  like Indexers, Curators and Delegators.  
Both the open-source license of the overall GitHub project and the usage the open-source database PostgreSQL are well aligned with the [DeFi paradigms](https://github.com/ong/awesome-decentralized-finance#what-is-decentralized-finance) of decentralization and open-source. 

## Google BigQuery Ethereum dataset
During the dashboard creation the was [UMA UMIP 20]( https://github.com/UMAprotocol/UMIPs/blob/master/UMIPs/umip-20.md) referenced to calculate the 30 days median Gas price for the uGas synthetic futures.
Within the UMIP is a sample coding point the [Google BigQuery Ethereum dataset](https://cloud.google.com/blog/products/data-analytics/ethereum-bigquery-public-dataset-smart-contract-analytics). Even though BigQuery is a leading analytics database and would have enabled the strongest degree of flexibility like using preferred analytics tools like Tableau, BigQuery was not further evaluated. 
There are two non-technical aspects which make BigQuery theoretically not a good fit for DeFi projects and paradigms like censorship resistance: 
* GCP Big Query is not developed and provided under an open-source license 
* Deployed as PaaS service on the Google Cloud Platform which is an easy target for censorship. [Link](https://transparencyreport.google.com/user-data/us-national-security)

![GCP-Marketplace](https://github.com/YET-Another-Github-Account/Blockchain-Analytics/blob/main/images/GCP_Marketplace.png?raw=true)
*GCP Big Query Datasets*

## Dune Analytics 
Due to this [YouTube video]( https://www.youtube.com/watch?v=AWlwO9T8dkY) Dune Analytics was evaluated as the next option for creating an advanced DeFi dashboard. 
Dune analytics is an [Oslo](https://careers.duneanalytics.com/) based company with a free and pro [offering]( https://www.duneanalytics.com/pricing) for Dune analytics. 
This evaluation was done with the free version of Dune Analytics. 
Like for The Graph, the technical backend of Dune analytics is a PostgreSQL database. 
For the development of the Dashboard, there are four components provided by Dune analytics. 

### The Dashboard designer 
The Dashboard designer is a browser based tool to design the dashboard. It provides basic design and layout options, but is sufficient enough to create visual appealing Dashboard. 
Compared to leading commercial business intelligence or dashboard tools, the Dune designer provided about 10%-20% of the functionality. 

Dune comes with an impressive [gallery of popular dashboards]( https://explore.duneanalytics.com/dashboards/popular) created by the team and community, which demonstrate the current functionality is more than sufficient to build professional and beatutiful dashboards.  

![SuperRareDashboard](https://github.com/YET-Another-Github-Account/Blockchain-Analytics/blob/main/images/SuperRareDahsboard.png?raw=true)
*Dune SuperRare Dashboard by keeganead*
 
The designer allows to drag & drop textboxes and widgets on the dashboard. The widgets provide the option for layout formatting with a markup language and the option to add images. 

### The query designer 
For data engineers the most exciting feature of Dune is the access to the Dune database schema and the option to leverage the PostgreSQL-syntax and features. 

The dune query designer combines a SQL-Editor and visualization designer, by providing the option to configure visual elements like charts, tables or maps for the SQL-query results. 
To prevent developers having to start from the scratch, a broad library of sample queries is available and the option to fork these queries for own adjustments. 

When browsing and reading the sample queries, the complexity and quality of the queries clearly indicate the involvement of skilled and expierenced data engineers.

![QueryDesigner](https://github.com/YET-Another-Github-Account/Blockchain-Analytics/blob/main/images/QueryDesigner.png?raw=true)
 *Dune Query Designer showing a SuperRare SQL Query*


### The dune decoding and abstractions 
Next to the SQL-queries, the indexing/decoding for project specific contracts and the abstractions layer are important services for creating blockchain specific data queries. 
In case project related contracts are required for queries, the Dune team provides a [form]( https://duneanalytics.retool.com/embedded/public/892af55f-a6ff-41df-b203-f8acb6f0a38b) to schedule contracts for decoding. 
 
Smart-contract domain specific database views and tables enable SQL-developers to reuse existing data-models for example pre-calculated prices for tokens or views containing dex trades. 

These views and tables are referred as [abstraction layer]( https://duneanalytics.retool.com/embedded/public/892af55f-a6ff-41df-b203-f8acb6f0a38b) within the Dune data platform. Building domain specific and predefined datasets is essential for providing an efficient and sustainable infrastructure within the Dune database- and data models. 

For implementing dashboards for new projects, the contracts have to be maintained in abstraction layer tables. For example contracts have to be added to the ER20 tokens table, to be made available for DEX queries. During implementation, the maintenance of new contracts and tokens to the abstraction layer will happen via GitHub workflows like Pull-requests. These interactions require basic knowledge of GitHub. 

![DuneDecoding](https://github.com/YET-Another-Github-Account/Blockchain-Analytics/blob/main/images/DuneDecoding.png?raw=true)
*Dune form to schedule contract decoding*
## Implementation of the degenerative.finance dashboard 
The general setup here reflected to typical implementation of a dashboard project in corporate environments. The domain experts with strong DeFi background defined the requirements documents as basic dashboard mock-up. The actual implementation was done with a technical background in analytics, but basic knowledge about Solidity contracts and the Dune data model. Discord was used the discuss the implementation and progress. 

![DashboardMockup](https://github.com/YET-Another-Github-Account/Blockchain-Analytics/blob/main/images/DashboardMockUp.png?raw=true)
*Dashboard mockup by @nonstopTheo*
 
### Lessons learned and best practice 
During the implementation the following best practices where identified for new Dashboard and projects. 

* Document all relevant contracts and schedule them for decoding at the beginning of the Dashboad implementation 

* Get familiar with the Dune abstraction layer and maintain relevant contracts there early 

* Browser and analyse the existing dashboards and queries to learn and adopt best practices  

* In case of teams with distributed skillsets the Solidity developers or DeFi experts ideally specify specifications similar to the UMA [UMIPs]( https://github.com/UMAprotocol/UMIPs/blob/master/UMIPs/umip-16.md) with pseudocode examples to adapted in SQL 

* Ideally the Dune team and community would curate a glossary and quality assured gallery for implementing common DeFi queries and charts like TVL, unique wallet holder, minting etc. Currently there are already almost too many examples and queries. A gallery with most frequent DeFi performance indicators will help developers to on-board quickly. This series of tweets is already a good starting point: 
https://twitter.com/0xBoxer/status/1367563948082532362
* The Dune team is very supportive and active on their Discord which was a strong influencing factor for choosing the product and the required support.  https://discord.gg/PxYDzqx4

![DegenDashboard1](https://github.com/YET-Another-Github-Account/Blockchain-Analytics/blob/main/images/DegenDashboard1.png?raw=true)
*Degenerative.finance Dashboard*

### Conclusion and state of the Blockchain analytics 
Some general thoughts, room for improvement and ideas for Blockchain analytics. 
* Duplicating the transactional Blockchains ledger to analytical databases reproduces the 30+ year old approach of having to copy transactional systems of records to data-warehouses for advanced analytics

* Future Blockchain or distributed ledger technologies might mitigate this complexity of having to duplicate transactional data with built in analytical capabilities. Especially since built in analytical capabilities will enable more real-time enabled advanced analytics directly on the DLT 

* Duplicating and persisting a Blockchain in a relational database destroys all immutability characteristics of DLT

* Instead of batching the transactions into a relational database, more event oriented architectures and using stream functionality could be a viable architecture alternative. Particularly since the programming of smart contracts is mainly event oriented. 

### Disclaimer 
This document is a working document and reflects the authors current experience and knowledge in the area of Blockchain analytics. 
It will likely be continuously improved and extended. In case of comments, critics or suggestions for improvement, please create a GitHub Issue. 
