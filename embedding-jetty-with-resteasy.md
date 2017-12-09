# Embedding Jetty with RESTEasy
_In this blog post I will explain how you would embed the Jetty server 
together with RESTEasy in a single standalone Java application. 
The project uses Maven, and it is available to you on my GitHub-account.
[Download Jetty-RESTEasy-Combo](https://github.com/svenmalvik/jetty-resteasy-combo)._

## Agenda
* Create a maven project.
* Setup the server.
* Create an endpoint
* Connect the endpoint with the server

## Create a maven project

Run the command below, or use the IDE of your choice to create a simple maven project:
```shell
$ cd YOUR_PROJECT
$ mvn archetype:generate -DgroupId=com.mydomain 
                         -DartifactId=server 
                         -DarchetypeArtifactId=maven-archetype-quickstart 
                         -DinteractiveMode=false
```

Next, we'll edit the `pom.xml`-file to add some dependencies. At first you'll need Jetty. 
I like to go for the whole package in prototype-like projects, that's
why I choose to go for `jetty-all`. We'll also need `slf4j-simple` to send messages to stdout. 
Without that dependency, Jetty (> 9.3) will complain. Finally, we put  our resteasy into the 
list of our dependencies.

```xml
<!-- pom.xml -->
<dependency>
  <groupId>org.eclipse.jetty.aggregate</groupId>
  <artifactId>jetty-all</artifactId>
  <version>9.4.7.RC0</version>
</dependency>
<dependency>
  <groupId>org.slf4j</groupId>
  <artifactId>slf4j-simple</artifactId>
  <version>1.7.25</version>
</dependency>
<dependency>
  <groupId>org.jboss.resteasy</groupId>
  <artifactId>resteasy-jaxrs</artifactId>
  <version>3.1.4.Final</version>
</dependency>
```

## Setup the server
So, we're going to setup the server. for that we open the generated ```App.java``` file. 
That's the file where the main method is located.
In here we'll implement the Jetty server startup.
```java
// App.java
public static void main(String[] args) throws Exception {
    Server server = new Server(8080); // Port 8080
    // startup code
    server.start();
    server.join(); // Wait until the startup code is completed
}
```

## Create an endpoint
Before we mess around the server-setup, I suggest that we implement the endpoint that will
answer all requests at first. 

```java
// Endpoint.java
@Path("api")
public class Endpoint {

    @GET // GET request
    @Produces(MediaType.TEXT_PLAIN) // Response type
    @Path("ping") // Endpoint path
    public String ping() {
        return "pong";
    }
}
```

We'are not finished yet. We need a container that holds all of our endpoint-classes - for now we 
got one. We bame it `AppResourceConfig`.
 
```java
// AppResourceConfig.java
public class AppResourceConfig extends Application {

    Set<Class<?>> classes = new HashSet<Class<?>>();
    
    public AppResourceConfig() {
        classes.add(Endpoint.class);
    }
    
    public Set<Class<?>> getClasses() {
        return classes;
    }
}
```

As we now have a container with our endpoint-class named "Endpoint", we can set it in the server.

## Connect the endpoint with the server

`HttpServletDispatcher` is an ordinary HttpServlet that dipatches requests to the right endpoint classes.
That's why we also tell where those classes are to find - in `AppResourceConfig`.

```java
// App.java
private static Handler getRESTEasyHandler() {
    ServletContextHandler handler = 
        new ServletContextHandler(ServletContextHandler.NO_SESSIONS);
    
    ServletHolder servlet = handler.addServlet(HttpServletDispatcher.class, "/");
    
    servlet.setInitParameter("javax.ws.rs.Application", 
                             AppResourceConfig.class.getCanonicalName());
    return handler;
}
```

Finally, we set the handler (the return value) to the server.
```java
// App.java
public static void main( String[] args ) throws Exception {
    Server server = new Server(8080);
    
    server.setHandler(getRESTEasyHandler());
    
    server.start();
    server.join();
}
```

## Conclusion
It's a basic example of how you would embed Jetty with RESTEasy in Java. 
[**Please subscribe to my YouTube-channel.**](https://www.youtube.com/playlist?list=PLDAA9E2877BC4145D)

