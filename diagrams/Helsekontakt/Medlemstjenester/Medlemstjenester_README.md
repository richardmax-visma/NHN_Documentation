# Medlemstjenester (Membership Services)

**Technology:** FHIR (v4.0)  
**Endpoint:** `https://eksternapi.helsenorge.no/helsekontakter/api/v1`  
**Auth Scope:** Helsekontakter

## Overview

For organizations that offer the same health services to all their members. Sends health offerings and member lists to Helsenorge so citizens can access digital services like appointment management and provider communication.

## Authentication

Two options:

1. **HelseId** - Select scope "Helsekontakter" in self-service
2. **Helsenorge STS** - Pre-configure with public key

## Two-Step Process

### Step 1: Send Health Offerings (Helsetilbud)

Defines what health services members receive.

**FHIR Resources:**

| Resource              | Field               | Description                     | Required |
| --------------------- | ------------------- | ------------------------------- | -------- |
| **HealthcareService** | identifier          | Local GUID                      | ✅       |
|                       | active              | Is active                       |          |
|                       | name                | Service name (shown to citizen) | ✅       |
|                       | comment             | Description                     |          |
|                       | providedBy          | Ref to Organization             | ✅       |
|                       | endpoint.identifier | Communication partner ID        | ✅       |
| **Organization**      | identifier          | Org number (e.g., 948 554 062)  | ✅       |
|                       | name                | Organization name               | ✅       |
|                       | endpoint.id         | Business ID                     | ✅       |
| **Location**          | address.line        | Street address                  | ✅       |
|                       | address.city        | City                            | ✅       |
|                       | address.postalCode  | Postal code                     | ✅       |
|                       | telecom.value       | Phone/URL                       |          |

### Step 2: Send Member List (Medlemsliste)

Links members to the health offerings.

**FHIR Patient Resource:**

| Field                           | Description                          | Required |
| ------------------------------- | ------------------------------------ | -------- |
| identifier                      | National ID (fødselsnummer/d-nummer) | ✅       |
| contact.organization.identifier | Organization number                  | ✅       |
| contact.period.start            | Service start date                   | ✅       |
| contact.period.end              | Service end date                     | ✅       |

## Non-Functional Requirements

| Type                      | Requirement                          |
| ------------------------- | ------------------------------------ |
| Response time (offerings) | < 3 sec for 99%                      |
| Response time (members)   | < 10 sec for 99%                     |
| Timeout (members)         | 15 sec                               |
| Retry                     | Must handle resending if no response |

## Environments

| Environment | URL                                                              |
| ----------- | ---------------------------------------------------------------- |
| MAS-01      | https://eksternapi-hn-mas-01.int-hn.nhn.no/helsekontakter/api/v1 |
| MAS-02      | https://eksternapi-hn-mas-02.int-hn.nhn.no/helsekontakter/api/v1 |
| TEST1       | https://eksternapi.hn.test.nhn.no/helsekontakter/api/v1          |
| TEST2       | https://eksternapi.hn2.test.nhn.no/helsekontakter/api/v1         |
| PROD        | https://eksternapi.helsenorge.no/helsekontakter/api/v1           |

## Notes

- If citizen hasn't consented to Helsenorge, their info cannot be stored
- Sender should track digital status and periodically retry inactive members
- Split member lists into configurable batches to avoid timeouts

## Sources

- Medlemstjenester (official): https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/pages/24018962/Medlemstjenester
