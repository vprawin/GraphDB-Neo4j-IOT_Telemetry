# Representing HP IOT Telemetry Data in form of GraphDB Using Neo4j

## GraphDB

A graph database, also known as a graph-oriented database or graph data store, is a type of NoSQL database that uses graph theory to store, map, and query relationships between data. In a graph database, data is represented in the form of nodes and edges, where nodes represent entities and edges represent relationships between these entities.

**A simple example is shown below**

![alt text](https://github.com/vprawin/GraphDB/blob/main/Image%20Source/graphdb_example.png)


Graph databases are designed to handle complex and highly interconnected data, making them particularly useful for applications such as social networks, recommendation systems, and fraud detection, among others. They can provide more natural and efficient ways of querying data compared to traditional relational databases, which use tables and rows to store and organize information.

Popular graph databases include Neo4j, Amazon Neptune, and Microsoft Azure Cosmos DB.

**-We are Using Neo4j to create GraphDB for HP Entities-**


## HP GraphDB Entities

Below are the entites considered to supply IOT Telemetry Data
- Manufacturer (OEM Name)
- Asset (Printer Unit)
- Asset Type (Type of Printer Unit like Laser / Dot etc.)
- Network (Network Adapter used in Printer)
- Sensor (Different sensor like Thermistor, Positioning, Flow Sensors etc. equipped within Printer)
- Power Source (Power Supply Modules within Printer)
- Vendor (Vendor's associated with Printer Parts)
- Module (Different Modules equipped in Printer like GPS, Mother Board)
- Application (Internal Application using IOT Telemetry Data)
- Department (Department within HP using Data)


## GraphDB Schema 

![alt text](https://github.com/vprawin/GraphDB/blob/main/Image%20Source/Graph Schema.png)
