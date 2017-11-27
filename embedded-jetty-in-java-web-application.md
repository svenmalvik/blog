## Embedding Jetty Server in 15 minutes - Quickstart by Sven Malvik

In the world of microservices and container technologies, 
we need Java applications to start as standalone units rather than within heavy application servers. 
This post will show how to embed the Jetty Server within a Java application. 
It will load a war file that is part of the project and that lives as a maven sub-module.

The following tutorial is a more of a transcript of my video "**Embedding Jetty Server in 15 minutes.**". 
[![Embedding Jetty Server in 15 minutes - Quickstart by Sven Malvik](https://raw.github.com/svenmalvik/blog/master/img/youtube.png)](https://youtu.be/rBcwbsEFcVI)

### Agenda
* Create a maven project.
* Create a maven module for the server.
* Add a servlet.
* Create a maven module for the web application that build the war file.
* Add webapp (.war) support into the server module.

### Create the maven project
The first job you've to do is to open your IDE and create a new maven project. 
In my case I'm going for maven 3.3.9. When done you might notice a source (src) folder 
that you can delete since we're going for a multi module project. 
You don't need to modify the **root pom.xml** yet.

```xml
<!-- pom.xml -->
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
                             http://maven.apache.org/xsd/maven-4.0.0.xsd">
         
    <modelVersion>4.0.0</modelVersion>
    <groupId>de.malvik</groupId>
    <artifactId>myjetty</artifactId>
    <packaging>pom</packaging>
    <version>1.0-SNAPSHOT</version>
</project>
```

### Create a maven module for the server.
Now, add a new maven modul either with help from your IDE or from **command line**:
```shell
$ cd YOUR_PROJECT
$ mvn archetype:generate -DgroupId=com.mydomain 
                         -DartifactId=server 
                         -DarchetypeArtifactId=maven-archetype-quickstart 
                         -DinteractiveMode=false
```

This will generate a maven sub module named 'server' and will be declared in your root pom file:
```xml
<!-- pom.xml -->
<modules>
    <module>server</module>
</modules>
```

The next step is to open the generated ```App.java``` file. 
That's the file where the main method is located.
In here we're going to implement the Jetty server startup.
```java
// App.java
public static void main(String[] args) throws Exception {
    Server server = new Server(8080); // Port 8080
    // startup code
    server.start();
    server.join(); // Wait until the startup code is completed
}
```

### Add a servlet.
The next step is more about getting an understanding about what you're doing. 
We'll add a simple servlet that will respond to our requests.
This is done by a handler that you will set for the server-object. 
The handler needs two information from you. A context-path like "/ping", and a handler.
An very simple handler extends either from `AbstractHandler`, or eventually from `HttpServlet`.
Extending your handler-class from `HttpServlet` means that you save some work 
like manually telling that you're finished processing the request-object. 
Here's an example of my `PingHandler`:
```java
// PingHandler.java
public class PingHandler extends HttpServlet {
    
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) 
            throws ServletException, IOException {
        resp.setStatus(HttpServletResponse.SC_OK);
        resp.getWriter().println("<h1>This is a test.</h1>");
    }
}
```

We're not done yet. We need to connect the handler with the server and set the context-path:
```java
// App.java
private static void setServlet(Server server) {
    ServletHandler handler = new ServletHandler();
    handler.addServletWithMapping(PingHandler.class, "/ping");
    server.setHandler(handler);
}
```

That's basically it. The next step will be about responding from a `.war` file

### Create a maven module for the web application that build the war file.
Again, we need to create a maven module. Run this command from within your shell or use your IDE:
```shell
$ cd YOUR_PROJECT
$ mvn archetype:generate -DgroupId=com.mycompany
                         -DartifactId=webapp 
                         -DarchetypeArtifactId=maven-archetype-webapp 
                         -DinteractiveMode=false
```

Your project-structure should now look similar to this one:

![Project structure](https://raw.github.com/svenmalvik/blog/master/img/project.PNG)

### Add webapp (.war) support into the server modul.



