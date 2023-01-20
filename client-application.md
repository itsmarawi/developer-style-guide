# Client Application Style Guide

## Sections

* [Folder Structure](#folder-structure)
* [Base Resource](#entity-resource)

## Folder Structure
- /layouts
- /components
- /dialogs
- /pages
- /interfaces
- /store
- /resource
- /services
- /workers

## UI Logic
## Entity Resource 
## Resource Registration
## Local Base
- Local Database
- Cache 
## Enitity Service
## REST Client SDK

## Definition of Terms

### Entity

Represents a single record on the business domain. 

Entity is central focus of application. All presentation logic are implemented based on the requirements required to manipulate entity properties or records.

*Employee for example is an entity that represents the properties of an employee in an institution.*

*Student for example is an enity that represent the properties of a school student.*

### Entity Resource     

A Resource is the data represention of an entity that is stored OFFLINE or/and ONLINE.

Enity Resource is record manager for specific [entity](#entity) that keeps synchronization between OFFLINE *(or Cached records)* to/from ONLINE *(or Server records)*.

Middleware between UI States and Storage.

### Entity Service 

Service Access for a specific entity to ONLINE resources via RESTFul API.





