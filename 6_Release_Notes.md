## Version 2.2.2 GA (_11 nov 2010_) ##


  * _Bug fix_: <a href='http://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=27&can=1'><a href='https://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=27'>Issue 27</a></a> fixed.

  * _Bug fix_: <a href='http://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=28&can=1'><a href='https://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=28'>Issue 28</a></a> fixed.


## Version 2.2.1 GA (_11 sep 2010_) ##


  * _Bug fix_: <a href='http://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=10&can=1'><a href='https://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=20'>Issue 20</a></a> fixed.



## Version 2.2 GA (_08 mar 2010_) ##


  * _Bug fix_: <a href='http://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=8&can=1'><a href='https://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=8'>Issue 8</a></a> fixed (Hibernate Validator 4 compatible).

  * _Bug fix_: <a href='http://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=18&can=1'><a href='https://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=18'>Issue 18</a></a> fixed.

  * _Improvement_: Messages Cache for Hibernate Validator Messages.


## Version 2.1.3 GA (_19 jan 2010_) ##


  * _Bug fix_: <a href='http://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=10&can=1'><a href='https://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=10'>Issue 10</a></a> fixed.


  * _Bug fix_: <a href='http://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=12&can=1'><a href='https://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=12'>Issue 12</a></a> fixed.


  * _Bug fix_: <a href='http://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=13&can=1'><a href='https://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=13'>Issue 13</a></a> fixed.


  * _Bug fix_: <a href='http://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=14&can=1'><a href='https://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=14'>Issue 14</a></a> fixed.


  * _Bug fix_: <a href='http://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=15&can=1'><a href='https://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=15'>Issue 15</a></a> fixed.


## Version 2.1.2 GA (_17 dec 2009_) ##


  * _Bug fix_: <a href='http://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=9&can=1'><a href='https://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=9'>Issue 9</a></a> fixed.


## Version 2.1.1 GA (_15 dec 2009_) ##


  * _Bug fix_: <a href='http://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=7&can=1'><a href='https://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=7'>Issue 7</a></a> fixed.
  * _New Feature_: JDBC Connection Test by Hibernate Configuration file at **Hibernate Manager Web Tool**
  * _Improvement_: Better performance at Hibernate Core Session and Transaction injection by Annotations ([read about](http://code.google.com/p/full-hibernate-plugin-for-struts2/wiki/3_Hibernate_Core_Sessions_Transactions_injecton) the new "hibernatePlugin.searchMappingsInsideJars" property).



## Version 2.1 GA (_20 nov 2009_) ##


  * _Bug fix_: <a href='http://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=4&can=1'><a href='https://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=4'>Issue 4</a></a> fixed.
  * _Bug fix_: <a href='http://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=5&can=1'><a href='https://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=5'>Issue 5</a></a> fixed.
  * _Bug fix_: <a href='http://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=6&can=1'><a href='https://code.google.com/p/full-hibernate-plugin-for-struts2/issues/detail?id=6'>Issue 6</a></a> fixed.
  * _Improvement_: **C3P0** Pooled Datasources are closed and destroyed when **destroyFactory()** method is invoked from **com.googlecode.s2hibernate.struts2.plugin.util.HibernateSessionFactory**



## Version 2.0 Beta (_21 oct 2009_) ##


  * _Bug fix_: Debug messages from plugin's Intercetors not displayed.
  * _New Feature_: The Plugin's Hibernate Session Factory now can work with multiple database servers simultaneity (multiple Session Factories)
  * _New Feature_: Dynamic search and configuration of Hibernate properties files (multiple Hibernate properties files allowed)
  * _New Feature_: Auto Rebuild SessionFactories when an org.hibernate.exception.JDBCConnectionException occurs
  * _New Feature_: Spanish messages (Thanks to Nacho Marijuan).
  * _Improvement_: Faster algorithm for Session/Transaction Injection.
  * _Improvement_: More and Betters debug messages.



## Version 1.5 GA (_27 aug 2009_) ##


  * _Improvement_: Objects with Session and Transaction targets (ie. DAOs) can be instantiated inside Action methods.
  * _Improvement_: Better log messages for debugging.
  * _New Feature_: German messages (Thanks to Johannes Geppert).


## Version 1.4 GA (_30 jul 2009_) ##


  * _Bug Fix_: Hibernate Core Sessions are closed and Transactions are rolled back when a unexpected exception is throwed by the Action.
  * _New Feature_: The internal Hibernate Core Session Factory class now has a method to get a new Hibernate Core Session, NOT the Session of the current thread (HTTP request).
  * _Improvement_: Better log messages.


## Version 1.3 GA (_09 jul 2009_) ##


  * _Bug Fix_: Wrong messages about Session and Transaction injection. **Still doing** the injection, sometimes the message _"Target not found..."_ appears.


## Version 1.2 GA (_07 jul 2009_) ##


  * _New Feature_: Auto detect Hibernate Mapping Type. The Plugin detects if your project uses XML or Annotations mapping. **hibernatePlugin.configurationType** property is Deprecated. Not necessary from this version on.
  * _Bug Fix_: When the tag _<s:action_ used with the attribute _executeResult="true"_ a NullPointerExpection is throwed.
  * _Bug Fix_: Session and Transaction objects can be in superclasses (ie. a "GenericDAO") when using annotations


## Version 1.1 GA (_05 jul 2009_) ##


  * _New Feature_: EJB3 like access for the annotated Session and Transaction fields. Setters are optional now and used only if exists
  * _New Feature_: Close session method can be configured for custom Session Factory class
  * _Bug Fix_: Bug when test the connection for Oracle, MS SQL Server and Firebird/Interbase - thanks to _Nacho Marijuan_
  * Better Hibernate Core Session Factory, using the Thread Local Pattern (https://www.hibernate.org/207.html)


## Version 1.0 GA (_11 jun 2009_) ##


  * _New Feature_: Hibernate Core Session injection by annotation
  * _New Feature_: Transaction injection by annotation
  * _Class change_: The **com.googlecode.s2hibernate.struts2.plugin.s2hibernatesession.HibernateSessionInterceptor** in 1.0 Beta version now is **com.googlecode.s2hibernate.struts2.plugin.interceptors.SessionTransactionInjectorInterceptor**