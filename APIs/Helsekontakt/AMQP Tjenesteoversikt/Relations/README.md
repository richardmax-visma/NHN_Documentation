# Relations

Mermaid diagrams showing message and payload relationships for AMQP Tjenesteoversikt.

- [MsgHeadRelations.mmd](MsgHeadRelations.mmd) – Hodemelding linkages

```mermaid
classDiagram

class MsgHead {
	+MsgInfo msgInfo
	+Document document
}

class MsgInfo {
	+string msgId
	+Type type
	+Sender sender
	+Receiver receiver
	+Patient patient
	+Ack ack
}

class TjenesteOversikt {
	+Tjeneste[] tjenester
}

class Tjeneste {
	+string id
	+string navn
	+bool digitalInnbyggertjeneste
	+RelaterteRoller relaterteRoller
}

class RelaterteRoller {
	+Helsepersonell[] helsepersonell
}

MsgHead *-- MsgInfo : msgInfo
MsgHead *-- TjenesteOversikt : document
TjenesteOversikt *-- Tjeneste : tjenester
Tjeneste *-- RelaterteRoller : relaterteRoller

```

- [ApplikasjonskvitteringRelations.mmd](ApplikasjonskvitteringRelations.mmd) – Receipt structure

```mermaid
classDiagram

class Applikasjonskvittering {
	+string msgId
	+string status
	+string errorCode
}

note for Applikasjonskvittering "Returned by Helsenorge after processing MsgHead"

```
