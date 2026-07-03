# Task 3: Java Application Automation & CI/CD Pipeline using Gradle 🚀

This repository contains a streamlined Java application integrated with **Gradle** for automated build execution, dependency management, and automated continuous delivery (CD) utilizing **GitHub Actions**.

---

## 🛠️ Project Features & DevOps Principles

*   **Build Automation**: Utilizes Gradle to compile, test, and package the Java application seamlessly.
*   **Dependency Management**: Centralized dependency resolution via Maven Central configured in `build.gradle`.
*   **Continuous Integration (CI)**: GitHub Actions workflow triggers automatically on every code push to validate code compilation.
*   **Continuous Delivery (CD)**: Successfully generates production-ready `.jar` artifacts and safely deploys them to GitHub Artifact storage on successful builds.

---

## 📂 Project Structure

```text
java-gradle-task/
├── .github/
│   └── workflows/
│       └── gradle-ci.yml      # CI/CD Workflow Configuration
├── src/
│   └── main/
│       └── java/
│           └── com/
│               └── example/
│                   └── App.java  # Main Java Application File
├── build.gradle               # Gradle Build & Dependency Configuration
└── README.md                  # Project Documentation


1. Build & Dependency Setup (build.gradle)
The build file automates the build lifecycle and manages enterprise-standard dependencies (such as JUnit Jupiter for automated testing compliance):

plugins {
    id 'java'
    id 'application'
}

repositories {
    mavenCentral()
}

dependencies {
    testImplementation 'org.junit.jupiter:junit-jupiter:5.10.0'
}

application {
    mainClass = 'com.example.App'
}


CI/CD Automated Workflow:

name: Java Gradle CI & Continuous Delivery 🚀

on:
  push:
    branches: [ "main" ]

jobs:
  build-and-deliver:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Code
      uses: actions/checkout@v4

    - name: Set up JDK 17
      uses: actions/setup-java@v4
      with:
        java-version: '17'
        distribution: 'temurin'

    - name: Setup Gradle
      uses: gradle/actions/setup-gradle@v3

    - name: Build and Package Application
      run: gradle build

    - name: Upload Production JAR to Github Artifacts
      uses: actions/upload-artifact@v4
      with:
        name: java-production-build
        path: build/libs/*.jar
