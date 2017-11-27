## Embedding Jetty Server in 15 minutes - Quickstart by Sven Malvik

In the world of microservices and container technologies, we need Java applications to start as standalone units rather than within heavy application servers. This post will show how to embed the Jetty Server within a Java application. It will load a war file that is part of the project and that lives as a maven sub-modul.

The following tutorial is a more of a transcript of my video "**Embedding Jetty Server in 15 minutes.**". 
[![Embedding Jetty Server in 15 minutes - Quickstart by Sven Malvik](https://raw.github.com/svenmalvik/blog/master/img/youtube.png)](https://youtu.be/rBcwbsEFcVI)

### Agenda
* Create a maven project.
* Create a maven module for the server.
* Add a servlet.
* Create a maven module for the web application that build the war file.
* Add webapp (.war) support into the server modul.

### Create the maven project
The first job you've to do is to open your IDE and create a new maven project. 
In my case I'm going for maven 3.3.9. When done you might motice a source (src) folder 
that you can delete since we're going for a multi modul project. You don't need to modify the root pom.xml yet.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
         
    <modelVersion>4.0.0</modelVersion>
    <groupId>de.malvik</groupId>
    <artifactId>myjetty</artifactId>
    <packaging>pom</packaging>
    <version>1.0-SNAPSHOT</version>
</project>
```

### Create a maven module for the server.

### Add a servlet.

### Create a maven module for the web application that build the war file.

### Add webapp (.war) support into the server modul.



