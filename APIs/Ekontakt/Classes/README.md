# Classes

Payload and helper models for E-kontakt AMQP messaging.

- [EkontaktMelding.mmd](EkontaktMelding.mmd) – Base message structure

```mermaid
classDiagram
class EkontaktMelding {
	+String dialogId
	+String meldingsId
	+String tema
	+String innhold
	+DateTime opprettet
	+String avsenderType
	+Vedlegg[] vedlegg
}
note for EkontaktMelding "dialogId: dialog ID (thread)\nmeldingsId: message ID\ntema: topic/subject\ninnhold: content\nopprettet: created at\navsenderType: sender type\nvedlegg: attachments"

```

- [Vedlegg.mmd](Vedlegg.mmd) – Attachment metadata/content

```mermaid
classDiagram
class Vedlegg {
	+String filnavn
	+String mimeType
	+byte[] innhold
	+int storrelse
}
note for Vedlegg "filnavn: filename\nmimeType: PDF/JPG/PNG\ninnhold: content (base64)\nstorrelse: size in bytes"

```

- [ForespørselFraInnbygger.mmd](ForespørselFraInnbygger.mmd) – Citizen-initiated request

```mermaid
classDiagram
class ForespørselFraInnbygger {
	+String innbyggerId
	+String tjeneste
	+String meldingInnhold
	+Vedlegg[] vedlegg
}
note for ForespørselFraInnbygger "Request from Citizen"

```

- [SvarFraHelsekontakt.mmd](SvarFraHelsekontakt.mmd) – Provider response

```mermaid
classDiagram
class SvarFraHelsekontakt {
	+String dialogId
	+String svarInnhold
	+DateTime sendt
	+Vedlegg[] vedlegg
}
note for SvarFraHelsekontakt "Response from Health Contact"

```

- [ForespørselFraHelsekontakt.mmd](ForespørselFraHelsekontakt.mmd) – Provider-initiated request

```mermaid
classDiagram
class ForespørselFraHelsekontakt {
	+String innbyggerId
	+String tjeneste
	+String meldingInnhold
	+Vedlegg[] vedlegg
}
note for ForespørselFraHelsekontakt "Request from Health Contact"

```

- [SvarFraInnbygger.mmd](SvarFraInnbygger.mmd) – Citizen response

```mermaid
classDiagram
class SvarFraInnbygger {
	+String dialogId
	+String svarInnhold
	+DateTime sendt
	+Vedlegg[] vedlegg
}
note for SvarFraInnbygger "Response from Citizen"

```
