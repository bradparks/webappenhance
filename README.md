# Java Web Application Enhancements Library

Utility library for Java web applications

### Note: more info about this here:
http://stackoverflow.com/a/11439311/26510

## Add library to your project

Add this Maven dependency:

    <dependency>
      <groupId>com.github.pukkaone</groupId>
      <artifactId>webappenhance</artifactId>
      <version>1.0.1</version>
    </dependency>


## Compile JSPs on startup

In the `web.xml` file, add a listener:

    <listener>
      <listener-class>com.github.pukkaone.jsp.JspCompileListener</listener-class>
    </listener> 


## Escape JSP EL values to prevent cross-site scripting

In the `web.xml` file, add a listener:

    <listener>
      <listener-class>com.github.pukkaone.jsp.EscapeXmlELResolverListener</listener-class>
    </listener> 


### Disable escaping

Use a custom tag to surround JSP code in which EL values should not be escaped:

    <%@ taglib prefix="enhance" uri="http://pukkaone.github.com/jsp" %>

    <enhance:out escapeXml="false">
      I hope this expression returns safe HTML: ${user.name}
    </enhance:out>


## Read model data in Jersey MVC JSP templates without "it."

Jersey's MVC framework exposes the model object to the JSP template as a
request attribute named "it".  To read the model data, a JSP template must
evaluate an EL expression reading a property of this object, for example,
`${it.propertyName}`.  This custom EL resolver exposes model properties as
implicit objects, allowing a JSP template to read a model property with an EL
expression like `${propertyName}`.

In the `web.xml` file, add a listener:

    <listener>
      <listener-class>com.github.pukkaone.jsp.ViewableModelELResolverListener</listener-class>
    </listener> 
