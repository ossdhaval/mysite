# Janssen code notes

### code involved in loading configuration

- `io.jans.as.common.service.common.ConfigurationService`:
  - allows to add and update configuration in the database using `PersistenceEntryManager`. Also provides other methods.
- jans-orm : `FileConfiguration` is used to read configuration from property files

### Misc notes:

- jans-auth-server `AppInitializer` class loads all the services required by jans-server, like persistence manager.
  - `AppInitializer` uses methods in `ApplicationFactory` to read properties stored in files and create objects like `PersistenceEntryManagerFactory` using `PersistanceFactoryService` which is injected in `ApplicationFactory`
- To see which entity classes are mapped to which tables, search for `@ObjectClass` in jans-auth-server project. You'll find `@ObjectClass(tablename)`.
  - there are many `model` packages in AS but only few (~23) are persistence related. Others (like `CodeVerifier` under `io.jans.as.model.authorize` package) are not related to persistance rather they are like POJOs.
- `objectClass` is the name of the table. This is visible from `SqlConnectionProvider`.`getTableMappingByKey()`.
- 

### properties and featureflags

- Classes that hold the properties of some of the modules are below:
  - io.jans.as.model.configuration.AppConfiguration
  - io.jans.as.model.common.FeatureFlagType
  - io.jans.fido2.model.conf.Fido2Configuration
  - io.jans.scim.model.conf.AppConfiguration
