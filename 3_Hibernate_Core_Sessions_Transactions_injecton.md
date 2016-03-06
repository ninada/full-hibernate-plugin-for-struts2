# Introduction #

This feature provides an Interceptor that open and sets in the value stack a Hibernate Core Session and closes (or not) this after the results are rendered for the client. The same Interceptor opens and sets in the value stack a Transaction and commit this after the results are rendered for the client if a rollback method was not invoked.

No code lines need to be added to manage Hibernate sessions in Struts 2 projects. Only some XML (or .properties) lines needed.

This feature follows the concepts in http://www.hibernate.org/43.html

**Important!** _**[hibernatesession-plugin-for-struts2](http://code.google.com/p/hibernatesession-plugin-for-struts2/)** users: You are strongly encouraged to migrate for this plugin!_




&lt;hr/&gt;


# Usage #

At first, **[install](http://code.google.com/p/full-hibernate-plugin-for-struts2/wiki/Installation)** the plugin. <br /><br />

If you want to use the Hibernate Core Sessions and Transactions injection capability, your(s) mapping package(s) <u>need</u> to extend the package _**hibernate-default**_.
So, you have to use some configuration properties in **struts.xml** or **struts.properties**.
This properties are:

  * **hibernatePlugin.sessionTarget**: Comma-separated Hibernate Session Target in the Action ValueStack. This property can be used in 2 ways:
    1. Simple values. Examples: myHibSession, myHibSession2; hibSession; myDao.session, myDao2.session
    1. Values using Wildcard. Examples: **Dao.session;**Facade.hibernateSession
> This property is **Optional**.

&lt;hr/&gt;




  * **hibernatePlugin.transactionTarget**: Comma-separated Hibernate Transaction Target in the Action ValueStack. This property can be used in 2 ways:
    1. Simple values. Examples: myHibTransaction, myHibTransaction2; hibernateTransaction; myDao.transaction, myDao2.transaction
    1. Values using Wildcard. Examples: **Dao.transaction;**Facade.hibernateTransaction
> This property is **Optional**.

&lt;hr/&gt;




  * **hibernatePlugin.configurationFiles**:  Comma-separated Hibernate Configuration file names. Note that if <b>hibernatePlugin.customSessionFactoryClass</b> property is used that is not guarantee about the using of the files named here.<br />
> This property is **Optional**. Default <b>/hibernate.cfg.xml</b>.

&lt;hr/&gt;



  * **hibernatePlugin.autoRebuild** (**version 2.0+**): Define if the Full Hibernate Plugin's Session Factory will rebuild all configured SessionFactories when an org.hibernate.exception.JDBCConnectionException is thrown. Use **true** or **false**.<br />
> This property is **Optional**. Default <b>true</b>.

&lt;hr/&gt;



  * **hibernatePlugin.configurationType** (**Deprecated since 1.2**): Hibernate Configuration Type. Values: <b>xml</b> or <b>annotation</b>. <br />Note that if <b>hibernatePlugin.customSessionFactoryClass</b> property is used that is not guarantee about the using of the configuration type named here. <br />This property is **Optional**. Default <b>xml</b>. 

&lt;hr/&gt;




  * **hibernatePlugin.customSessionFactoryClass**: Full qualified name of the custom class used as a Hibernate Session Factory.
> This property is **Optional**. If not used, the Hibernate Plugin will use an internal Session Factory Class (com.googlecode.s2hibernate.struts2.plugin.util.HibernateSessionFactory).

&lt;hr/&gt;




  * **hibernatePlugin.getSessionMethod**: Method used to get the Hibernate Session from the Session Factory class configured at <b>hibernatePlugin.customSessionFactoryClass</b>.
> Examples: <i>getSession</i>; <i>getHibernateSession</i>
> <br /><b>Optional</b>, but <b>Required</b> if <b>hibernatePlugin.customSessionFactoryClass</b> property is used.

&lt;hr/&gt;




  * **hibernatePlugin.rebuildSessionFactoryMethod**: Public method from the Hibernate Session Factory class for rebuild configurations. <br /><b>Optional</b>, but <b>Required</b> if <b>hibernatePlugin.customSessionFactoryClass</b> property is used.

&lt;hr/&gt;




  * **hibernatePlugin.staticGetSessionMethod**: Is the method used to get the Hibernate Session static? If <b>true</b> the method if used in static mode (ie. <i>MySessionFactoryClass.getSession()</i>).<br /> If <b>false</b> the Hibernate Plugin will instantiate the Session Factory class. <br /><b>Optional</b>, but <b>Required</b> if <b>hibernatePlugin.customSessionFactoryClass</b> property is used. <br />Default <b>true</b>.

&lt;hr/&gt;





  * **hibernatePlugin.closeSessionMethod** (version 1.1+): Method used to CLOSE the Hibernate Session from the Session Factory class configured at <b>hibernatePlugin.customSessionFactoryClass</b>.
> Example: <i>closeSession</i>
> <br /><b>Optional</b>, but <b>Required</b> if <b>hibernatePlugin.customSessionFactoryClass</b> property is used.

&lt;hr/&gt;





  * **hibernatePlugin.useSessionObjectInCloseSessionMethod** (version 1.1+): Indicates the use of the Hibernate Session Object as parameter in close session method at the Session Factory class configured at <b>hibernatePlugin.customSessionFactoryClass</b>.
> <br />Use **true** or **false**
> <br /><b>Optional</b>.
> <br />Default <b>true</b>.



  * **hibernatePlugin.staticRebuildSessionFactoryMethod**: Set the access mode of the rebuild Session Factory method of the Session Factory class configured at <b>hibernatePlugin.customSessionFactoryClass</b>.<br />If <b>true</b> the method if used in static mode (ie. <i>MySessionFactoryClass.rebuildMySessionFactory()</i>).<br />  If <b>false</b> the Hibernate Plugin will instantiate the Session Factory class. <br /><b>Optional</b>, but <b>Required</b> if <b>hibernatePlugin.customSessionFactoryClass</b> property is used. Default <b>true</b>.

&lt;hr/&gt;




  * **hibernatePlugin.closeSessionAfterInvoke**:If <b>true</b>, the Hibernate Session of the request will be closed after the response. <br />If <b>false</b>, the Hibernate Session of the request WILL NOT be closed after the response. <br /><b>Optional</b>. Default <b>true</b>.

&lt;hr/&gt;




  * **hibernatePlugin.searchMappingsInsideJars** (version 2.1.1+):If <b>true</b>, @SessionTarget and @TransactionTarget will be searched in Jar files (performance will decrease). Use <b>true</b> only if you have one of these annotations in classes inside Jar files.<br /><b>Optional</b>. Default <b>false</b>.

&lt;hr/&gt;






## Easiest configuration ##

If you do not use a custom class as a Hibernate Session Factory and don't want to disable auto close sessions function, you will need to use just <u>2</u> properties in your project:
**hibernatePlugin.sessionTarget** and **hibernatePlugin.transactionTarget**.
<br />Look an example **[here](http://code.google.com/p/full-hibernate-plugin-for-struts2/wiki/Hibernate_Validator_integration)**.
Instead, you can use the **Annotations configuration**.


## Annotations configuration ##

You can use annotations over your **session** and **transaction** objects:<br />
**@SessionTarget** (for Hibernate Session objects)<br />
**@TransactionTarget** (for Transaction objects)<br />
This feature can be used with the **hibernatePlugin.sessionTarget** and **hibernatePlugin.transactionTarget** configuration properties. If both are used (annotations and properties), both will be used by the plugin.><br />
This annotations can be used in Actions or in any class in your project (DAOs, Facades...).
<br />Look an example **[here](http://code.google.com/p/full-hibernate-plugin-for-struts2/wiki/Hibernate_Validator_integration)**.



&lt;hr/&gt;


# More details about "hibernate-default" package #

This plugin provides a mapping package called _**hibernate-default**_. And this has 3 interceptor stacks indicated for general use:

  * **basicStackHibernate**: Like Struts2 basickStack (NO validations here!), but with Hibernate Core session and transaction injections capability. <br /><br />
  * **defaultStackHibernate**: Like Struts2 defaultStack, but DO NOT USE Struts2 validation methods (annotation and XML). Uses Hibernate Validation framework instead.<br /><br />
  * **defaultStackHibernateStrutsValidation**: Struts2 defaultStack + plugin basicStackHibernate. <br /><br />

This package extends the _**hibernate-default**_ package, so all default Struts2 configurations can be used if you need.

_**hibernate-default**_ package is abstract, so you can extends this with other. Example:
```
  ...
  <package name="principal" extends="hibernate-default,jasperreports-default,json-default" >
  ...
```




&lt;hr/&gt;


# The Hibernate Core Session Factory #

This plugin provides a powerfull Hibernate Core Session Factory class. <br />
The class is **com.googlecode.s2hibernate.struts2.plugin.util.HibernateSessionFactory**. <br />
If you <u>do not</u> configure a <u>custom</u> Hibernate Core Session Factory class, you can use this methods:
  * **getSession()**: Get the current thread's Hibernate Core Session<br /><br />
  * **closeSession()**: Close the current thread's Hibernate Core Session<br /><br />
  * **getNewSession()**: Get an "isolated" Hibernate Core Session<br /><br />
  * **rebuildSessionFactory()**: Reload the session factory configurations according the configuration files<br /><br />
  * **destroyFactory()**: Destroy Session Factory. _In Web Applications with Hibernate, when the context is reload, it's necessary to destroy the session factory to evict problems with connection pools like C3P0_.
  * **getSessionFactory(String sessionFactoryName)**: Returns one of the configured SessionFactories (version 2.0+)