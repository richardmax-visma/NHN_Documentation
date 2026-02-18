# Authentication

This section covers authentication methods used for integrating with Helsenorge and NHN services. Different APIs and protocols require different authentication approaches.

## Overview

### [HelseID Authentication](./HelseID_Auth/)

HelseID is Norway's national authentication service for the health sector. It's required for:

- System-to-system (machine-to-machine) API calls to NHN/Helsenorge
- User authentication flows for healthcare applications

**⚠️ As of December 1, 2025, all healthcare actors must use HelseID for system-to-system API access.**

Key features:

- OAuth 2.0 client credentials flow
- Bearer token-based authentication
- Support for Norwegian national ID providers

### [AMQP Authentication](./AMQP_Auth/)

AMQP authentication is used specifically for Helsenorge messaging via NHN's Tjenestebuss (RabbitMQ broker). This includes:

- E-kontakt messages
- Helsekontakt AMQP flows

Key features:

- TLS transport encryption (`amqps://` on port 5671)
- Username/password authentication (SASL PLAIN)
- Virksomhetssertifikat for message-level signing and encryption (not transport auth)
- Broker ACL-based queue/vhost access control
- No bearer tokens within AMQP frames

## Which authentication method do I need?

| Use Case                                 | Authentication Method |
| ---------------------------------------- | --------------------- |
| REST/FHIR API calls                      | HelseID               |
| AMQP messaging (E-kontakt, Helsekontakt) | AMQP Auth (TLS + username/password) |
| User login flows                         | HelseID               |
| Both messaging and APIs                  | Both methods          |

## Quick Links

- [HelseID Authentication Details](./HelseID_Auth/)
- [AMQP Authentication Details](./AMQP_Auth/)
- [Test Environments](../Test_Environments/)
