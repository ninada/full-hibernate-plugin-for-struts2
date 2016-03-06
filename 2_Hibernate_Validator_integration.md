# Introduction #

Hibernate Validator is a fantastic validation framework. Following the DRY (Don't Repeat Yourself) principle, Hibernate Validator let's you express your domain constraints once (and only once) and ensure their compliance at various level of your system automatically.

Annotations are a very convenient and elegant way to specify invariant constraints on the domain model implementation, the persistent classes. Hibernate Validator comes bundled with a set of common validations (@NotNull, @Email, @Max, and so on), and you can build you own validation rules very easily.

**This plugin is compatible with _Hibernate Validator 4 (since version 2.2 GA)_**

More about this framework at http://www.hibernate.org/412.html

Hibernate Validator Manual:<br />
[PDF version](http://www.hibernate.org/hib_docs/validator/reference/en/pdf/hibernate_validator.pdf)<br />
[HTML version](http://www.hibernate.org/hib_docs/validator/reference/en/html_single/)



&lt;hr/&gt;


# Usage #

At first, **[install](http://code.google.com/p/full-hibernate-plugin-for-struts2/wiki/Installation)** the plugin. <br />

Do not use
```
validate="true" 
```
in your JSPs (

&lt;s:form&gt;

**tag).**

This capability can be used to validate Entity class POJOs or simple fields in Actions. Like in Struts2 default validation methods, an **_input_** result is required when validation fails.


## Validating Entity POJOs ##

If you have an Entity class with specific validation annotations, just use the _@Valid_ annotation over a declaration or a setter method of this in the Action!

_Example:_



&lt;hr/&gt;


<u>Entity class</u>: **Soccerplayer.java**
```
    public class Soccerplayer implements java.io.Serializable {

        private Integer idplayer;
	
	@NotNull
	@Valid
	private Soccerteam soccerteam;
	
	@NotEmpty
	@Length(min=2, max=20)
	private String name;
	
	@NotNull
	@Past
	private Date birthdate;
	
	@Min(value=1)
	@Max(value=2)
	private Float height;
	
	@Length(max=100)
	private String notes;

        // ... getters and setters ...
    }
```
<font color='red'><b>=> <i>Validation annotations as need...</i></b></font><br />
**Important:**_You can use Hibernate Validator annotations when using XML mapping files and in JPA/EJB annotated Entity classes. In both cases this plugin works fine._ <br />
Note that there is no error message configured. What messages will be generated? Wait and continue reading this page...




&lt;hr/&gt;


<u>Struts XML mapping file</u>: **struts.xml**
```
    <?xml version="1.0" encoding="UTF-8" ?>
    <!DOCTYPE struts PUBLIC
    "-//Apache Software Foundation//DTD Struts Configuration 2.0//EN"
    "struts-2.0.dtd">
    <struts>

      <package name="main" extends="hibernate-default">
    
	<action name="savePlayer" class="SoccerplayerAction" method="save">
    	    <result name="input">/form.jsp</result>
    	    <result type="redirect-action">listPlayer</result>
    	</action>

    	<action name="listPlayer" class="SoccerplayerAction" method="list">
    	    <interceptor-ref name="basicStackHibernate"/>
    	    <result>/list.jsp</result>
    	</action>

    	<action name="deletePlayer" class="SoccerplayerAction" method="delete">
            <interceptor-ref name="basicStackHibernate"/>
    	    <result>/list.jsp</result>
    	</action>

      </package>

    </struts>
```
<font color='red'><i>=> <b>The package extends</b><u>hibernate-default</u>. This is REQUIRED!</i>**</font>. The default interceptor stack when you extends this package is**defaultStackHibernate**, that is the responsable by the validation.**<br />
**Note that you have to create a**<u>input</u> result (just like when using Struts2 default validation method).<br />
**listPlayer** and **deletePlayer** mappings use **basicStackHibernate** interceptor because don't need validation but need Hibernate access (Session and/or Transaction). See more details about **Hibernate Core Sessions and Transactions injection capability [Here](http://code.google.com/p/full-hibernate-plugin-for-struts2/wiki/Hibernate_Core_Sessions_Transactions_injecton)**.




&lt;hr/&gt;


<u>Struts Properties file</u>: **struts.properties**
```
    hibernatePlugin.sessionTarget=hibernateSession
    hibernatePlugin.transactionTarget=hibernateTransaction
```
Look: At **SoccerplayerAction.java** (next file) there are a Hibernate Session object (**hibernateSession**) and a Hibernate Transaction object (**hibernateTransaction**) with their Assessors methods (getters and setters). <br />
This example uses the Hibernate Session Factory class from plugin, so just this 2 properties are need.
<br />See more details about **Hibernate Core Sessions and Transactions injection capability [Here](http://code.google.com/p/full-hibernate-plugin-for-struts2/wiki/Hibernate_Core_Sessions_Transactions_injecton)**.




&lt;hr/&gt;


<u>Action class</u>: **SoccerplayerAction.java**
```
    public class ManagePlayersAction extends ActionSupport{
	
	@Valid
	Soccerplayer player = new Soccerplayer();
        
        org.hibernate.Session hibernateSession;

        org.hibernate.Transaction hibernateTransaction;
    
        // ... getters, setters and action methods ( ie. execute() ) ...

    }
```
<font color='red'><b>=> <i>@Valid over the POJO to be validated...</i></b></font>
In this Action, the **player** object will be validated in every request that use the **defaultStackHibernate** (default interceptor stack if the package extends **hibernate-defaults**). If requests to this action that don't use this stack no hibernate validation will be done.
This Action could be used with annotations for Session and Transaction. Like this
```
     import com.googlecode.s2hibernate.struts2.plugin.annotations.SessionTarget;
     import com.googlecode.s2hibernate.struts2.plugin.annotations.TransactionTarget;

     ...

     @SessionTarget
     org.hibernate.Session hibernateSession;

     @TransactionTarget
     org.hibernate.Transaction hibernateTransaction;

     ...
```
In this case, **hibernatePlugin.sessionTarget** and **hibernatePlugin.transactionTarget** properties at **struts.properties** would not be necessary.<br />
**Version 1.1+**: Setters are not required for this fields (EJB3 like), but if you create this in Java Bean default, will be used.<br />




&lt;hr/&gt;


<u>JSP file</u>: **form.jsp**
```
    <%@ taglib uri="/struts-tags" prefix="s" %>

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
    
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head>
    <s:head/>
    <title>Soccer Players</title>
    </head>
    <body>	
	<s:url id="urlList" action="listPlayer"></s:url>
	<s:a theme="ajax" href="%{urlList}" targets="divIntern" indicator="indicator" showLoadingText="false">List All Players</s:a>

	<s:form action="savePlayer">
		<s:hidden name="player.idplayer"></s:hidden>
		<s:textfield key="player.name"></s:textfield>
		<s:textfield key="player.birthdate"></s:textfield>
		<s:textfield key="player.height"></s:textfield>
		<s:textarea key="player.notes" cols="50" rows="3"></s:textarea>
		<s:select list="teamsList" name="player.soccerteam.idteam" label="Team"
		 listKey="idteam" listValue="name"
		 headerKey="" headerValue="- What Team? -"></s:select>
		<s:submit value="Save" />
	</s:form>

    </body>
    </html>
```
<font color='red'><b>=> <i>Input fields here use keys for the automatic generation of label and name attributes... but not just this: Please, pay attention to this keys...</i></b></font>




&lt;hr/&gt;


**I18N messages file: SoccerplayerAction.properties
```
    player.name=Player Name
    player.birthdate=Birth
    player.height=Height (m)
    player.notes=Notes about this Player
    player.soccerteam.idteam=Team
```**<font color='red'><b>=> <i>Please, pay attention to this keys...</i></b></font>

<font color='red'><b>=> <i>Ok, did you pay attention to the keys?</i></b></font>

Now, look to the result...

Form before submit: <br />
<img src='http://lh3.ggpht.com/_BudW2b3yOHU/ShP02Ub6vZI/AAAAAAAAABk/5JG8RA12hLI/formSoccerPlayersBeforeSubmit.JPG' border='1' /> <br />
The messages are provided by Hibernate Validator!

<br />

Form AFTER submit and validation:<br />
<img src='http://lh6.ggpht.com/_BudW2b3yOHU/ShP02TyVExI/AAAAAAAAABo/gBOwfv5N7DE/formSoccerPlayersAfterSubmit.JPG' border='1' />

Did you see that the validation message had the field label as prefix? This Plugin try to use a I18N key for this! How?
If the Entity class reference at the Action is **player**, so the Value Stack keys for this will be:
  * player.name
  * player.birthdate
  * player.height
  * player.notes
  * player.soccerteam.idteam

**_So, there is another DRY pratice here!_**

_Do i need to use message keys to use this capability?_<br />
**NO.** If no key acording the Value Stack item name key found, the message WILL BE created BUT **without** the field label.
The result would be this: <br />
<img src='http://lh6.ggpht.com/_BudW2b3yOHU/ShP3SEa-I-I/AAAAAAAAABs/95ofRnvpAnY/formSoccerPlayersAfterSubmitNoLabel.JPG' border='1' />



## Validate Simple Fields in the Action ##

You can validate simple fields in the Action using Hibernate Validator Annotations!

_Example:_

**Action class: MySimpleAction.java**
```
    public class MySimpleAction extends ActionSupport {

        private Integer myFieldNotValidated;
	
	@NotEmpty
	@Length(min=2, max=20)
	private String myValidatedField1;
	
	@NotNull
	@Past
	private Date myValidatedField2;
	
        // ... getters and setters for this 3 fields ...
    }
```
In this Action, there are 3 fields, but just 2 will be validated in requests (if using the **defaultStackHibernate**).




&lt;hr/&gt;


# Details _(FAQ style)_ #

**Q1:**<font color='navy'>My Entity class has 10 fields with Hibernate Validator annotations, but in a specific Action in my project i would like to submit and only 3 field of this class. What can i do?</font><br />
**A1:** Peace of cake! This plugin validates only fields in the request. In the case on question, if the 3 fields pass in validation, the action will run fine.


**Q2:**<font color='navy'>I have an Entity class object with Hibernate Validator annotations in my Action. But this Action has 2 mapped urls. In one of this i need validation and in the other, not. What can i do?</font><br />
**A2:** This plugin has an interceptor stack that do not validate: **basicStackHibernate**. This one only use the Hibernate Core session and transaction injections.

**Q3:**<font color='navy'>What about Struts2 validations (annotations and XML)?</font><br />
**A3:** This plugin has 3 interceptor stacks:
  * **basicStackHibernate**: Like Struts2 **basickStack** (NO validations here!), but with Hibernate Core session and transaction injections capability.<br />
  * **defaultStackHibernate**: Like Struts2 **defaultStack**, but _DO NOT USE_ Struts2 validation methods (annotation and XML). Uses Hibernate Validation framework instead.<br />
  * **defaultStackHibernateStrutsValidation**: Struts2 **defaultStack** + plugin **basicStackHibernate**.


**Q4:**<font color='navy'>My clients don't speak english! How can I translate validation messages?</font><br />
**A4:** Peace of cake! This plugin access the default messages files from Hibernate Validator framework. Hibernate validator has messages in 13 languages (cs, da, de, en, es, fr, it, ja, nl, pt\_BR, sv, zh\_CN, zh\_TW). But if you want to use custom messages, create a ValidatorMessages`_`??.properties in your default java package.
<br />**Note:**_Versions_<u>2.0.14</u> and <u>2.1.6</u> of Struts 2: **Client Locale X-Work Bug**: [Issue WW-3027](https://issues.apache.org/struts/browse/WW-3027)


**Q5:**<font color='navy'>Talking about messages... What about if i want to use a super custom validation message?</font><br />
**A5:** Just use the **message** attribute present in all Hibernate Validator annotations. You can use a I18N key or a message directly.

**Example:**
```
    public class MyBuduiaAction extends ActionSupport{
	
        // The plugin will look for a I18N key "error_field_not_empty_because_i_want".
        // If not found, the message will be "error_field_not_empty_because_i_want", literally
        @NotEmpty(message="error_field_not_empty_because_i_want");
	String myFieldValidateWithKey;
 	
        // The plugin will use the message "Hey, guy... What about write some word here?"
        @NotEmpty(message="Hey, guy... What about white some word here?");
	String myFieldValidateWithKey;     
        // other methods...
    }
```

This resource can be used when validate simple fields (like the example above) or Entity POJOs in Actions.


**Q6:**<font color='navy'>I'm using Hibernate Core with XMLs mapping files. If i use just Hibernate Validator annotations in my Entity classes, will the validation go on?</font><br />
**A6:** YES. In your Entity classes you can use just Hibernate Validator annotations or Hibernate Entity / EJB Annotations two.


**Q7:**<font color='navy'>I have done every thing perfect! Why validations are not been done?!?</font><br />
**A7:** The actual version of this plugin can use the Hibernate Validator capability only in Actions that 'ISA' ActionSupport. Otherwise validation will be ignored!