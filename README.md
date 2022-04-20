uJar Checkstyle Configuration
================================

[![Build Status](https://drone.ujar.org/api/badges/ujar-org/code-quality-checkstyle/status.svg?ref=refs/heads/main)](https://drone.ujar.org/ujar-org/code-quality-checkstyle)

This project provides a default configuration for checkstyle.

To use it, configure your maven-checkstyle-plugin like so:

```
   <plugin>
     <artifactId>maven-checkstyle-plugin</artifactId>
     <version>3.1.2</version>
     <dependencies>
       <dependency>
         <groupId>org.ujar.codequality</groupId>
         <artifactId>code-quality-checkstyle</artifactId>
         <version>LATEST-VERSION</version>
       </dependency>
       <dependency>
         <groupId>com.puppycrawl.tools</groupId>
         <artifactId>checkstyle</artifactId>
         <version>9.1</version>
       </dependency>
     </dependencies>
     <configuration>
       <configLocation>ujar_checks.xml</configLocation>
       
       <!-- The following parameters are optional: -->
       <consoleOutput>true</consoleOutput>
       <failOnViolation>true</failOnViolation>
       <logViolationsToConsole>true</logViolationsToConsole>
       <violationSeverity>error</violationSeverity>
     </configuration>
     <executions>
       <execution>
         <id>validate</id>
         <phase>validate</phase>
         <goals>
           <goal>check</goal>
         </goals>
       </execution>
     </executions>
   </plugin>
```

See the [maven-checkstyle-plugin docs](https://maven.apache.org/plugins/maven-checkstyle-plugin/check-mojo.html)
for more information about what the configuration parameters mean.

Internally, we have the above configuration in the `<pluginManagement/>` section of a company-wide parent pom, meaning
that projects only need to specify the below in their
`<build><plugins>` section:

```
   <plugin>
      <artifactId>maven-checkstyle-plugin</artifactId>
   </plugin>
```

# Configuration

## Suppressions

The configuration of the checkstyle plugin you get from `ujar_checks.xml` tells it to optionally look for a file
named `checkstyle-suppressions.xml` as per the
[SuppressionFilter docs](http://checkstyle.sourceforge.net/config_filters.html#SuppressionFilter). This means you can
configure suppressions by providing such a file on your project's classpath or in the current directory where you build
it - note that for multi-module projects, it's probably a good idea to use something
like [this solution](http://stackoverflow.com/a/19690484/1659929) to share the configuration among each sub-module.

# IDEA support

There is a [configuration file for IntelliJ IDEA](src/main/idea/ujar-checkstyle-idea.xml) that you can import into your
project.
