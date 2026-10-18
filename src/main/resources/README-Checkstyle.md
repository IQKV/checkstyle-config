# Checkstyle Configuration for Java Projects

This directory contains a comprehensive Checkstyle configuration optimized for **Checkstyle 11.1** and modern Java development practices, including Spring Boot applications.

## Files Overview

### Core Configuration

- `maven-project-common-checkstyle.xml` - Main Checkstyle configuration file
- `checkstyle-suppressions.xml` - Standard suppressions for common scenarios
- `checkstyle-xpath-suppressions.xml` - Advanced XPath-based suppressions

### IDE Integration

- `../idea/IDEA-Checkstyle-Defaults.xml` - IntelliJ IDEA code style settings aligned with Checkstyle rules

## Key Features

### ✅ Checkstyle 11.1 Compatibility

- Updated DTD and module references
- Support for modern Java features (Records, Text Blocks, Pattern Matching)
- Enhanced switch expression support
- Improved annotation handling

### ✅ Modern Java Support

- **Java 25+ Features**: Pattern matching, sealed classes, records
- **Text Blocks**: Proper formatting and validation
- **Records**: Component naming and structure validation
- **Switch Expressions**: Enhanced syntax support

### ✅ Spring Boot Optimized

- Relaxed rules for `@Configuration` classes
- Special handling for `@Controller` and `@Service` classes
- Suppression for dependency injection annotations
- Application class exemptions

### ✅ Comprehensive Rule Set

#### Code Quality

- Unused imports and variables detection
- Unnecessary semicolons and parentheses
- Magic number detection with sensible exceptions
- Boolean expression simplification
- Proper exception handling

#### Design Patterns

- Utility class constructor hiding
- Final class enforcement where appropriate
- Interface type validation
- Visibility modifier checks with Spring-aware exceptions

#### Metrics & Complexity

- Cyclomatic complexity (max 15)
- Method length limits (50 NCSS)
- Class size limits (1500 NCSS)
- Nested depth controls
- Boolean expression complexity

#### Formatting & Style

- 2-space indentation
- 190 character line length (soft limit at 100)
- Proper import organization
- Consistent brace placement
- Whitespace standardization

## Usage

### Maven Integration

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-checkstyle-plugin</artifactId>
    <version>3.3.1</version>
    <configuration>
        <configLocation>maven-project-common-checkstyle.xml</configLocation>
        <suppressionsLocation>checkstyle-suppressions.xml</suppressionsLocation>
        <encoding>UTF-8</encoding>
        <consoleOutput>true</consoleOutput>
        <failsOnError>true</failsOnError>
        <linkXRef>false</linkXRef>
    </configuration>
    <dependencies>
        <dependency>
            <groupId>com.puppycrawl.tools</groupId>
            <artifactId>checkstyle</artifactId>
            <version>11.1</version>
        </dependency>
    </dependencies>
</plugin>
```

### Gradle Integration

```gradle
checkstyle {
    toolVersion = '11.1'
    configFile = file('src/main/resources/maven-project-common-checkstyle.xml')
    configProperties = [
        'org.checkstyle.google.suppressionfilter.config': 'checkstyle-suppressions.xml',
        'org.checkstyle.google.suppressionxpathfilter.config': 'checkstyle-xpath-suppressions.xml'
    ]
}
```

## Suppressions Strategy

### Automatic Suppressions

- **Test Classes**: Relaxed complexity and magic number rules
- **Spring Components**: Appropriate visibility and design pattern exceptions
- **DTOs/Entities**: Flexible field visibility for data classes
- **Generated Code**: Complete suppression for generated sources

### Smart Suppressions

- HTTP status codes (200, 404, etc.) exempt from magic number rules
- Builder pattern methods exempt from return count limits
- Annotation values exempt from magic number detection
- Test methods have relaxed string literal rules

## IDE Setup

### IntelliJ IDEA

1. Import the code style: `Settings → Editor → Code Style → Java → Import Scheme`
2. Select `IDEA-Checkstyle-Defaults.xml`
3. Install Checkstyle-IDEA plugin
4. Configure plugin to use `maven-project-common-checkstyle.xml`

### Eclipse

1. Install Checkstyle plugin
2. Import configuration from `maven-project-common-checkstyle.xml`
3. Apply formatting rules from the configuration

## Customization

### Adding Project-Specific Rules

Create a custom suppression file:

```xml
<?xml version="1.0"?>
<!DOCTYPE suppressions PUBLIC
        "-//Checkstyle//DTD SuppressionFilter Configuration 1.2//EN"
        "https://checkstyle.org/dtds/suppressions_1_2.dtd">
<suppressions>
    <!-- Your custom suppressions -->
    <suppress checks="MagicNumber" files="YourSpecificClass\.java"/>
</suppressions>
```

### Adjusting Complexity Limits

Modify the following properties in the main configuration:

- `CyclomaticComplexity.max` (default: 15)
- `JavaNCSS.methodMaximum` (default: 50)
- `NPathComplexity.max` (default: 200)
- `ReturnCount.max` (default: 3)

## Migration from Older Versions

### From Checkstyle 8.x/9.x/10.x

- All existing rules are preserved
- New rules are added with sensible defaults
- Suppressions handle compatibility issues
- No breaking changes to existing valid code

### Common Migration Issues

1. **New semicolon checks**: May flag unnecessary semicolons
2. **Enhanced record support**: Better validation of record components
3. **Improved pattern matching**: Support for modern Java syntax

## Best Practices

### Code Organization

- Keep utility classes final with private constructors
- Use proper visibility modifiers
- Organize imports according to the defined groups
- Maintain consistent indentation (2 spaces)

### Spring Boot Specific

- Use constructor injection over field injection
- Properly annotate configuration classes
- Follow REST controller conventions
- Implement proper exception handling

### Testing

- Test classes have relaxed rules for readability
- Use descriptive test method names
- Organize test data sensibly
- Leverage parameterized tests where appropriate

## Troubleshooting

### Common Issues

1. **Line too long**: Use the 190-character limit, break at logical points
2. **Magic numbers**: Define constants or add suppressions for legitimate cases
3. **Complexity warnings**: Refactor large methods into smaller, focused ones
4. **Import organization**: Use IDE auto-formatting or configure import order

### Getting Help

- Check suppression files for existing exemptions
- Review XPath suppressions for annotation-based rules
- Consider project-specific suppression files for unique cases
- Ensure Checkstyle 11.1 is being used for full compatibility

## Version History

- **v1.0**: Initial Checkstyle 11.1 compatible configuration
- Enhanced Spring Boot support
- Comprehensive rule set with smart suppressions
- Modern Java feature support (Records, Text Blocks, Pattern Matching)
