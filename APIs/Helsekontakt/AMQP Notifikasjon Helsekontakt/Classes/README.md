# Classes

Message header and FHIR resource snippets used in AMQP Notifikasjon Helsekontakt.

- [MsgHead.mmd](MsgHead.mmd) – Hodemelding wrapper

```mermaid
classDiagram
class MsgHead {
	+MsgInfo msgInfo
	+Document document
}

```

- [EpisodeOfCare.mmd](EpisodeOfCare.mmd) – FHIR EpisodeOfCare payload

```mermaid
classDiagram
class EpisodeOfCare {
	+string id
	+string status
	+Meta meta
	+Reference patient
	+Reference managingOrg
	+CareTeam careTeam
}

```

- [CareTeam.mmd](CareTeam.mmd) – Contained CareTeam

```mermaid
classDiagram
class CareTeam {
	+string name
	+Participant[] participant
}

```

- [Participant.mmd](Participant.mmd) – Care team participant

```mermaid
classDiagram
class Participant {
	+Role role
	+Reference member
}

```

- [AccessSecurity.mmd](AccessSecurity.mmd) – Access restriction codes

```mermaid
classDiagram
class AccessSecurity {
	<<enumeration>>
	N
	NORN_FORANS
	NORN_UNGDOM
}
note for AccessSecurity "N = Normal (both parents and youth)\nNORN_FORANS = Parents denied\nNORN_UNGDOM = Youth denied"

```
