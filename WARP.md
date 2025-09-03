# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Project Overview

This is a Java Maven project for the Parallel Computing in Java course (Coursera). It demonstrates basic parallel programming concepts using the PCDP (Parallel Computing and Data Processing) library from Rice University.

**Key Technologies:**
- Java 8 (compiled with Maven compiler 3.13.0)
- PCDP Core Library 0.0.4-SNAPSHOT for parallel computing constructs
- JUnit 4.13.2 for testing
- Maven 3.x for build management
- Google Java Style checkstyle configuration

## Architecture Overview

The project follows a standard Maven directory structure:

- `src/main/java/edu/coursera/parallel/` - Main source code
  - `Setup.java` - Demonstrates basic PCDP usage with `finish` and `async` constructs
  - `package-info.java` - Package documentation
- `src/test/java/edu/coursera/parallel/` - Test classes
  - `SetupTest.java` - Simple JUnit test for the Setup class
- `src/main/resources/checkstyle.xml` - Google Java Style configuration (customized)

**PCDP Programming Model:**
The project uses PCDP's `finish` and `async` constructs for parallel programming:
- `finish` - Waits for all nested async tasks to complete
- `async` - Creates asynchronous tasks that run in parallel

## Development Commands

### Build and Compilation
```bash
# Clean and compile the project
mvn clean compile

# Compile only (incremental)
mvn compile

# Package into JAR
mvn package
```

### Testing
```bash
# Run all tests
mvn test

# Run a specific test class
mvn test -Dtest=SetupTest

# Run a specific test method
mvn test -Dtest=SetupTest#testSetup
```

### Code Quality
```bash
# Run checkstyle validation (Google Java Style)
mvn checkstyle:check

# Run checkstyle during validate phase
mvn validate
```

### Dependencies
```bash
# Download dependencies and populate classpath properties
mvn dependency:properties

# Display dependency tree
mvn dependency:tree

# Display effective POM
mvn help:effective-pom
```

## Development Configuration

**Maven Surefire Configuration:**
- Tests run with `-Xmx4g` heap size
- Fork count: 1 (single forked process)
- Reuse forks: disabled for test isolation
- Test failures are ignored (for Coursera submission workflow)

**Checkstyle Configuration:**
- Based on Google Java Style Guide
- Key customizations:
  - Line length limit disabled
  - Star imports allowed
  - Abbreviated names up to 3 characters allowed
  - Variable distance up to 30 lines allowed

**Java Compilation:**
- Source/target: Java 1.8
- Encoding: UTF-8
- Warnings about obsolete Java 8 options are expected

## PCDP Library Usage

When working with parallel constructs:
1. Import static methods: `import static edu.rice.pcdp.PCDP.finish;` and `import static edu.rice.pcdp.PCDP.async;`
2. Use `finish` blocks to wait for all nested async tasks
3. Use `async` to create parallel tasks
4. Be cautious with shared mutable state - use final variables for task communication

## Repository Dependencies

The project depends on a custom Maven repository for PCDP:
- Repository: `https://raw.github.com/habanero-maven/hjlib-maven-repo/mvn-repo-pcdp-0.0.4-SNAPSHOT/`
- The PCDP library is automatically downloaded during build

## Testing Notes

- Tests use JUnit 4 framework (not JUnit 5)
- Use `extends TestCase` pattern for test classes
- Test methods should be public and start with `test`
- The project includes a simple integration test to verify PCDP functionality
