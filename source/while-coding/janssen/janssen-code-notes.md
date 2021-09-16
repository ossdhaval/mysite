# Janssen code notes

### code involved in loading configuration

- `io.jans.as.common.service.common.ConfigurationService`:
  - allows to add and update configuration in the database using `PersistenceEntryManager`. Also provides other methods.
- jans-orm : `FileConfiguration` is used to read configuration from property files

### Misc notes:

- jans-auth-server `AppInitializer` class loads all the services required by jans-server, like persistence manager.
  - `AppInitializer` uses methods in `ApplicationFactory` to read properties stored in files and create objects like `PersistenceEntryManagerFactory` using `PersistanceFactoryService` which is injected in `ApplicationFactory`
  - 
