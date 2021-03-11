







### difference between the business layer & service layer

In our projects we often have the following structure:

Service layer:

- Publishes the Service Endpoint (this could be your MVC web page, or a WCF endpoint)
- Does a security check
- Maps data from contract data transfer objects to business objects
- Calls functionality in the business layer

Business layer

- Contains business logic
- Accesses the data layer (this could be your entity framework data model)