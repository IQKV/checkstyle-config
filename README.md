Checkstyle Configuration
================================

[![Build Status](https://know-how.run/api/badges/IQKV/iqkv-checkstyle-config/status.svg)](https://know-how.run/IQKV/iqkv-checkstyle-config)

This project provides a default configuration for checkstyle.

To use it, configure your maven-checkstyle-plugin like so:

```
   <plugin>
     <artifactId>maven-checkstyle-plugin</artifactId>
     <version>3.3.0</version>
     <dependencies>
       <dependency>
         <groupId>org.iqkv.checkstyle</groupId>
         <artifactId>iqkv-checkstyle-config</artifactId>
         <version>LATEST-VERSION</version>
       </dependency>
       <dependency>
         <groupId>com.puppycrawl.tools</groupId>
         <artifactId>checkstyle</artifactId>
         <version>10.12.4</version>
       </dependency>
     </dependencies>
     <configuration>
       <configLocation>iqkv-common-checkstyle.xml</configLocation>
       
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

### Suppressions

The configuration of the checkstyle plugin you get from `iqkv-common-checkstyle.xml` tells it to optionally look for a file
named `checkstyle-suppressions.xml` as per the
[SuppressionFilter docs](http://checkstyle.sourceforge.net/config_filters.html#SuppressionFilter). This means you can
configure suppressions by providing such a file on your project's classpath or in the current directory where you build
it - note that for multi-module projects, it's probably a good idea to use something
like [this solution](http://stackoverflow.com/a/19690484/1659929) to share the configuration among each sub-module.

### IDEA support

There is a [configuration file for IntelliJ IDEA](src/main/idea/svc-common-checkstyle-idea.xml) that you can import into your
project.

## Versioning

Project uses a three-segment [CalVer](https://calver.org/) scheme, with a short year in the major version slot, short month in the minor version slot, and micro/patch version in the third
and final slot.

```
YY.MM.MICRO
```

1. **YY** - short year - 6, 16, 106
1. **MM** - short month - 1, 2 ... 11, 12
1. **MICRO** -  "patch" segment
