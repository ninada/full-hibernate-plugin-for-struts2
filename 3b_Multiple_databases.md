# Example #

## Hibernate configuration file #1 ##
**Name:** hibernate.mysql.cfg.xml <br />
**Package:** pkc1.hibConfigs <br />
**Content**:<br />
```
<hibernate-configuration>
  <session-factory name="sfMySql">  <!-- look here -->
	<property name="hibernate.connection.driver_class">com.mysql.jdbc.Driver</property>
	<property name="hibernate.connection.password">mypasswd</property>
	<property name="hibernate.connection.url">jdbc:mysql://localhost:3306/mydatabase</property>
	<property name="hibernate.connection.username">mylogin</property>
	<property name="hibernate.dialect">org.hibernate.dialect.MySQLDialect</property>

	<mapping resource="model/Soccerplayer.hbm.xml" />
	<mapping resource="model/Soccerteam.hbm.xml" />
	<!-- others... -->
	</hibernate-configuration>
</session-factory>
```

## Hibernate configuration file #2 ##
**Name:** hibernate.postgres.cfg.xml <br />
**Package:** pkc1.hibConfigs <br />
**Content**:<br />
```
<hibernate-configuration>
  <session-factory name="sfPostgres"> <!-- look here -->
	<property name="hibernate.connection.driver_class">org.postgresql.Driver</property>
	<property name="hibernate.connection.password">mypasswd</property>
	<property name="hibernate.connection.url">jdbc:postgresql://localhost/mydatabase</property>
	<property name="hibernate.connection.username">mylogin</property>
	<property name="hibernate.dialect">org.hibernate.dialect.PostgreSQLDialect</property>

	<mapping resource="model/User.hbm.xml" />
	<!-- others... -->
	</hibernate-configuration>
</session-factory>
```

**Configuring these two classes:**<br />
**struts.propeties**
```
 hibernatePlugin.configurationFiles=/pkc1/hibConfigs/hibernate.mysql.cfg.xml,/pkc1/hibConfigs/hibernate.postgres.cfg.xml
```

**struts.xml**
```
 <constant name="hibernatePlugin.configurationFiles" value="/pkc1/hibConfigs/hibernate.mysql.cfg.xml,/pkc1/hibConfigs/hibernate.postgres.cfg.xml"></constant>
```

# Using annotations #

## If using a single Hibernate configuration (only one configurantion file) ##

Hibernate Core Session:
```
  @SessionTarget
  org.hibernate.Session session;
```

Transaction:
```
  @TransactionTarget
  org.hibernate.Transaction transaction;
```


## If using a single multiple Hibernate configuration (multiple one configurantion files, like the two above) ##

Hibernate Core Session:
```
  @SessionTarget("sfMySql") // the same of the *name* attribute of tag *<session-factory>* from the hibernate configuration file
  org.hibernate.Session session1;


  @SessionTarget("sfPostgres") // the same of the *name* attribute of tag *<session-factory>* from the hibernate configuration file
  org.hibernate.Session session2;
```

Transaction:
```
  @TransactionTarget("session1") // this transaction will be retrieved from *session1* object in the same class
  org.hibernate.Transaction1 transaction1;


  @TransactionTarget("session2") // this transaction will be retrieved from *session2* object in the same class
  org.hibernate.Transaction2 transaction2;
```


<font color='red'><b>Note:</b></font> The Full Hibernate Plugin's Session Factory Class sets the SessionFactory from the first configuration file as the default. So, in the example, the **sfMySql** would be the default. So, for inject a Session from this SessionFactory we should do just...
```
  @SessionTarget // the *sfMySql* will be used
  org.hibernate.Session session1;
```


<font color='red'><b>Note2:</b></font> If just one Session object is setted at the @TransactionTarget, the first Session object found in the classe will be used. So...

```
  @SessionTarget("sfMySql") 
  org.hibernate.Session sessionA;


  @SessionTarget("sfPostgres")
  org.hibernate.Session sessionB;

  @TransactionTarget // this transaction will be retrieved from *sessionA* object
  org.hibernate.Transaction2 transaction;
```