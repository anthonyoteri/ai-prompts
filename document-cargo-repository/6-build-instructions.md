You are a senior AI engineer responsible for generating a project architecture guide. The goal is to generate a proper guide in markdown format at:

`{final_output_file}`

This file will serve as complete technical documentation for the project in this codebase.  It must be extensive.

You must synthesize the following source materials:

- `./{output_folder}/1-techstack.md`: Provides tech choices and domain boundaries
- `./{output_folder}/2-file-categorization.json`: Lists the file categories and their canonical examples
- `./{output_folder}/5-style-guides/{category}.md`: Describes unique conventions for each file category
- `./{output_folder}/3-architectural-domains.json`: Defines how domains like `ui`, `routing`, `data-layer`, etc. are implemented, along with constraints and required patterns

## Your Output: `{final_output_file}`

This file must include:

### 1. **Introduction & System Overview**

Explain the purpose of this document:
- Project goals, context, and high-level architecture diagram
- Intended use cases and target environments
- It is intended to serve as a technical overview of the project, documenting the project with sufficient details that a reader can come away with a good understanding of how the project works.
- It is based only on actual, observed patterns from the codebase — not invented practices.

### 2. **System Requirements**
- Supported platforms, prerequisites, and dependencies
- Hardware, OS, and network requirements

### 3. **Installation & Setup**
- Step-by-step instructions for local, staging, and production setups
- Environment variables, secrets, config files, and directory structure
- Example configuration files and annotated samples

### 4. **Configuration**
- All runtime options, environment variables, and config file keys
- How to customize for different environments
- Security and secret management practices

### 5. **Running & Operating**
- How to start, stop, and monitor all services
- Common operational workflows (deploy, upgrade, rollback, recover)
- Troubleshooting guide for common errors and failure modes

### 6. **File Category Reference**

For each category in `2-file-categorization.json`:

- Include a comprehensive summary of the file in plain English.  Include in this overview, any significant features, patterns and public APIs.
- List out all public symbols exported from this module if any, along with a brief description for each.
- Give usage examples for key public APIs provided by the file where appropriate
- Summarize key conventions based on its corresponding `5-style-guides/{category}.md`

### 7. **Background Tasks & Event Processing**
- Description of all background jobs (pollers, aggregators, confd monitor)
- How event sourcing, snapshotting, and recovery work
- Failure handling and recovery strategies

### 8. **Security**
- TLS setup, JWT authentication, RBAC, and best practices
- Container security, image scanning, and runtime hardening

### 9. **Monitoring & Observability**
- Metrics, tracing, logging, and alerting
- How to integrate with external monitoring systems
- Example queries and dashboards

### 10. **High Level Architecutre**

From the`2-file-categorization.json`, `3-architectural-domains.json` and `4-domains/{domain}.md` files, determine how all key components in teh architecture fit together.

- What are all the key components?
- Given every component, how does it connect to each other component?
- What APIs are in use between each component.

This section should include mermaid diagrams and sufficient documentation to outline
all the major flows, and relationships used by the general application architecture.

> You may skip any minor components such as linking Error and Exception types, minor utility funcitons, etc.

This section should give the reader enough of an understanding to follow the application flow from the main entrypoint to the end of the program.

A subsection of this chapter should detail the common error flows.  Keep this at a high level, as specific implementation details for ever error case in every function would be overwhelming to a reader.  Stick to the major error flows here.

### 11. Common Patterns

This section describes the common design patterns in use throughout the application.

- What are the common design patterns in use throughout the application?
- List 1-2 examples of where and how each are used in the code.
- Keep this relatively high-level. This section is designed to give new developers some basic preparation information as to what they patterns they should be familiar with to be able to understand the code.

### 12. Testing

This section should detail the projects testing frameworks.

- List out all testing frameworks used.
- Summarize the general use-case for the testing framework, e.g. Python tests using pytest for system-level testing, Unit tests using Rust's built-in test framework, etc.
- Mention which areas of the code are sufficiently covered with test cases, and which areas may be missed.
- If there are any documented dependencies for runnign the tests such as external services that must be started, ensure that information ends up in this document.
- Be sure to document how to run the tests.  Developers need to know this information.  If there are examples for how to run the tests, include those examples here.  They should be setup such that a developer could copy and paste these commands to execute the test framework.

### 13. **CI/CD & Deployment**
- Full pipeline walkthrough (GitHub Actions, Jenkins, etc.)
- Artifact management, secrets, and environment promotion
- Containerization details, Helm/Ansible usage, upgrade/migration guides

### 14. **FAQ & Best Practices**
- Common questions, edge cases, and operational tips
- Rationale for major design decisions and trade-offs

### 15. **Styleguide**

Using the files in `./{output_folder}/5-style-guides/` generate a comprehensive and detailed style guide for each language used in the project.  This should list all common conventions and style rules currently in use in the project.

- Be detailed here.
- If a convention is being followed it MUST be listed in this guide.
- **Do not** include invented style rules.  Use only those that are supported by the codebase.

There should be one styleguide chapter **PER LANGUAGE** in use in the project.  You may omit guides for any language that are used very sparingly.  The rule of thumb is that if the language is used in more than about 10% of the overall codebase, it **MUST** have a styleguide chapter.  You may skip languages such as Makefiles, Shell scripts, etc., if they are only used for supporting utilities and build scripts.

### 16. Appendix

If there are automations such as Makefiles, Justfiles, etc that automate day-to-day
tasks such as building, runnign test suites, linting the code, etc. Be sure to document each command in an appendix.  A simple table showing the list of commands, and brief descriptions of each is acceptable here.

- Additional appendices should include but are not limited to:
  - Table of dependencies, listing version and licensing information if applicable.
  - Links to source code, relevant external and internal documentation.
  - Links to documentation and source code for each library in use in the codebase.
  - Brief description of any helper scripts and tooling that is included with the projects.
  - Any relevant software necessary for a developer to setup their environment, such as Docker, Podman, IDEs, Text editors, command line testing tools, etc.

## ⚠️ Requirements

- **Do not** include invented best practices
- **Do not** list categories or conventions that aren’t supported by the codebase
- **Do not** omit any categories or domains defined in the analysis
- Use narrative explanations, not just lists—explain the why and how.
- Include annotated code/configuration snippets and real-world examples.
- Provide diagrams for architecture, data flow, CI/CD, and deployment.
- Cover edge cases, limitations, and recovery strategies.
- Structure the document for onboarding, daily operations, and troubleshooting.
- Make the guide actionable for operators, developers, and maintainers.
- Cross-reference and synthesize information from all previous outputs in `./{output_dir}/`.
- **Do not** skip sections, or limit output due to complexity or time. Completeness is **mission-critical**.

To clarify further, if `{final_output_file}` already exists, overwrite it.
