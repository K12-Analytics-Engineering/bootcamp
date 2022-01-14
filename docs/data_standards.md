# Data standards

- [Ed-Fi](#ed-fi)


----

## Ed-Fi
### The Ed-Fi Data Standard
The Ed-Fi Data Standard is the set of rules for the collection, management, and organization of educational data. The data standard consists of the [Ed-Fi Unifying Data Model](https://techdocs.ed-fi.org/display/EFDS33/Unifying+Data+Model+-+v3.3+Model+Reference) and a set of [Rest API bindings](https://api.ed-fi.org/v5.3/docs/swagger/index.html?urls.primaryName=Resources). The data model serves to organize educational data from a variety of data sources. This means using a common language to talk about things like students, courses, and sections.

Imagine taking data from your student information system (SIS), learning management system (LMS), and assessment platform, and needing to organize it for your analytics. All systems use different names for similar things. Student last name, family name, surname, etc. Ed-Fi is a way of using common names and structures to organize our data.


### Ed-Fi technology
The Ed-Fi Alliance also publishes technology in the form of the Ed-Fi API and ODS that is an implementation of the standard. An operational data store (ODS) integrates data from multiple data sources and for Ed-Fi comes in the form of a Microsoft SQL Server or PostgreSQL database. The ODS is highly normalized storing data in such a way that reduces duplication. The ODS is a transactional store meant to support a high number of insertions, updates, and deletes. The Ed-Fi API is the mechanism by which the data in the ODS is updated.

### Ed-Fi certification
When an EdTech vendor becomes certified, they have proven that they are able manage a set of data on a target Ed-Fi API. This means if you implement the Ed-Fi API and ODS, your vendor will send data back to you! You won't need to pull / extract it, they will send it to you.

