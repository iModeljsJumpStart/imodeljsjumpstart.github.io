# Challenge: Creating useful queries

## Summary

By completing this you will learn how to:
- Registering a new project to be used with the imodel console.
- Learn useful ECSQL queries.

// Do users already have a background in SQL?

## Setup

// TODO

// Will all challenges be based on the same imodel?

## Goals

# Opening your project on imodelconsole.bentley.com
// Point and click to target and open cloned project

// How much background needs to be provided for our Bis Schema?

# Providing more descriptive labels 
**Goal** Provide a more descriptive userlabe - displaya more descriptive form of the label by replacing 'Fabric' with 'GreenFabric'
> SELECT ECInstanceId, UserLabel, replace(UserLabel,'Fabric','SoftFabric') ModifiedLabel FROM bis.Element WHERE UserLabel LIKE '%Fabric%'

# Limiting the results of queries
**Goal** Return all [SpatialElement](https://www.imodeljs.org/bis/domains/biscore.ecschema/#spatialelement)s that do have a user label and limit the results to 5
> SELECT ECInstanceId,ECClassId, UserLabel FROM bis.SpatialElement WHERE UserLabel IS NOT NULL LIMIT 5

# Targetting specific ECClasses
// Background on ECClasses
**Goal** Returns elements only if it's exactly of the specified types - sub-classes are not included
> SELECT * FROM bis.Element WHERE ECClassId IS (ONLY Generic.PhysicalObject, ONLY BisCore.LightLocation)

# Joining tables to aggregate information
**Goal** Return the [Model](https://www.imodeljs.org/bis/domains/BisCore.ecschema.md#model) that contains the [Element](https://www.imodeljs.org/bis/domains/BisCore.ecschema.md#element) with code containing 'Sheets'
> SELECT rel.SourceECInstanceId ModelId FROM bis.ModelContainsElements rel JOIN bis.Element ON rel.TargetECInstanceId=Element.ECInstanceId WHERE Element.CodeValue='Sheets'

# Spatial queries
**Goal** Return all [SpatialElement](https://www.imodeljs.org/bis/domains/biscore.ecschema/#spatialelement)s that are contained or overlap a cube defined by the minimum coordinate (0, 0, 0) and maximum coordinate (415|120|15).
> SELECT e.ECInstanceId, e.UserLabel, i.MinX, i.MinY, i.MinZ, i.MaxX, i.MaxY, i.MaxZ FROM bis.SpatialElement e JOIN bis.SpatialIndex i ON e.ECInstanceId=i.ECInstanceId WHERE i.MinX<=415 AND i.MinY<=120 AND i.MinZ<=15 AND i.MaxX >= 0 AND i.MaxY >= 0 AND i.MaxZ >= 0
