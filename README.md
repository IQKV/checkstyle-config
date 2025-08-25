# ✨ Checkstyle Configuration

[![Build Status](https://know-how.run/api/badges/dimdnk/checkstyle-config/status.svg)](https://know-how.run/dimdnk/checkstyle-config)

A comprehensive Checkstyle configuration package that provides consistent Java code quality standards across your projects.

## 🚀 Quick Start

Add the following plugin configuration to your Maven project's `pom.xml`:
```xml
<plugin>
  <artifactId>maven-checkstyle-plugin</artifactId>
  <version>3.6.0</version>
  <dependencies>
    <dependency>
      <groupId>com.iqkv</groupId>
      <artifactId>checkstyle-config</artifactId>
      <version>25.0.0</version>
    </dependency>
    <dependency>
      <groupId>com.puppycrawl.tools</groupId>
      <artifactId>checkstyle</artifactId>
      <version>11.0.0</version>
    </dependency>
  </dependencies>
  <configuration>
    <configLocation>maven-project-common-checkstyle.xml</configLocation>
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
For detailed configuration options, see the [maven-checkstyle-plugin documentation](https://maven.apache.org/plugins/maven-checkstyle-plugin/check-mojo.html).

## 🎯 Enterprise Setup

For organizations using a parent POM approach, add the plugin configuration to your `<pluginManagement/>` section in your parent POM. This allows individual projects to simply reference the plugin without duplicating configuration:
```xml
<plugin>
  <artifactId>maven-checkstyle-plugin</artifactId>
</plugin>
```
## ⚙️ Configuration

### Custom Suppressions

You can customize the rules by providing a `checkstyle-suppressions.xml` file in your project's classpath or current directory. The configuration automatically looks for this file using the [SuppressionFilter](http://checkstyle.sourceforge.net/config_filters.html#SuppressionFilter).

For multi-module projects, consider using a [shared suppressions configuration](http://stackoverflow.com/a/19690484/1659929) to maintain consistency across modules.

### IDE Integration

#### IntelliJ IDEA
Import the provided configuration file at `src/main/idea/IDEA-Checkstyle-Defaults.xml` into your IntelliJ IDEA project to sync your IDE with the same rules used in the build process.

## 📝 Features

- ✅ Comprehensive Java code style rules
- ✅ Maven plugin integration
- ✅ Customizable suppressions
- ✅ IDE configuration support
- ✅ Enterprise-ready for parent POM usage

## 📄 License

This project is licensed under the Apache Software License, Version 2.0 - see the [LICENSE](LICENSE) file for details.
