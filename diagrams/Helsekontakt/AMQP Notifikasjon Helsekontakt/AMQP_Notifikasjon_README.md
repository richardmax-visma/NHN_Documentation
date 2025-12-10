# AMQP Notifikasjon Helsekontakt

**API Name:** NOTIFIKASJON_INNBYGGER_HELSEKONTAKT  
**Technology:** AMQP + FHIR  
**Status:** In Production (since Apr 2023)  
**Use case:** General health contact notifications (new solution, under pilot)

## Overview

Sends new or updated health contact information to citizens. The health contact (Helsekontakt) enables digital dialog between citizen and healthcare provider.

## Prerequisites

- Sender must be registered in Address Registry with Level 2 HerId
- Sender must support AMQP message exchange with Helsenorge

## Message Structure

### MsgHead (Header)

Contains sender, receiver, and patient info. The actual health contact is in the Document section as FHIR resource.

| Element         | Description             |
| --------------- | ----------------------- |
| MsgId           | Unique message ID       |
| Type            | Message type            |
| Ack             | Acknowledgment settings |
| Sender/Receiver | Organization info       |
| Patient         | Patient info            |
| Document        | FHIR EpisodeOfCare      |

### FHIR Resources

Uses two FHIR resources:

#### EpisodeOfCare

| Field                | Description                          |
| -------------------- | ------------------------------------ |
| id                   | Episode identifier                   |
| status               | Current status                       |
| meta.security        | Access restriction (for youth 12-16) |
| patient              | Reference to patient                 |
| managingOrganization | Healthcare organization              |
| careTeam             | Contained CareTeam                   |

#### CareTeam (contained)

| Field       | Description                        |
| ----------- | ---------------------------------- |
| name        | Team/service name                  |
| participant | List of healthcare personnel/roles |

### AccessSecurity Enum (meta.security)

For patients aged 12-15, must specify access restrictions:

| Code        | Norwegian                 | English                            |
| ----------- | ------------------------- | ---------------------------------- |
| N           | Normal                    | Both parents and youth have access |
| NORN_FORANS | Nektet, foreldreansvarlig | Parents denied (youth only)        |
| NORN_UNGDOM | Nektet, ungdom            | Youth denied (parents only)        |

_Source: Volven kodeverk 9603_

## Dialog Categorization (New Feature - Nov 2025)

Health contacts can now specify dialog categories:

- Helps EPJ route incoming messages to correct personnel
- Citizen sees category options when sending messages
- If no categories defined, feature is hidden from citizen

Implemented via CareTeam participants with different roles.

## Flow

1. **Healthcare System** sends notification via AMQP
2. Message contains `MsgHead` + FHIR `EpisodeOfCare`
3. **Helsenorge** processes and returns acknowledgment
4. Citizen can now use digital services (dialog, appointments)
5. Citizen messages flow back via AMQP Dialog

## Standards

- Hodemelding v1.2
- FHIR EpisodeOfCare: http://helsenorge.no/fhir/StructureDefinition/hn-specialist-EpisodeOfCare
- FHIR CareTeam: http://helsenorge.no/fhir/StructureDefinition/hn-specialist-EpisodeOfCare_containedCareTeam

## Sources

- AMQP Notifikasjon Helsekontakt: https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/pages/1975418911/AMQP+Notifikasjon+Helsekontakt
- Meldingsutveksling med Helsenorge: https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/pages/690913297/Meldingsutveksling+med+Helsenorge
