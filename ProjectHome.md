## Full Hibernate Plugin 2.2.2 GA Released _(11 nov 2010)_ ##
([Release Notes page](http://code.google.com/p/full-hibernate-plugin-for-struts2/wiki/6_Release_Notes))

## Alternative Tutorial [Here](http://www.vaannila.com/struts-2/struts-2-tutorial/struts-2-tutorial.html) ##

## Hibernate Validator integration ##
**_DRY - Don't Repeat Yourself!_**

This feature allow the use of the fantastic Hibernate Validator Framework with very simple use of annotations in your Actions. This plugin is compatible with _Hibernate Validator 3.1.0_ and _4.0.2_ (since 2.2 version).

More about Hibernate Validator at http://www.hibernate.org/412.html

<br />

## Hibernate Core Sessions injection capability ##
**_The Open Session in View pattern made easy_**

This feature provides an Interceptor that open and sets in the value stack a Hibernate Core Session and closes (or not) this after the results are rendered for the client.

Very easy to use: Using the **@SessionTarget** Annotation or some XML lines.
This feature follows the concepts in http://www.hibernate.org/43.html

**Important!** _**[hibernatesession-plugin-for-struts2](http://code.google.com/p/hibernatesession-plugin-for-struts2/)** users: You are strongly encouraged to migrate for this plugin!_

<br />

## Hibernate Transactions injection capability ##
**_Transactions by request_**

This feature provides an Interceptor that opens and sets in the value stack a Transaction and commit this after the results are rendered for the client if a rollback method was not invoked.

You can configure multiple databases (2.0+).

Very easy to use: Using the **@TransactionTarget** Annotation or some XML lines.

<br />

## Hibernate Core configuration management Web Tool ##
**_Manage, reload and test your Hibernate Core configurations without reload your web content_**

This feature provides an WEB front-end tool for view and reload your Hibernate Core configurations.

You can provide this tool in your context in a public way or protect this by 2 ways: IPs/Hosts list or HTTP Autentication.

<br />


<a href='https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=2SC696DUFMKPG'><img src='http://www.avalihc.com.br/v01/donate.PNG' border='0' width='180' title="Make a donation to this project. The owner says 'Thank you very much!'"></img></a>