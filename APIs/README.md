# APIs

Documentation for NHN/DigiHelse integrations grouped by domain. Each subfolder has its own detailed README and Mermaid diagrams.

## Available APIs

- [HelsenorgeAktivSjekken](./HelsenorgeAktivSjekken/) — Check if a citizen is digitally reachable on Helsenorge before sending messages.
- [Helsekontakt](./Helsekontakt/) — Citizen-facing health contact flows (AMQP notifications, service overview, membership services).
- [E-kontakt](./Ekontakt/) — Administrative messaging between citizens and providers over AMQP.

## Prerequisites

- Authentication: [HelseID](../Authentication/HelseID_Auth/) for REST/FHIR; [AMQP mTLS](../Authentication/AMQP_Auth/) for messaging queues.
- Environment endpoints: see [Test Environments](../Test_Environments/README.md).

## Diagrams

Mermaid diagrams are included in each subfolder for flows and data models. Open them in VS Code (Mermaid Preview) or the Mermaid Live Editor.
