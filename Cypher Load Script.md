# Cypher Load Script to generate GraphDB using Neo4j

## Entity: Asset

Key Statement:
CREATE CONSTRAINT `imp_uniq_Asset_id` IF NOT EXISTS
FOR (n: `Asset`)
REQUIRE (n.`id`) IS UNIQUE;

Load Statement:
UNWIND $nodeRecords AS nodeRecord
WITH *
WHERE NOT nodeRecord.`id` IN $idsToSkip AND NOT nodeRecord.`id` IS NULL
MERGE (n: `Asset` { `id`: nodeRecord.`id` })
SET n.`name` = nodeRecord.`name`
SET n.`lat` = toFloat(trim(nodeRecord.`lat`))
SET n.`lon` = toFloat(trim(nodeRecord.`lon`));


## Entity: Application

Key Statement:
CREATE CONSTRAINT `imp_uniq_Application_id` IF NOT EXISTS
FOR (n: `Application`)
REQUIRE (n.`id`) IS UNIQUE;

Load Statement:
UNWIND $nodeRecords AS nodeRecord
WITH *
WHERE NOT nodeRecord.`id` IN $idsToSkip AND NOT nodeRecord.`id` IS NULL
MERGE (n: `Application` { `id`: nodeRecord.`id` })
SET n.`name` = nodeRecord.`name`;


## Entity: Department

Key Statement:
CREATE CONSTRAINT `imp_uniq_Department_id` IF NOT EXISTS
FOR (n: `Department`)
REQUIRE (n.`id`) IS UNIQUE;

Load Statement:
UNWIND $nodeRecords AS nodeRecord
WITH *
WHERE NOT nodeRecord.`id` IN $idsToSkip AND NOT nodeRecord.`id` IS NULL
MERGE (n: `Department` { `id`: nodeRecord.`id` })
SET n.`name` = nodeRecord.`name`;

## Entity: Sensor

Key Statement:
CREATE CONSTRAINT `imp_uniq_Sensor_id` IF NOT EXISTS
FOR (n: `Sensor`)
REQUIRE (n.`id`) IS UNIQUE;

Load Statement:
UNWIND $nodeRecords AS nodeRecord
WITH *
WHERE NOT nodeRecord.`id` IN $idsToSkip AND NOT nodeRecord.`id` IS NULL
MERGE (n: `Sensor` { `id`: nodeRecord.`id` })
SET n.`entType` = nodeRecord.`entType`
SET n.`name` = nodeRecord.`name`;

## Entity: Network

Key Statement:
CREATE CONSTRAINT `imp_uniq_NETWORK_id` IF NOT EXISTS
FOR (n: `NETWORK`)
REQUIRE (n.`id`) IS UNIQUE;

Load Statement:
UNWIND $nodeRecords AS nodeRecord
WITH *
WHERE NOT nodeRecord.`id` IN $idsToSkip AND NOT nodeRecord.`id` IS NULL
MERGE (n: `NETWORK` { `id`: nodeRecord.`id` })
SET n.`entType` = nodeRecord.`entType`
SET n.`name` = nodeRecord.`name`;

## Entity: Asset Type

Key Statement:
CREATE CONSTRAINT `imp_uniq_Asset Type_id` IF NOT EXISTS
FOR (n: `Asset Type`)
REQUIRE (n.`id`) IS UNIQUE;

Load Statement:
UNWIND $nodeRecords AS nodeRecord
WITH *
WHERE NOT nodeRecord.`id` IN $idsToSkip AND NOT nodeRecord.`id` IS NULL
MERGE (n: `Asset Type` { `id`: nodeRecord.`id` })
SET n.`name` = nodeRecord.`name`;

## Entity: Vendor

Key Statement:
CREATE CONSTRAINT `imp_uniq_Vendor_id` IF NOT EXISTS
FOR (n: `Vendor`)
REQUIRE (n.`id`) IS UNIQUE;

Load Statement:
UNWIND $nodeRecords AS nodeRecord
WITH *
WHERE NOT nodeRecord.`id` IN $idsToSkip AND NOT nodeRecord.`id` IS NULL
MERGE (n: `Vendor` { `id`: nodeRecord.`id` })
SET n.`entType` = nodeRecord.`entType`
SET n.`name` = nodeRecord.`name`;

## Entity: Manufacturer

Key Statement:
CREATE CONSTRAINT `imp_uniq_Manufacturer_id` IF NOT EXISTS
FOR (n: `Manufacturer`)
REQUIRE (n.`id`) IS UNIQUE;

Load Statement:
UNWIND $nodeRecords AS nodeRecord
WITH *
WHERE NOT nodeRecord.`id` IN $idsToSkip AND NOT nodeRecord.`id` IS NULL
MERGE (n: `Manufacturer` { `id`: nodeRecord.`id` })
SET n.`name` = nodeRecord.`name`;

## Entity: Module

Key Statement:
CREATE CONSTRAINT `imp_uniq_Module_id` IF NOT EXISTS
FOR (n: `Module`)
REQUIRE (n.`id`) IS UNIQUE;

Load Statement:
UNWIND $nodeRecords AS nodeRecord
WITH *
WHERE NOT nodeRecord.`id` IN $idsToSkip AND NOT nodeRecord.`id` IS NULL
MERGE (n: `Module` { `id`: nodeRecord.`id` })
SET n.`name` = nodeRecord.`name`;

## Entity: Power Source

Key Statement:
CREATE CONSTRAINT `imp_uniq_Power Source_id` IF NOT EXISTS
FOR (n: `Power Source`)
REQUIRE (n.`id`) IS UNIQUE;

Load Statement:
UNWIND $nodeRecords AS nodeRecord
WITH *
WHERE NOT nodeRecord.`id` IN $idsToSkip AND NOT nodeRecord.`id` IS NULL
MERGE (n: `Power Source` { `id`: nodeRecord.`id` })
SET n.`name` = nodeRecord.`name`;



## Relation: IS_USED_BY

Load Statement:
UNWIND $relRecords AS relRecord
MATCH (source: `Application` { `id`: relRecord.`thingId` })
MATCH (target: `Department` { `id`: relRecord.`entityid` })
MERGE (source)-[r: `IS_USED_BY`]->(target);

## Relation: IS_CONTROLLING

Load Statement:
UNWIND $relRecords AS relRecord
MATCH (source: `Application` { `id`: relRecord.`thingId` })
MATCH (target: `Asset` { `id`: relRecord.`entityid` })
MERGE (source)-[r: `IS_CONTROLLING`]->(target);

## Relation: IS_FEEDING_DATA_TO

Load Statement:
UNWIND $relRecords AS relRecord
MATCH (source: `Asset` { `id`: relRecord.`thingId` })
MATCH (target: `Application` { `id`: relRecord.`entityid` })
MERGE (source)-[r: `IS_FEEDING_DATA_TO`]->(target);

## Relation: IS_CONTAINING_SENSOR

Load Statement:
UNWIND $relRecords AS relRecord
MATCH (source: `Asset` { `id`: relRecord.`thingId` })
MATCH (target: `Sensor` { `id`: relRecord.`entityid` })
MERGE (source)-[r: `IS_CONTAINING_SENSOR`]->(target);

## Relation: IS_USING

Load Statement:
UNWIND $relRecords AS relRecord
MATCH (source: `Asset` { `id`: relRecord.`thingId` })
MATCH (target: `NETWORK` { `id`: relRecord.`entityid` })
MERGE (source)-[r: `IS_USING`]->(target);

## Relation: IS_OF_TYPE

Load Statement:
UNWIND $relRecords AS relRecord
MATCH (source: `Asset` { `id`: relRecord.`thingId` })
MATCH (target: `Asset Type` { `id`: relRecord.`entityid` })
MERGE (source)-[r: `IS_OF_TYPE`]->(target);

## Relation: IS_FROM_VENDOR

Load Statement:
UNWIND $relRecords AS relRecord
MATCH (source: `Asset` { `id`: relRecord.`thingId` })
MATCH (target: `Vendor` { `id`: relRecord.`entityid` })
MERGE (source)-[r: `IS_FROM_VENDOR`]->(target);

## Relation: IS_MANUFACTURED_BY

Load Statement:
UNWIND $relRecords AS relRecord
MATCH (source: `Asset` { `id`: relRecord.`thingId` })
MATCH (target: `Manufacturer` { `id`: relRecord.`entityid` })
MERGE (source)-[r: `IS_MANUFACTURED_BY`]->(target);

## Relation: IS_EQUIPPED_WITH

Load Statement:
UNWIND $relRecords AS relRecord
MATCH (source: `Asset` { `id`: relRecord.`thingId` })
MATCH (target: `Module` { `id`: relRecord.`entityid` })
MERGE (source)-[r: `IS_EQUIPPED_WITH`]->(target);

## Relation: IS_POWERED_BY

Load Statement:
UNWIND $relRecords AS relRecord
MATCH (source: `Asset` { `id`: relRecord.`thingId` })
MATCH (target: `Power Source` { `id`: relRecord.`entityid` })
MERGE (source)-[r: `IS_POWERED_BY`]->(target);
