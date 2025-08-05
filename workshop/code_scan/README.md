# Code Security Analysis (SAST/SCA) [🚧 Under construction]

This workshop module covers Static Application Security Testing (SAST) and Software Composition Analysis (SCA) to identify security vulnerabilities in application code and dependencies.

## What is SAST (Static Application Security Testing)?

SAST analyzes source code, bytecode, or binary code to identify security vulnerabilities without executing the program. It examines code patterns, data flow, and control flow to detect potential security issues.

## What is SCA (Software Composition Analysis)?

SCA identifies and analyzes open source components and third-party dependencies in applications to detect known vulnerabilities, license compliance issues, and outdated packages.

## Why is Code Security Important?

Malicious actors can exploit vulnerabilities in your code to gain unauthorized access, steal sensitive data, or disrupt your systems.

## Common Code Security Issues

### SAST Findings:
- **SQL Injection** - Unsafe database queries
- **Cross-Site Scripting (XSS)** - Unvalidated user input
- **Authentication Flaws** - Weak authentication mechanisms
- **Authorization Issues** - Missing access controls
- **Hardcoded Secrets** - Credentials in source code
- **Input Validation** - Missing or improper validation

### SCA Findings:
- **Known Vulnerabilities** - CVEs in dependencies
- **Outdated Packages** - Dependencies with security updates
- **License Issues** - Non-compliant licenses
- **Supply Chain Risks** - Malicious packages

## Tools Used in This Module

- [**Dependency Check**](https://github.com/dependency-check/DependencyCheck) - OWASP tool for Software Composition Analysis (SCA) to identify known vulnerabilities in dependencies

## Learning Objectives

By the end of this module, you will:
- Understand the difference between SAST and SCA
- Learn to configure and run security scanners
- Understand common vulnerability patterns
- Learn to integrate security scanning into CI/CD

## Security Checklist

- [ ] SAST integrated into CI/CD pipeline
- [ ] SCA scanning for all dependencies
- [ ] Regular dependency updates
- [ ] Security hotspots addressed
- [ ] False positive management
- [ ] Security metrics tracking
