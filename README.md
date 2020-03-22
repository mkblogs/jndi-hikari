# Hikari Implementation of JNDI DataSource
In this example, read the `db.properties` file and created JNDI DataSource using Tomcat JNDI Context
## Setting for JNDI Context
```java
 protected void postProcessContext(Context context) {
	 	log.info("in side post process");
        ContextResource resource = new ContextResource();
        resource.setName(jndiName);
        resource.setProperty("factory", "com.zaxxer.hikari.HikariJNDIFactory");
        resource.setProperty("auth", "Container");
        resource.setType(DataSource.class.getName());
		resource.setProperty("driverClassName", driverClassName);
		resource.setProperty("jdbcUrl", url);
		resource.setProperty("username", username);
		resource.setProperty("password", password);
        context.getNamingResources().addResource(resource);
    }
```
## Getting from JNDI Context
```java
 JndiDataSourceLookup dsLookup = new JndiDataSourceLookup();
 dsLookup.setResourceRef(true);
 DataSource dataSource = dsLookup.getDataSource(jndiName);
```
```java
 @Value("${spring.datasource.jndi-name}")
 private String jndiName;
```	 
### application.yml
```yaml
spring:
  datasource:
   jndi-name: jdbc/MysqlJNDI
```
