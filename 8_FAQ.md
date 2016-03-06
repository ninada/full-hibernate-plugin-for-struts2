### 1. I was using the Hibernate Session Plugin. Do I need to migrate? ###

The Hibernate Session Plugin will be depreated. Will not be continued. The Full Hibernate Plugin contain the the Hibernate Session injection feature and much more.

### 2. I want to use only Session and Transaction injection features but not the Hibernate Validator feature. Can I do it? ###

Yes. The are 4 ways:

1. Using the **basicStackHibernate** interceptor stack (Struts2 basickStack + Session and Transaction injection)

2. Using the **defaultStackHibernateStrutsValidation** (Struts2 defaultStack + Session and Transaction injection)

3. Using the **com.googlecode.s2hibernate.struts2.plugin.interceptors.SessionTransactionInjectorInterceptor** class as an Interceptor in a custom Interceptors Stack.

4. Do not use the **@Valid** annotation over the Entity POJO declaration in the Action

### 3. I want to use Hibernate Validator feature, but not Session and Transaction injection features. Can I do it? ###

Yes. Use the **com.googlecode.s2hibernate.struts2.plugin.s2hibernatevalidator.interceptor.HibernateValidatorInterceptor** class as an Interceptor in a custom Interceptors Stack and DO NOT USE **basicStackHibernate**, **defaultStackHibernate** and **defaultStackHibernateStrutsValidation** stacks.


### 4. What version of Struts 2 can I use with this Plugin? ###

From Struts 2.0.9+ to 2.1.6.


### 5. Can I use this plugin with Struts 2.0.x Code Behind Plugin? ###

Not tested. Feedback is appreciated.


### 6. Can I use this plugin with Struts 2.1.x Convention Plugin? ###

Yes. This plugin works fine with XML and Annotation (from Convention Plugin) mappings.


### 7. I did every thing right! But the Session/Transaction injection do not goes! What is the problem? ###

All the [Dependencies](http://code.google.com/p/full-hibernate-plugin-for-struts2/wiki/7_Dependencies) must be configured.


### 8. The Session/Transaction injection is Ok in my Actions and this fields. How can I access the injected Session in other class (ie. a custom Interceptor)? ###
If you want to use the same instance of the Session that was used in the Action, use:
**com.googlecode.s2hibernate.struts2.plugin.util.HibernateSessionFactory.getSession()**
This is the internal Hibernate Session Factory of the plugim that uses the local thread pattern.<br />
If you want an "isolated" Session , since **1.4** version, the **com.googlecode.s2hibernate.struts2.plugin.util.HibernateSessionFactory** has the **getNewSession()** method, that returns a new Hibernate Core Session, NOT the Session of the current thread.

### 9. I was using the 1.5 version. From 2.0 on there is possible to use multiple databases. Do I need to change all my configurations? ###

No. The annotations and XML parameters are the same. If you are using a single database at your project, no change is need.

### 10. Is this required to configure a Hibernate Transaction by XML or Annotation? ###

No. You can configure only Hibernate Core Sessions if you prefer.