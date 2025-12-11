# Classes

Message header and payload models for AMQP Tjenesteoversikt.

- [MsgHead.mmd](MsgHead.mmd) – Hodemelding wrapper

```mermaid
classDiagram
class MsgHead {
	+MsgInfo msgInfo
	+Document document
}

```

- [MsgInfo.mmd](MsgInfo.mmd) – Header metadata

```mermaid
classDiagram
class MsgInfo {
	+string msgId
	+Type type
	+Sender sender
	+Receiver receiver
	+Patient patient
	+Ack ack
}

```

- [TjenesteOversikt.mmd](TjenesteOversikt.mmd) – Service overview container

```mermaid
classDiagram
class TjenesteOversikt {
	+Tjeneste[] tjenester
}

```

- [Tjeneste.mmd](Tjeneste.mmd) – Individual service entry

```mermaid
classDiagram
class Tjeneste {
	+string id
	+string navn
	+bool digitalInnbyggertjeneste
	+RelaterteRoller relaterteRoller
}

```

- [RelaterteRoller.mmd](RelaterteRoller.mmd) – Related personnel roles

```mermaid
classDiagram
class RelaterteRoller {
	+Helsepersonell[] helsepersonell
}

```

- [Applikasjonskvittering.mmd](Applikasjonskvittering.mmd) – Application receipt

```mermaid
classDiagram
class Applikasjonskvittering {
	+string msgId
	+string status
	+string errorCode
}

```
