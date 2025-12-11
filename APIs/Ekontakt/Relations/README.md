# Relations

Mermaid class relationship diagrams for E-kontakt flows.

- [CitizenInitiatedRelations.mmd](CitizenInitiatedRelations.mmd) – Citizen starts dialog

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

class Vedlegg {
	+String filnavn
	+String mimeType
	+byte[] innhold
	+int storrelse
}

class ForespørselFraInnbygger {
	+String innbyggerId
	+String tjeneste
	+String meldingInnhold
	+Vedlegg[] vedlegg
}

class SvarFraHelsekontakt {
	+String dialogId
	+String svarInnhold
	+DateTime sendt
	+Vedlegg[] vedlegg
}

EkontaktMelding <|-- ForespørselFraInnbygger
EkontaktMelding <|-- SvarFraHelsekontakt
EkontaktMelding "1" *-- "0..*" Vedlegg : vedlegg

```

- [ProviderInitiatedRelations.mmd](ProviderInitiatedRelations.mmd) – Provider starts dialog

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

class Vedlegg {
	+String filnavn
	+String mimeType
	+byte[] innhold
	+int storrelse
}

class ForespørselFraHelsekontakt {
	+String innbyggerId
	+String tjeneste
	+String meldingInnhold
	+Vedlegg[] vedlegg
}

class SvarFraInnbygger {
	+String dialogId
	+String svarInnhold
	+DateTime sendt
	+Vedlegg[] vedlegg
}

EkontaktMelding <|-- ForespørselFraHelsekontakt
EkontaktMelding <|-- SvarFraInnbygger
EkontaktMelding "1" *-- "0..*" Vedlegg : vedlegg

```
