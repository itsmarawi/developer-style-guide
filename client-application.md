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

### **Entity**

Represents a record on the business domain. 

Entity is central focus of application. All presentation logic are implemented based on the requirements required to manipulate entity properties or records.

*Employee for example is an entity that represents the properties of an employee in an institution.*

*Student for example is an enity that represent the properties of a school student.*

### **Entity Resource**     

A Resource is the data represention of an entity that is stored OFFLINE or/and ONLINE.

Enity Resource is record manager for specific [entity](#entity) that keeps synchronization between OFFLINE *(or Cached records)* to/from ONLINE *(or Server records)*.

Middleware between UI States and Storage.

### **Entity Service**

Web Service Access for a specific entity to ONLINE resources via RESTFul API.

### Synchronizatin Worker

Background resource processor that runs on a separate thread to improve responsiveness of UI or main thread.

Bulk of collaboration to remote service is executed under worker thread.

### Resource Registration

Common code integration between UI thread and background worker thread.

Resource registration allows every entities to have different implementations and categories.

Entity resources are grouped based on microservice component in server-side they most related to and are categorized to three as follows:

- **Pure Entity** - Simplest Entity category with equivalent record on database server. All CRUD (Create, Read, Update, Delete) operations can be done with it.
- **Virtual Entity** - Entity category that are dynamically generated or computed on server-side. Virtual entities are usually aggregation of various entities. Only read operations can be done with virtual entities.
- **Form Entities** - Entity category submitted from client to server computation or recording. Various pure entities are maybe generated or created on server-side from the submission of form entity record.


### Resource Synchronizer

Manages all registered entity resource instances.

It controls synchronization status by stoping synching when current user is not authorized and resuming it once authorized.

It monitors all record requires to be synchronized and provide summary.

### REST Client SDK

Auto-generated Client SDK that integrates client application to Dansalan Gateway RESTFul API.

### Dansalan Gateway

RESTful Web-Service Application that serves as the access-point to server-side resources.

### Microservice

Server Component that represents a specific domain function.