# E-kontakt (Electronic Contact)

AMQP-based bidirectional messaging between citizens and healthcare providers via Helsenorge.

**API Name:** `DIALOG_INNBYGGER_EKONTAKT`  
**Technology:** AMQP (Advanced Message Queuing Protocol)

## When to use

- Administrative, non-clinical dialogs with citizens.
- Either party (citizen or provider) needs to start or continue a threaded dialog.
- Attachments need to accompany the dialog.

## Channel and authentication

- Transport: AMQP on NHN messaging infrastructure.
- Auth/transport setup follows NHN AMQP requirements (cert-based). Use the queue configuration assigned by NHN.

## [Message flows](Ekontakt_Flow.mmd)

- Citizen-initiated: `ForespørselFraInnbygger` → `SvarFraHelsekontakt`.
- Provider-initiated: `ForespørselFraHelsekontakt` → `SvarFraInnbygger`.

## Diagrams

- Flow: [Ekontakt_Flow.mmd](Ekontakt_Flow.mmd)
- Citizen-initiated relations: [Relations/CitizenInitiatedRelations.mmd](Relations/CitizenInitiatedRelations.mmd)
- Provider-initiated relations: [Relations/ProviderInitiatedRelations.mmd](Relations/ProviderInitiatedRelations.mmd)
- Classes: [Classes folder](Classes/)

## Payloads and classes

Classes: [EkontaktMelding](Classes/EkontaktMelding.mmd), [Vedlegg](Classes/Vedlegg.mmd), [ForespørselFraInnbygger](Classes/ForespørselFraInnbygger.mmd), [SvarFraHelsekontakt](Classes/SvarFraHelsekontakt.mmd), [ForespørselFraHelsekontakt](Classes/ForespørselFraHelsekontakt.mmd), [SvarFraInnbygger](Classes/SvarFraInnbygger.mmd).

Core fields ([EkontaktMelding](Classes/EkontaktMelding.mmd)):

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

## [Attachments](Classes/Vedlegg.mmd)

| Format | MIME Type       | Notes     |
| ------ | --------------- | --------- |
| PDF    | application/pdf | Documents |
| JPG    | image/jpeg      | Images    |
| PNG    | image/png       | Images    |

## Sources

- Helsenorgetjenester overview: https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/pages/690749444/Helsenorgetjenester
- Meldingsutveksling med Helsenorge: https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/pages/690913297/Meldingsutveksling+med+Helsenorge
- Teknisk integrasjon med Helsenorge og PVK: https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/pages/691175425/Teknisk+integrasjon+med+Helsenorge+og+Personvernkomponenten+PVK
