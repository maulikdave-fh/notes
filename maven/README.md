Maven is a software project lifecycle management tool. It is based on POM (Project Object Model). It follows convention over configuration & follows a pre-defined directory structure.

The output can be jar / war. Default packaging type is jar, if not specified.

# pom.xml
## Maven Dependencies
Frameworks and libs used in a project. Dependencies of dependency are called transitive dependencies. Maven downloads transitive dependencies as well.

## parent POM
All parent POM properties are inherited by child POM - all spring-boot-starter projects have parent POM. Effective POM reflects parent POM properties as well. ```<dependencyManagement>``` tag in Effective POM outlines all dependencies including their versions.

## Project Name
- ```<groupId>``` is similar to package name - indicates a namespace
- ```<artifactId>``` is similar to class name - indicates a project name
- ```<version>``` - project version

Project's fully qualified name - ```<groupId>:<artifactId>:<version>```

**Dependency Issues:** Start by analyzing Effective POM.

## Super POM
All POMs extend the super POM. 

# Maven Repos
## Central Repo
1. Contains jars indexed by groupId and artifactId
2. Stores all the versions of dependencies
3. Use ```<repositories><repository>``` to specify custom repo
4. ```<pluginrepositories><pluginrepository>``` - repo where plugins are stored

## Local Repo
1. Maven downloads dependencies from central repo to local repo and are added to project classpath
2. Local repo is a temporary directory on developer's machine

# Maven Commands
1. mvn --version
2. mvn compile - compiles src/main/java source files
3. mvn test-compile - complies test classes + source files
4. mvn clean - deletes target directory
5. mvn test - runs all unit tests
6. mvn package - creates jar / war file and puts it into target directory
7. mvn install - mvn package + puts a jar file in local repo
8. mvn help:effective-pom - prints effective pom
9. mvn dependency:tree - prints project dependencies

# Minimal pom.xml
```
<project>
    <modelVersion></modelVersion>
    <groupId></groupId>
    <artifactId></artifactId>
    <version></version>
</project>
```
    

