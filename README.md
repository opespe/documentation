# o1.documentation
Documentation Repository for OPES

<strong>Version: 0.2.0 </strong> 

## Table of Contents

- [White Paper](./whitepaper/README.md)
  - [Activity](./whitepaper/activity/README.md)
  - [Consensus](./whitepaper/consensus/README.md)
  - [Glossary](./whitepaper/glossary/README.md)
  - [Managed Services](./whitepaper/managed_services/README.md)
  - [Tokenomics](./whitepaper/tokenomics/README.md)
  - [User Roles](./whitepaper/user_roles/README.md)
- Processes
  - [General DevOps](./processes/devops/README.md)
    - [Cloud Triggers](./processes/devops/cloud_triggers/README.md)
  - [Personal Node](./processes/personal/README.md)
    - [Onboarding](./processes/personal/onboarding/README.md)
    - [Supporting Access Nodes](./processes/personal/support_nodes/README.md)
    - [Sending Transactions](./processes/personal/transactions/README.md)
  - [Access Node](./processes/access/README.md)
    - [Onboarding](./processes/access/onboarding/README.md)
    - [Deployment](./processes/access/deployment/README.md)
    - [Claiming Rewards](./processes/access/claim_funds/README.md)
  - [Community Node](./processes/community/README.md)
    - [Onboarding](./processes/community/onboarding/README.md)
    - [Creation](./processes/community/creation/README.md)
    - [Deployment](./processes/community/deployment/README.md)
    - [Claiming Rewards](./processes/community/claim_funds/README.md)
  - [Infrastructure Node](./processes/infrastructure/README.md)
    - [Deployment](./processes/infrastructure/deployment/README.md)
    - [Claiming Rewards](./processes/infrastructure/claim_funds/README.md)
  - [OPES Blockchain Node](./processes/blockchain/README.md)
    - [Deployment](./processes/blockchain/deployment/README.md)
  - [Bug Reporting](./processes/bugfixes/README.md)
- Services
  - [High-Level Architecture](./services/README.md)
  - [Batch Service](./services/batching/README.md)
  - [Block Gateway](./services/block_gateway/README.md)
    - [API](./services/block_gateway/api/README.md)
  - [Infrastructure Node](./services/infrastructure/README.md)
    - [API](./services/infrastructure/api/README.md)
  - [OPES Service](./services/opes/README.md)
    - [API](./services/opes/api/README.md)
  - [Puzzle Service](./services/puzzle/README.md)
    - [API](./services/puzzle/api/README.md)

## Folder Structure

Services will be grouped based on if they are managed internally (opes_services) or externally (user_services).

### Services

Within each Service's directory, the following structure should be observed:

```
[Service Name]/
  - API/
    - README.md
    - [Route Name]_api.md
  - Configuration/
    - README.md
    - [Service Name]_deploy.md
  - README.md
  - Resources/
    - README.md
    - [Resource File]
  - Testing/
    - README.md
    - [Test Name]_test.md
```
 
Example Service:

```
example_service/
  - API
    - README.md
    - hello_world_api.md
    - goodbye_world_api.md
  - Configuration/
    - README.md
    - example_service_deploy.md
  - README.md
  - Resources/
    - README.md
    - responses.json
    - polite_responses.json
  - Testing/
    - README.md
    - setup_service_test.md
    - healthcheck_test.md
    - hello_world_test.md
    - goodbye_world_test.md
```


## Formats

Various templates are provided for creating new documentation. When creating a new document, copy the template to the working folder and complete the fields as indicated. Final documentation should follow the structure of the template as closely as possible, though it is recognized that there are cases where more or less information is appropriate or available.

### CI/CD Docs
Continuous Integration / Continuous Delivery Docs are written towards DevOps. 

[CI/CD Template](./templates/blank_deploy.md)


### API Docs
API documentation are written in clear, human-readable language to the outside developer.

[API Template](./templates/blank_api.md)

### Service Docs
Service docs are written towards internal developers. They may include terminology that is deprecated or inconsistent with marketing.

[Service Template](./templates/blank_service.md)

### Module Docs
Module docs are written towards internal developers. They describe software libraries that are not standalone services. They may include terminology that is deprecated or inconsistent with marketing.

[Module Template](./templates/blank_module.md)

### Testing Docs
Testing documents are written towards internal testers. They describe the process for testing each component or service. 

[Test Template](./templates/blank_test.md)

## Versioning

This repository conforms to the [Semantic Versioning](https://semver.org/) standard 

| Version | Changes | Example |
| ------- | ------- | ------- |
| Major | Previous documentation is incompatible with current implementation | A process adds required steps |
| Minor | Previous documentation is compatible with current implementaton | A process removed required steps, adds optional steps |
| Patch | Previous documentation matches current implementation exactly | A typo was fixed, grammar corrected, layout updated |
