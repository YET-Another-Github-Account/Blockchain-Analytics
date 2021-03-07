# Introduction 
The intention of this document is to analyse and to evaluate current options and scenarios for blockchain analytics. 
Practical scenario for this evaluation was the requirement of the YAM DAO to support the [degenerative.finance](https://degenerative.finance /) subproject with a dashboard that contains specific measures for observing the development and success of the project. 
For developing the dashboard, three scenarios and technologies were briefly evaluated: 
* [The Graph]( https://thegraph.com/)
* [Dune Analytics](https://duneanalytics.com/)
* [Google BigQuery Ethereum dataset](https://cloud.google.com/blog/products/data-analytics/ethereum-bigquery-public-dataset-smart-contract-analytics)

# DeFi Dashboard solution evaluation 
In this next section the developer experiences and evaluation criteria for selecting the dashboard solution will be described. 

## The Graph 
The Graph is positioned as indexing protocol to build and publish APIs. These indexed and published APIs are referred as Subgraph. A wide variety of hosted and community provided Subgraphs for a significant amount of Blochchain and Defi projects are available [here](https://thegraph.com/explorer/)
Technical backbone of a graph-node is a PostgreSQL database. [Link]( https://github.com/graphprotocol/graph-node#quick-start)
The developments in the projects GithHub are licensed under the Apache Open-Source license. 
The first implementation attempt was started with The Graph, but were later discontinued and replaced with Dune Analytics. 
During the evaluation of the The Graph, the following challenges were experienced 

* ### Ramp-Up time and developer background 
Even though the procedure is well [documented]( https://thegraph.com/docs/define-a-subgraph#create-a-subgraph-project ), setting up a SubGraph requires a minumum of Solidity developer skills and setting up a developer IDE.  The clear advantage here is the scalable self-service approach, in case the users come with the required technological background. 
For this evaluation it was possible to setup and index a SubGraph, unfortunately the indexed data was incomplete 

* ### GraphQL as query language for analytical dashboards 
Interface for querying the SubGraphs is the API query language 
GraphQL is not positioned as an advanced analytics query language like SQL is. [here]( https://graphql.org/faq/#is-graphql-a-database-language-like-sql)
Therefore using a SubGraph and the GraphQL query language would not have been a suitable solution for creating a Dashboard that requires advanced analytical functions comparable to what modern SQL databases provide.  
