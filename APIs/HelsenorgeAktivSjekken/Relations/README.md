# Relations

Mermaid diagrams showing class relationships for HelsenorgeAktivSjekken.

- [RequestRelations.mmd](RequestRelations.mmd) – Request to context area mapping

```mermaid
classDiagram
	class Request {
		+string[] fnrListe
		+int omraade
	}

	class Omraade {
		<<enumeration>>
		HELSEHJELP = 3
		UNGDOM = 6
	}

	Request --> Omraade : omraade

```

- [ResponseRelations.mmd](ResponseRelations.mmd) – Response status composition

```mermaid
classDiagram
	class Response {
		+Map~String, ErAktivStatus~ erAktivListe
	}

	note for Response "erAktivListe key = fnr (national ID)"

	class ErAktivStatus {
		+bool erAktivSelv
		+bool erAktivViaAndre
		+bool tildeltFullmakt
	}

	Response *-- ErAktivStatus : contains

```
