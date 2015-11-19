Spring Boot Starter Handlebars
====

[![Build Status](https://travis-ci.org/allegro/handlebars-spring-boot-starter.svg)](https://travis-ci.org/allegro/handlebars-spring-boot-starter)
[![Coverage Status](https://coveralls.io/repos/allegro/handlebars-spring-boot-starter/badge.svg)](https://coveralls.io/r/allegro/handlebars-spring-boot-starter)
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/pl.allegro.tech.boot/handlebars-spring-boot-starter/badge.svg?style=flat)](https://maven-badges.herokuapp.com/maven-central/pl.allegro.tech.boot/handlebars-spring-boot-starter)

Spring Boot Starter support for
[Handlebars.java](https://github.com/jknack/handlebars.java)
(logic-less templates).

## Usage

Add `handlebars-spring-boot-starter` as dependency:
```gradle
repositories {
    mavenCentral()
}

dependencies {
    compile 'pl.allegro.tech.boot:handlebars-spring-boot-starter:0.2.9'
}
```
## Helpers

Spring Boot Starter Handlebars will automatically register handlebars helpers based on project dependencies.
Add any handlebars helper to dependencies and you can start using it.
```gradle
dependencies {
    compile 'com.github.jknack:handlebars-helpers:4.0.1',
            'com.github.jknack:handlebars-jackson2:4.0.1',
            'com.github.jknack:handlebars-humanize:4.0.1',
            'com.github.jknack:handlebars-markdown:4.0.1'
}
```
NOTE: Jackson2Helper and MarkdownHelper will register with name `json` and `md` respectively.
Every other helper will register with its default name.

More information about available helpers can be found on
[Handlebars.java](https://github.com/jknack/handlebars.java#helpers).

### Custom helpers

To register a custom helper use [@HandlebarsHelper](src/main/java/pl/allegro/tech/boot/autoconfigure/handlebars/HandlebarsHelper.java) annotation.

#### Example
```java
@HandlebarsHelper
class CustomHelper {
    CharSequence foo() {
        return 'bar'
    }
}
```
More information about how to create custom helpers can be found on [Using a HelperSource](https://github.com/jknack/handlebars.java#using-a-helpersource)

## Configuration

Properties space is: `handlebars`. All basic properties of
[AbstractTemplateViewResolverProperties.java](http://docs.spring.io/autorepo/docs/spring-boot/current/api/org/springframework/boot/autoconfigure/template/AbstractTemplateViewResolverProperties.html)
are available.

Default configuration:
```yaml
handlebars.prefix: classpath:templates/
handlebars.suffix: .hbs
handlebars.cache: true
handlebars.registerMessageHelper: true
handlebars.failOnMissingFile: false
handlebars.prettyPrint: false
```
NOTE: `handlebars-guava-cache` is used as template cache implementation.

`resolver` configuration allows on/off available handlebars value resolvers.
Here goes default configuration:
```yaml
handlebars.resolver.javaBean: true
handlebars.resolver.map: true
handlebars.resolver.method: false
handlebars.resolver.field: false
```
More information about value resolvers can be found on
[Using the ValueResolver](https://github.com/jknack/handlebars.java#using-the-valueresolver).

### Custom cache template

Set handlebars template cache by `@Bean` of type [TemplateCache](https://github.com/jknack/handlebars.java/blob/master/handlebars/src/main/java/com/github/jknack/handlebars/cache/TemplateCache.java).

### Custom template loader

Set handlebars template loader by `@Bean` of type [TemplateLoader](https://github.com/jknack/handlebars.java/blob/master/handlebars/src/main/java/com/github/jknack/handlebars/io/TemplateLoader.java).

## License

**handlebars-spring-boot-starter** is published under [Apache License 2.0](http://www.apache.org/licenses/LICENSE-2.0).
