# Introduction 
The intention of this document is to analyse and to evaluate current options and scenarios for blockchain analytics. 
Practical scenario for this evaluation was the requirement of the YAM DAO to support the [degenerative.finance](https://degenerative.finance/) subproject with a dashboard that contains specific measures for observing the development and success of the project. 
For developing the dashboard, three scenarios and technologies were briefly evaluated: 
* [The Graph]( https://thegraph.com/)
* [Dune Analytics](https://duneanalytics.com/)
* [Google BigQuery Ethereum dataset](https://cloud.google.com/blog/products/data-analytics/ethereum-bigquery-public-dataset-smart-contract-analytics)
# DeFi Dashboard solution evaluation 
In this next section the developer experiences and evaluation criteria for selecting the dashboard solution will be described. 

## The Graph 
The Graph is positioned as indexing protocol to build and publish APIs. These indexed and published APIs are referred as Subgraph. A wide variety of hosted and community provided Subgraphs for a significant amount of Blochchain and Defi projects are available [here](https://thegraph.com/explorer/).
Technical backbone of a graph-node is a [PostgreSQL database]( https://github.com/graphprotocol/graph-node#quick-start).
The developments in the projects GithHub are licensed under the Apache Open-Source license. 
The first implementation attempt was started with The Graph, but were later discontinued and replaced with Dune Analytics. 
During the evaluation of the The Graph, the following challenges were experienced: 

### Ramp-Up time and developer background 
Even though the procedure is well [documented]( https://thegraph.com/docs/define-a-subgraph#create-a-subgraph-project ), setting up a SubGraph requires a minimum of Solidity developer skills and setting up a developer IDE.  The clear advantage here is the scalable self-service approach, in case the users come with the required technological background. 
For this evaluation it was possible to setup and index a SubGraph, unfortunately the indexed data was incomplete. Due to missing or unknown debug or logging options, it was not possible to identify the reason for the incomplete indexing. 
### GraphQL as query language for analytical dashboards 
Interface for querying the SubGraphs is the API query language 
GraphQL is not positioned as an advanced analytics data query language like SQL. That’s why using a SubGraph and the GraphQL query language would not have been a suitable solution for creating a Dashboard that requires advanced analytical functions comparable to what modern SQL databases provide. The required advanced analytical functions are for example window-functions. 

### Documentation and community support  
The project documentation and available community content are enterprise software grade. 
Unfortunately the community support within the Discord channel left questions about the incomplete indexing unanswered and was not supportive as required to efficiently continue with the evaluation. This evaluation might be a temporal and subjective experience. 
### Summary   
The active GitHub indicates a strong adoption of The Graph for creating APIs that serves dApps. For this dashboard evaluation a tool for creating advanced analytical functions is mandatory. By design GraphQL doesn’t provide these rich analytical functions like SQL does. 
Therefore The Graph wasn’t probably the right architectural choice from the beginning on and serves a different use-case which is API and dApp creation. 
Out of scope in this evaluation were overall system design like the concepts of Indexers, Curators and Delegators.  
Both the open-source license of the overall GitHub project and the usage the open-source database PostgreSQL are well aligned with the [DeFi paradigms](https://github.com/ong/awesome-decentralized-finance#what-is-decentralized-finance) of decentralization and open-source. 

## Google BigQuery Ethereum dataset
During the dashboard creation the was [UMA UMIP 20]( https://github.com/UMAprotocol/UMIPs/blob/master/UMIPs/umip-20.md) referenced to calculate the 30 days median Gas price for the uGas synthetic futures.
Within the UMIP is a sample coding point the [Google BigQuery Ethereum dataset](https://cloud.google.com/blog/products/data-analytics/ethereum-bigquery-public-dataset-smart-contract-analytics). Even though BigQuery is a leading analytics database and would have enabled the strongest degree of flexibility like using preferred analytics tools like Tableau, BigQuery was not further evaluated. 
There are two non-technical aspects which make BigQuery might not be a good fit for DeFi projects: 
* GCP Big Query is not developed under an open-source license 
* Deployed as PaaS service on the Google Cloud Platform it’s an easy target for censorship. [Link](https://transparencyreport.google.com/user-data/us-national-security)

