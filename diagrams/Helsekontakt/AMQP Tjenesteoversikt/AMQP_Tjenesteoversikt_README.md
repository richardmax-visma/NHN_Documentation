# AMQP Tjenesteoversikt

**API Name:** DIALOG_INNBYGGER_TJENESTEOVERSIKT  
**Technology:** AMQP  
**Status:** In Production (since Feb 2017)  
**Use case:** Home care services (hjemmetjenester) only

## Overview

Sends health contact information to citizens via AMQP messaging. Originally called "Tjenesteoversikt" (Service Overview) because it provides an overview of health services the citizen receives.

## Prerequisites

- Sender must be able to mark services as digital citizen services
- Sender must be capable of electronic message exchange with Helsenorge.no

## Message Structure

### MsgHead (Header Message)

| Field      | Norwegian   | English                 |
| ---------- | ----------- | ----------------------- |
| `msgId`    | Meldings-ID | Message ID (unique)     |
| `type`     | Type        | Message type            |
| `sender`   | Avsender    | Sender info             |
| `receiver` | Mottaker    | Receiver info           |
| `patient`  | Pasient     | Patient info            |
| `ack`      | Kvittering  | Acknowledgment settings |

### TjenesteOversikt (Service Overview)

| Field       | Norwegian | English          |
| ----------- | --------- | ---------------- |
| `tjenester` | Tjenester | List of services |

### Tjeneste (Service)

| Field                      | Norwegian                 | English                           |
| -------------------------- | ------------------------- | --------------------------------- |
| `id`                       | ID                        | Service identifier                |
| `navn`                     | Navn                      | Service name                      |
| `digitalInnbyggertjeneste` | Digital innbyggertjeneste | Is digital citizen service (bool) |
| `relaterteRoller`          | Relaterte roller          | Related roles/personnel           |

### RelaterteRoller (Related Roles)

| Field            | Norwegian      | English                   |
| ---------------- | -------------- | ------------------------- |
| `helsepersonell` | Helsepersonell | Healthcare personnel list |

### Applikasjonskvittering (Application Receipt)

| Field       | Norwegian   | English                |
| ----------- | ----------- | ---------------------- |
| `msgId`     | Meldings-ID | Original message ID    |
| `status`    | Status      | Processing status      |
| `errorCode` | Feilkode    | Error code (if failed) |

## Flow

1. **Healthcare Provider** sends `TjenesteOversikt` message via AMQP
2. Message contains `MsgHead` (header) + `TjenesteOversikt` (payload)
3. **Helsenorge** receives and processes the message
4. **Helsenorge** returns `Applikasjonskvittering` (acknowledgment)

## Error Handling

If citizen is not digitally active, the acknowledgment will contain an error indicating the message cannot be processed.

## Standards

- Hodemelding v1.2: https://www.ehelse.no/standardisering/standarder/standard-for-hodemelding
- Applikasjonskvittering v1.1: https://ehelse.no/his80415-2012

## Sources

- Helsenorge for kommuner – hjemmetjenesten: https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/pages/1875804167/Helsenorge+for+kommuner+-+hjemmetjenesten
- Meldingsutveksling med Helsenorge: https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/pages/690913297/Meldingsutveksling+med+Helsenorge
