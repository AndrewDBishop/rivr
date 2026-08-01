# Rivr

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Java 21](https://img.shields.io/badge/Java-21-orange.svg)](https://www.oracle.com/java/)
[![Jakarta EE 10](https://img.shields.io/badge/Jakarta%20EE-10-blue.svg)](https://jakarta.ee/)
[![Build System](https://img.shields.io/badge/Build-Maven%20%7C%20Gradle-brightgreen.svg)](#building)

Rivr is a lightweight open-source dialogue engine enabling Java developers to easily create enterprise-grade VoiceXML applications.

This repository is a modern fork of Rivr updated for **Java 21 (LTS)**, **Jakarta EE 10+** (Tomcat 10.1+, Spring Boot 3+), and full **Apache Maven** support.

---

## Table of Contents

- [Features & Modernization](#features--modernization)
- [Prerequisites](#prerequisites)
- [Quick Start & Usage](#quick-start--usage)
  - [Using with Apache Maven](#using-with-apache-maven)
  - [Importing into Eclipse / Spring Tool Suite (STS)](#importing-into-eclipse--spring-tool-suite-sts)
- [Building from Source](#building-from-source)
- [Project Architecture](#project-architecture)
- [VoiceXML Concepts](#voicexml-concepts)
- [Contributing](#contributing)
- [License](#license)

---

## Features & Modernization

* **Java 21 Support**: Modernized source and bytecode target compatibility for modern JDKs.
* **Jakarta EE Migration**: Complete migration from `javax.servlet` to `jakarta.servlet` namespace for Jakarta EE 10+ web servers.
* **Apache Maven Integration**: Added parent and module `pom.xml` descriptors alongside the existing Gradle files.
* **Modern Dependencies**:
  * Jakarta JSON Processing (`jakarta.json-api` 2.1+)
  * Apache Commons FileUpload 2 (`commons-fileupload2-jakarta-servlet6`)
  * SLF4J 2.x Logging API (`slf4j-api` 2.0.16)
* **Testing & Quality Assurance**: Configured for JUnit 5, Checkstyle, and Maven Javadoc generation.

---

## Prerequisites

* **JDK 21** or higher
* **Apache Maven 3.8+** (or Gradle 7.6+)
* **Jakarta EE 10+ Servlet Container** (e.g., Apache Tomcat 10.1+, Spring Boot 3+)
* **VoiceXML 2.1 Compliant Platform** (for deployment)

---

## Quick Start & Usage

### Using with Apache Maven

1. Clone and install Rivr to your local Maven repository (`~/.m2/repository`):

   ```bash
   git clone https://github.com/AndrewDBishop/rivr.git
   cd rivr
   git checkout maven-build
   mvn clean install
   ```

2. Add `rivr-voicexml` as a dependency in your application's `pom.xml`:

   ```xml
   <dependency>
       <groupId>com.nuecho</groupId>
       <artifactId>rivr-voicexml</artifactId>
       <version>1.0.13</version>
   </dependency>
   ```

### Importing into Eclipse / Spring Tool Suite (STS)

1. Open **Spring Tool Suite** or **Eclipse**.
2. Select **File → Import... → Existing Maven Projects**.
3. Browse to the root `rivr` repository directory and complete the wizard.
4. Eclipse will automatically recognize all 3 sub-projects (`rivr-core`, `rivr-voicexml`, `rivr-voicexml-dialogue-runner`).

---

## Building from Source

### Maven Build Commands

* **Compile and package all artifacts**:
  ```bash
  mvn clean package
  ```
* **Install artifacts to local repository**:
  ```bash
  mvn clean install
  ```
* **Run Checkstyle code analysis**:
  ```bash
  mvn checkstyle:checkstyle
  ```
* **Generate Javadoc documentation**:
  ```bash
  mvn javadoc:javadoc
  ```

---

## Project Architecture

```
rivr/
├── rivr-core/                          # Core dialogue engine & abstract servlet handling
├── rivr-voicexml/                      # VoiceXML step renderers, turns, and event handling
├── rivr-voicexml-dialogue-runner/      # Interactive simulation runner (WAR application)
├── checkstyle/                         # Code style definitions
├── doc/                                # Javadoc documentation templates
└── pom.xml                             # Parent Maven POM
```

---

## VoiceXML Concepts

### What is Rivr?

Rivr is a Java library for VoiceXML application development. Developers write dialogue logic using regular Java control flow (loops, conditional branches, method calls), and Rivr generates VoiceXML documents dynamically during execution, handling user responses synchronously.

### What is VoiceXML?

VoiceXML is an W3C standard for Interactive Voice Response (IVR) systems. It controls speech recognition, DTMF keypress input, audio prompt playback, audio recording, and speech synthesis.

### Key Benefits

* **Code-driven Dialogue Control**: Dialogue logic is expressed in Java code rather than complex VoiceXML Form Interpretation Algorithm (FIA) XML documents.
* **Centralized State**: State and business logic remain securely on the server.
* **Unit Testing**: Dialogues can be unit-tested locally with JUnit without requiring an active telephony system.
* **Dialogue Abstraction**: Reuse high-order dialogues and parameterize call flows across enterprise projects.

---

## Contributing

Contributions, bug reports, and pull requests are welcome!

1. Fork the repository.
2. Create your feature branch (`git checkout -b feature/my-feature`).
3. Commit your changes (`git commit -m 'Add my feature'`).
4. Push to the branch (`git push origin feature/my-feature`).
5. Open a Pull Request.

---

## License

This project is licensed under the Apache License 2.0. See the original Nu Echo copyright headers in individual source files for details.
