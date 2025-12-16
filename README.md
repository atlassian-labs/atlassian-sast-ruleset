# Atlassian SAST Ruleset

[![Atlassian license](https://img.shields.io/badge/license-LGPL%202.1-blue.svg?style=flat-square)](LICENSE) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](CONTRIBUTING.md)

A comprehensive collection of **Static Application Security Testing (SAST) rules** designed specifically for Java enterprise applications commonly used within Atlassian's technology stack. This ruleset leverages [Semgrep](https://semgrep.dev/) to detect security vulnerabilities, insecure patterns, and potential attack vectors in enterprise Java codebases.

## Usage

Run the complete ruleset against your Java codebase:

```bash
# Scan entire project
semgrep --config=atlassian-sast-ruleset/sast-rules/ /path/to/your/java/project

# Scan specific directories
semgrep --config=atlassian-sast-ruleset/sast-rules/ src/main/java/

# Run specific rule categories
semgrep --config=atlassian-sast-ruleset/sast-rules/atlassian-internal-spring-security.yaml src/
```

**Example output:**
```
Found 3 findings.

src/main/java/TemplateController.java
  int-freemarker-tmpl-loading
    This FreeMarker code may be vulnerable to Server-Side Template Injection (SSTI)...

src/main/java/DeserializeService.java
  int-java-io-serde  
    Insecure deserialization detected: ObjectInputStream.readObject() poses significant security risks...
```

**CI/CD Integration:**
```yaml
# GitHub Actions example
- name: Run Atlassian SAST Rules
  run: |
    pip install semgrep
    semgrep --config=atlassian-sast-ruleset/sast-rules/ --error --quiet src/
```

## Installation

### Prerequisites
- [Semgrep](https://semgrep.dev/docs/getting-started/) installed locally or in CI/CD
- Java codebase (Java 8+)

### Setup

1. **Clone the ruleset:**
```bash
git clone https://github.com/atlassian/atlassian-sast-ruleset.git
cd atlassian-sast-ruleset
```

2. **Install Semgrep** (if not already installed):
```bash
# Using pip
pip install semgrep

# Using Homebrew (macOS)
brew install semgrep

# Using npm
npm install -g @semgrep/cli
```

3. **Verify installation:**
```bash
semgrep --config=sast-rules/ --dryrun
```

## Documentation

### Rule Coverage

This ruleset contains **37 security rules** across **11 categories**:

| Category | Rules | Focus Area |
|----------|-------|------------|
| **FreeMarker** | 2 | Server-Side Template Injection (SSTI) |
| **Jackson** | 2 | JSON deserialization vulnerabilities, XXE |
| **Java I/O** | 4 | Object deserialization, file path traversal |
| **JNDI** | 3 | JNDI injection, insecure lookups |
| **JMX** | 2 | Insecure JMX configuration |
| **Soy Templates** | 1 | HTML autoescaping bypass |
| **Spring Core** | 1 | Insecure property editors |
| **Spring EL** | 3 | Expression Language injection |
| **Spring Security** | 4 | Authentication/authorization bypasses |
| **Velocity** | 5 | Template injection vulnerabilities |
| **XStream** | 10 | XML deserialization attacks |

### Vulnerability Types Detected

- **🎯 Server-Side Template Injection (SSTI)** - FreeMarker, Velocity, Soy
- **💉 Injection Attacks** - JNDI, SpEL, command injection
- **🔓 Insecure Deserialization** - Java native, Jackson, XStream
- **📁 Path Traversal** - Arbitrary file read/write
- **🛡️ Authentication Bypass** - Spring Security misconfigurations
- **⚠️ XXE Vulnerabilities** - XML External Entity attacks

### Rule Severity Levels

- **ERROR (High):** Critical vulnerabilities requiring immediate attention
- **WARNING (Medium):** Important security issues that should be addressed
- **INFO (Low):** Security best practices and potential improvements

## Contributions

Contributions to Atlassian SAST Ruleset are welcome! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for details.

## License

Copyright (c) 2025 Atlassian US., Inc.
LGPL 2.1 licensed, see [LICENSE](LICENSE) file.

<br/>

[![With ❤️ from Atlassian](https://raw.githubusercontent.com/atlassian-internal/oss-assets/master/banner-cheers.png)](https://www.atlassian.com)
