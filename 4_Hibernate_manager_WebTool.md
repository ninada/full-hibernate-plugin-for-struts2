# Introduction #

This feature provides an WEB front-end tool for view, reload and test your Hibernate Core configurations.

Yout can provide this tool in your context in a public way or protect this by 2 ways: IPs/Hosts list or HTTP Autentication.



&lt;hr/&gt;


# Usage #

At first, **[install](http://code.google.com/p/full-hibernate-plugin-for-struts2/wiki/Installation)** the plugin. <br /><br />

To access the Web Tool, use the url **_/your\_context/hibernateManager/index.action_**



&lt;hr/&gt;


## Screenshots ##

**Main Page:**<br />
<img src='http://lh5.ggpht.com/_BudW2b3yOHU/SyfWdWjIJ0I/AAAAAAAAANo/dNL04xSBy78/s720/fhp_wtm01.PNG' /> 

&lt;hr/&gt;



**Click in configuration(s) file(s):**<br />
<img src='http://lh5.ggpht.com/_BudW2b3yOHU/SyfWdebU1zI/AAAAAAAAANs/LSIqeSwx9og/s800/fhp_wtm02.PNG' /> 

&lt;hr/&gt;



**After reload Hibernate Configurations:**<br />
<img src='http://lh5.ggpht.com/_BudW2b3yOHU/SyfWdQfgeLI/AAAAAAAAANw/5_zmKr5c_SE/s576/fhp_wtm03.PNG' /> 

&lt;hr/&gt;



**Test JDBC Connection (2.1.1+):**<br />
<img src='http://lh5.ggpht.com/_BudW2b3yOHU/SyfWdo3vMiI/AAAAAAAAAN0/mclDVgABF9k/s576/fhp_wtm04.PNG' /> 

&lt;hr/&gt;





&lt;hr/&gt;


# Security Configurations #

## IPs list ##

Configuration property: **hibernatePlugin.manager.validIpsHosts**<br />
Comma-separated IP numbers or host names that can access the Hibernate Manager Web Tool.
This property is **Optional**. Default **127.0.0.1** (the famous _localhost_);

<i>Examples: 10.1.0.3, myhost, admim.mydomain, pc1.mydomain.com </i>


## HTTP Autentication Security ##

Configuration property: **hibernatePlugin.manager.httpAuhtRoles**<br />
Comma-separated roles that can access the Hibernate Manager Web Tool.
<i>Example: manager, admin</i>
This property is **Optional**.


## Public Access ##

Configuration property: **hibernatePlugin.manager.publicAccessEnabled**<br />
If you want to allow public access to this tool, use the value **true** here.
This property is **Optional**. Default **false**.




&lt;hr/&gt;


# Optional Configurations #

If you want to use a custom class as Hibernate Session Factory, you have to use some configuration in your **struts.xml** or **struts.properties**.

  * **hibernatePlugin.customSessionFactoryClass**: Full qualified name of the custom class used as a Hibernate Session Factory. <br />This property is **Optional**. If not used, the Hibernate Plugin will use an internal Session Factory Class (com.googlecode.s2hibernate.struts2.plugin.util.HibernateSessionFactory).

&lt;hr/&gt;




  * **hibernatePlugin.rebuildSessionFactoryMethod**: Public method from the Hibernate Session Factory class for rebuild configurations. <br /><b>Optional</b>, but <b>Required</b> if <b>hibernatePlugin.customSessionFactoryClass</b> property is used.

&lt;hr/&gt;




  * **hibernatePlugin.staticRebuildSessionFactoryMethod**: Set the access mode of the rebuild Session Factory method of the Session Factory class configured at <b>hibernatePlugin.customSessionFactoryClass</b>.<br />If <b>true</b> the method if used in static mode (ie. <i>MySessionFactoryClass.rebuildMySessionFactory()</i>).<br />  If <b>false</b> the Hibernate Plugin will instantiate the Session Factory class. <br /><b>Optional</b>, but <b>Required</b> if <b>hibernatePlugin.customSessionFactoryClass</b> property is used. Default <b>true</b>.

&lt;hr/&gt;

