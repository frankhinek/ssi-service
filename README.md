[![godoc ssi-service](https://img.shields.io/badge/godoc-ssi--service-blue)](https://github.com/TBD54566975/ssi-service)
[![go version 1.17.6](https://img.shields.io/badge/go_version-1.17.6-brightgreen)](https://go.dev/)
[![license Apache 2](https://img.shields.io/badge/license-Apache%202-black)](https://github.com/TBD54566975/ssi-service/blob/main/LICENSE)
[![issues](https://img.shields.io/github/issues/TBD54566975/ssi-service)](https://github.com/TBD54566975/ssi-service/issues)
![push](https://github.com/TBD54566975/ssi-service/workflows/ssi-service-ci/badge.svg?branch=main&event=push)

# ssi-service

## Introduction

The Self Sovereign Identity Service (SSIS) facilitates all things relating to [DIDs](https://www.w3.org/TR/did-core/)
and [Verifiable Credentials](https://www.w3.org/TR/vc-data-model) -- in a box! The service is a part of a larger
Decentralized Web Platform architecture which you can learn more about in our
[collaboration repo](https://github.com/TBD54566975/collaboration). The SSI Service is a RESTful web service that
wraps the [ssi-sdk](https://github.com/TBD54566975/ssi-sdk). The core functionality of the SSIS includes,
but is not limited to: interacting with the standards around Verifiable Credentials, Credential Revocations, requesting
Credentials, exchanging Credentials, data schemas for Credentials and other verifiable data, messaging using
Decentralized Web Nodes, and usage of Decentralized Identifiers. Using these core standards, the SSIS enables robust
functionality to facilitate all verifiable interactions such as creating, signing, issuing, curating, requesting,
revoking, exchanging, validating, verifying credentials in varying degrees of complexity.

![ssi-sdk](doc/ssi-service.png)

## Configuration

Configuration is managed using
a [TOML](https://toml.io/en/) [file](https://github.com/TBD54566975/ssi-service/blob/main/config/config.toml). There are
sets of configuration values for the server (e.g. which port to listen on), the services (e.g. which database to use),
and each service. Each service may define specific configuration, such as which DID methods are enabled for the DID
service.

## Build & Test

This project uses [mage](https://magefile.org/), please
view [CONTRIBUTING](https://github.com/TBD54566975/ssi-service/blob/main/CONTRIBUTING.md) for more information.

After installing mage, you can build and test the SDK with the following commands:

```
mage build
mage test
```

A utility is provided to run _clean, build, and test_ in sequence with:

```
mage cbt
```

## Continuous Integration

CI is managed via [GitHub Actions](https://github.com/TBD54566975/ssi-service/actions). Actions are triggered to run
for each Pull Request, and on merge to `main`. You can run CI locally using a tool
like [act](https://github.com/nektos/act).

## Deployment

The service is packaged as a [Docker container](https://www.docker.com/), runnable in a wide variety of
environments. [Docker Compose](https://docs.docker.com/compose/) is used for simplification and orchestration. To run
the service, you can use the following command, which will start the service on port `8080`:

```shell
mage run
```

Or, you can run docker-compose yourself:

```shell
cd build && docker-compose up 
```

### Health and Readiness Checks

You should then be able to send requests as follows:

Note: port 3000 is used by default, specified in `config.toml`, for the SSI Service process. If you're running via `mage run` or docker compose, the port to access will be `8080`.

The command below will give you a health check, if the status is OK then you are up.

```shell
 ~ curl localhost:3000/health
{"status":"OK"}
```

The command below will tell if you all the services (credential, did, and schema) are up and ready.
```aidl
~ curl localhost:8080/readiness
{
    "status": {
        "status": "ready",
        "message": "all service ready"
    },
    "serviceStatuses": {
        "credential": {
            "status": "ready"
        },
        "did": {
            "status": "ready"
        },
        "schema": {
            "status": "ready"
        }
    }
}
```

## REST Endpoints

You can find more rest endpoints by checking out the swagger docs at:
http://localhost:8002/docs

Note: Your port by differ, the range of the ports for swagger are between 8002 and 8080.

## What's Supported?

- [x] [DID Management](https://www.w3.org/TR/did-core/)
    - Using [did:key](https://w3c-ccg.github.io/did-method-key/)
- [x] [Verifiable Credential Schema](https://w3c-ccg.github.io/vc-json-schemas/v2/index.html) Management
- [ ] [Verifiable Credential](https://www.w3.org/TR/vc-data-model) Issuance & Verification
- [ ] Requesting, Receiving, and the Validation of Verifiable Claims
  using [Presentation Exchange](https://identity.foundation/presentation-exchange/)
- [ ] Applying for Verifiable Credentials using [Credential Manifest](https://identity.foundation/credential-manifest/)
- [ ] Revocations of Verifiable Credentials using the [Status List 2021](https://w3c-ccg.github.io/vc-status-list-2021/)
- [ ] [Decentralized Web Node](https://identity.foundation/decentralized-web-node/spec/) Messaging

## Design Thinking

The design of the service, at present, assumes it will be run by a single entity. Additional work is needed
around authentication and authorization schemes to access the service and its functionalities, possible User Interfaces
to use the service, and much more!
Please [open a discussion](https://forums.tbd.website/c/self-sovereign-identity-developers/7)
if you are interested in helping shape the future of this project.

## Contributing

This project is fully open source, and we welcome contributions! For more information please see
[CONTRIBUTING](https://github.com/TBD54566975/ssi-service/blob/main/CONTRIBUTING.md). Our current thinking about the
development of the library is captured in
[GitHub Issues](https://github.com/TBD54566975/ssi-service/issues).

## Project Resources

| Resource                                   | Description                                                                   |
|--------------------------------------------|-------------------------------------------------------------------------------|
| [CODEOWNERS](https://github.com/TBD54566975/ssi-service/blob/main/CODEOWNERS)                 | Outlines the project lead(s)                                                  |
| [CODE_OF_CONDUCT.md](https://github.com/TBD54566975/ssi-service/blob/main/CODE_OF_CONDUCT.md) | Expected behavior for project contributors, promoting a welcoming environment |
| [CONTRIBUTING.md](https://github.com/TBD54566975/ssi-service/blob/main/CONTRIBUTING.md)       | Developer guide to build, test, run, access CI, chat, discuss, file issues    |
| [GOVERNANCE.md](https://github.com/TBD54566975/ssi-service/blob/main/GOVERNANCE.md)           | Project governance                                                            |
| [SECURITY.md](https://github.com/TBD54566975/ssi-service/blob/main/SECURITY.md)               | Vulnerability and bug reporting                                               |
| [LICENSE](https://github.com/TBD54566975/ssi-service/blob/main/LICENSE)                       | Apache License, Version 2.0                                                   |
