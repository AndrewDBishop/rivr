[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Java 21](https://img.shields.io/badge/Java-21-orange.svg)](https://www.oracle.com/java/)
[![Jakarta EE 10](https://img.shields.io/badge/Jakarta%20EE-10-blue.svg)](https://jakarta.ee/)

## Andrew's Fork & Modernization Updates

This repository is a modern fork of Rivr updated to run on **Java 21 (LTS)** and **Jakarta EE 10+** application servers (such as Tomcat 10.1+ and Spring Boot 3+).

### Key Modernization Features

* **Java 21 Support**: Modernized source and target compilation compatibility to Java 21.
* **Jakarta EE Migration**: Converted all `javax.servlet` packages to `jakarta.servlet` and updated dependencies to Jakarta JSON-P (`jakarta.json-api` 2.1+) and Commons FileUpload 2.x for Jakarta EE 10+ servlet support.
* **Apache Maven Support**: Added a complete multi-module Maven build structure (`pom.xml`) alongside Gradle, allowing seamless integration with Maven workflows and IDEs like Eclipse / Spring Tool Suite (STS).
* **Automated Code Quality & Testing**: Configured Maven plugins for JUnit 5, Checkstyle, and Javadoc generation.

### Quick Start with Maven

To build and install the Rivr modules into your local Maven repository (`~/.m2/repository`):

```bash
git clone https://github.com/AndrewDBishop/rivr.git
cd rivr
git checkout maven-build
mvn clean install
```

To use Rivr in your Maven project, add `rivr-voicexml` to your application's `pom.xml`:

```xml
<dependency>
    <groupId>com.nuecho</groupId>
    <artifactId>rivr-voicexml</artifactId>
    <version>1.0.13</version>
</dependency>
```

For Eclipse / Spring Tool Suite (STS) users, import the project directly via **File → Import... → Existing Maven Projects**.

---

## Overview

Rivr is a lightweight open-source dialogue engine enabling Java developers to easily create enterprise-grade VoiceXML applications.

Read our [Getting Started](https://github.com/nuecho/rivr/wiki/Getting-Started) to learn more.

The complete [Javadoc for Rivr](https://nuecho.github.io/rivr/javadoc/) is available online.

You can also get started by trying some of the Rivr sample applications:

- [Hello World](https://github.com/nuecho/rivr-cookbook/wiki/Hello-World) - a very simple hello world application
- [Voicemail](https://github.com/nuecho/rivr-voicemail) - a prototype voicemail application

You can continue to learn by example with the [Rivr cookbook](https://github.com/nuecho/rivr-cookbook/wiki).

## FAQ

### What is Rivr?

Rivr is a Java library for VoiceXML application development. The developer writes the dialogue as a normal Java program and Rivr takes care of generating VoiceXML documents dynamically during execution and makes user responses available to the dialogue in a synchronous manner.

Rivr is a Java-centric approach. All Java tools and practice can be applied to IVR application development.

### What is VoiceXML?

VoiceXML is a W3C standard for interactive voice response, i.e. telephony system interacting with the caller by using speech recognition, DTMF input, recording, speech synthesis, etc.

VoiceXML is primarily targeted at contact center environments and over-the-phone self-service applications.

[VoiceXML 2.0](https://www.w3.org/TR/voicexml20/) is the specification major version while [VoiceXML 2.1](https://www.w3.org/TR/voicexml21/) only adds a few more features on top of the 2.0 version.

### What is required to _develop_ a VoiceXML application with Rivr?

You should have a Java 21 development environment and Maven or Gradle. Also, you should already be familiar with the Java language and Jakarta Servlets. While not essential at the beginning, it can be very useful to understand some basic notions of VoiceXML such as prompt queuing, barge-in, properties, etc. Since the Rivr model is based on VoiceXML, it is sometimes necessary to understand the VoiceXML layer underneath.

### What is required to _run_ a VoiceXML application with Rivr?

You should have:

1. A VoiceXML-compliant platform (VoiceXML 2.1)
2. A Jakarta EE 10+ web application server / Servlet container (e.g. Tomcat 10.1+)
3. A Java web application (i.e. a WAR file) containing:
    1. the Rivr jar files (`rivr-core-1.0.13.jar`, `rivr-voicexml-1.0.13.jar`)
    2. the run-time dependencies:
        1. `slf4j-api.jar` and an SLF4J adapter
        2. `commons-fileupload2-jakarta-servlet6.jar`
        3. `jakarta.json-api.jar` and an implementation (e.g. GlassFish `org.glassfish:jakarta.json`)
    3. your Rivr application (minimally a Dialogue class)
    4. the appropriate configuration in `web.xml`

### What benefits Rivr offers?

#### Rivr allows Java developers to write callflows as programs.

The callflow logic is expressed directly in the code. For example, if the call flow required a question to be asked no more than 3 times, this can be implemented with a simple `for` loop. No need to fiddle with the VoiceXML Form Interpretation Algorithm (FIA).

#### All application logic in centralized in the Java code on the server-side.

With Rivr, no dialogue logic resides on the VoiceXML side. Dialogue rules can be expressed and controlled from the Java side. The dialogue state is maintained on the server.

#### Rivr allows unit and coverage testing.

Since Rivr dialogues are regular Java methods, they can be unit tested as any other regular Java code. It is simple to check with JUnit that a dialogue asks the expected questions and reacts correctly for any simulated user input. By combining the unit tests with a code coverage tool, we can rapidly setup an automated call flow coverage verification solution.

#### Development of application can start early in the project, even before VoiceXML platform is ready.

Development can start as soon as the dialogue specification is available. Rivr offers a VoiceXML simulation tool, _the dialogue runner_, which allows developers to interactively test the dialogues they are developing. Unit testing can also starts as soon as we have a working dialogue (which can be within minutes).

#### Dialogue abstraction, modularity and reuse.

The fact that a dialogue is pure Java code, it's easy to make them abstract. For example, one can define a dialogue as a Java method taking input parameters which will condition the dialogue execution. Those dialogues can be placed into reusable Java packages and shared between applications.

It's even possible to define meta-dialogues, i.e. high-order dialogue composing dialogues together. This level of abstraction is very hard to obtain when using VoiceXML directly but is easily achieved with Rivr.

#### No additional tools required

Rivr only requires standard Java tools, no special software or other design-time environment. Java already offers tons of tools that can be applied to the Rivr dialogues: debuggers, profilers, coverage tools, javadoc, etc.

#### Flexibility

Rivr is designed not to get in your way. It can be integrated with any enterprise framework or other existing framework (like Spring Boot 3+). Many points of control has been defined in Rivr, you are never stuck. You can provide your own implementations for many concepts and you can override many classes to fit your custom context.

Rivr even works with VoiceXML proprietary extensions. You can customize generated VoiceXML as required by your VoiceXML platform and exploit vendor-specific features.
