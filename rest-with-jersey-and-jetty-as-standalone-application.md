# REST with Jersey and Jetty as standalone application
_In a previous blog entry I wrote about how you run and setup your [**Java web application as 
a standalone application with Jetty**](embedding-jetty-in-java-web-application) 
and a `.war` file with maven. In this blog entry I want to show how you can integrate a RESTful 
interface with Jersey into your Jetty standalone application._

## Maven
Tell maven first that you need Jetty and the Jersey servlet libraries: 
```xml
<!-- server/pom.xml -->
<dependency>
    <groupId>org.eclipse.jetty.aggregate</groupId>
    <artifactId>jetty-all</artifactId>
    <version>9.2.11.v20150529</version>
</dependency>
<dependency>
    <groupId>org.glassfish.jersey.containers</groupId>
    <artifactId>jersey-container-servlet-core</artifactId>
    <version>2.7</version>
</dependency>
```

## Jetty Server
Navigate now to your `App.java` file and implement the server. We will set the handler that 
we'll discuss in the next section.
```java
// App.java
public static void main( String[] args ) throws Exception {
    Server server = new Server(8080);
    server.setHandler(getJerseyHandler());
    server.start();
    server.join();
}
```

## Jersey
Now we should implement a simple handler for dealing with Jersey.
At first, we need a context handler, as explained in 
[Java web application as a standalone application with Jetty](embedding-jetty-in-java-web-application)
After setting the context path for the application we will connect Jetty with Jersey through 
a `ServletHolder`. In the last step we tell Jersey where to find our Restful classes - that 
we don't have yet.

```java
// App.java
private static Handler getJerseyHandler() {
    ServletContextHandler ctx = 
        new ServletContextHandler(ServletContextHandler.NO_SESSIONS);
    ctx.setContextPath("/");
    ServletHolder servlet = 
        ctx.addServlet(ServletContainer.class, "/api/*");
    servlet.setInitParameter("jersey.config.server.provider.classnames", 
                             Entrypoint.class.getCanonicalName());
    return ctx;
}
```

## RESTful interface
`Entrypoint.java` is our RESTful interface. It will listen on `/ep`.
The method endpoint1 responds with plain text.
```java
// Entrypoint.java
@Path("/ep")
public class Entrypoint {
    
    @GET
    @Produces(MediaType.TEXT_PLAIN)
    @Path("1")
    public String endpoint1() {
        return "Hallo form endpoint1";
    }
}
```

## Conclusion
You can now start the server and call `http://localhost:8080/api/ep/1` in your browser.

For [**detailed information about the myjetty project**](https://github.com/svenmalvik/myjetty) you should visit my github.

_**Sven Malvik - Lead Software Engineer**_