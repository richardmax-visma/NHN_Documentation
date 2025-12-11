# Classes

Domain models for HelsenorgeAktivSjekken requests and responses.

- [Request.mmd](Request.mmd) – Request payload fields

```mermaid
classDiagram
	class Request {
		+string[] fnrListe
		+int omraade
	}

```

- [Omraade.mmd](Omraade.mmd) – Context area enum

```mermaid
classDiagram
	class Omraade {
		<<enumeration>>
		HELSEHJELP = 3
		UNGDOM = 6
	}

```

- [Response.mmd](Response.mmd) – Response wrapper with status map

```mermaid
classDiagram
	class Response {
		+Map~String, ErAktivStatus~ erAktivListe
	}

	note for Response "erAktivListe key = fnr (national ID)"

```

- [ErAktivStatus.mmd](ErAktivStatus.mmd) – Activity status flags

```mermaid
classDiagram
	class ErAktivStatus {
		+bool erAktivSelv
		+bool erAktivViaAndre
		+bool tildeltFullmakt
	}

```
