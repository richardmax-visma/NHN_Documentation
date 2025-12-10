# E-kontakt (Electronic Contact)

## Overview

E-kontakt is an AMQP-based bidirectional messaging service that enables secure communication between citizens and healthcare providers through Helsenorge.

**API Name:** `DIALOG_INNBYGGER_EKONTAKT`  
**Technology:** AMQP (Advanced Message Queuing Protocol)

## Features

- **Bidirectional Communication:** Both citizens and healthcare providers can initiate conversations
- **Threaded Dialogs:** Messages are grouped by `dialogId` for organized conversations
- **Attachment Support:** PDF, JPG, PNG files can be attached to messages
- **Administrative Contact:** Used for non-clinical administrative communication

## Diagrams

### Flow Diagram

See [Ekontakt_Flow.mmd](./Ekontakt_Flow.mmd) for the message flow visualization.

### Class Diagram

See [Ekontakt_Classes.mmd](./Ekontakt_Classes.mmd) for data model.

## Message Types

### Citizen-Initiated Flow

1. **ForespørselFraInnbygger** (Request from Citizen) - Citizen sends initial message
2. **SvarFraHelsekontakt** (Response from Health Contact) - Provider responds

### Healthcare-Initiated Flow

1. **ForespørselFraHelsekontakt** (Request from Health Contact) - Provider sends initial message
2. **SvarFraInnbygger** (Response from Citizen) - Citizen responds

## Field Translations

| Norwegian    | English     | Description                   |
| ------------ | ----------- | ----------------------------- |
| dialogId     | Dialog ID   | Unique thread identifier      |
| meldingsId   | Message ID  | Unique message identifier     |
| tema         | Topic       | Subject of the message        |
| innhold      | Content     | Message body                  |
| opprettet    | Created At  | Timestamp                     |
| avsenderType | Sender Type | Who sent the message          |
| vedlegg      | Attachments | List of attached files        |
| filnavn      | Filename    | Attachment filename           |
| storrelse    | Size        | File size in bytes            |
| innbyggerId  | Citizen ID  | National ID (fødselsnummer)   |
| tjeneste     | Service     | Healthcare service identifier |
| sendt        | Sent        | Send timestamp                |

## Attachment Support

| Format | MIME Type       | Notes     |
| ------ | --------------- | --------- |
| PDF    | application/pdf | Documents |
| JPG    | image/jpeg      | Images    |
| PNG    | image/png       | Images    |

## Sources

- Helsenorgetjenester overview: https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/pages/690749444/Helsenorgetjenester
- Meldingsutveksling med Helsenorge: https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/pages/690913297/Meldingsutveksling+med+Helsenorge
- Teknisk integrasjon med Helsenorge og PVK: https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/pages/691175425/Teknisk+integrasjon+med+Helsenorge+og+Personvernkomponenten+PVK
