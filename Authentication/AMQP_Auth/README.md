# AMQP Authentication (NHN messaging)

Transport security for Helsenorge messaging (E-kontakt, Helsekontakt AMQP flows) uses mutual TLS with NHN-issued certificates and broker ACLs—no bearer tokens inside AMQP frames.

## What you need

- NHN-issued client certificate and private key (Virksomhetssertifikat) registered for Tjenestebuss.
- Trust chain for NHN/CA (Buypass/Commfides) installed so the broker cert is trusted.
- Queue/virtual host permissions from NHN (tb.test.nhn.no / tb.nhn.no, port 5671).
- Current Helsenorge.Messaging client library (≥ 6.0.3) if you use their SDK.

## How it works

- Client presents cert/key during TLS handshake to Tjenestebuss (RabbitMQ). Broker authenticates via the client cert subject and applies queue/vhost ACLs.
- Once the TLS channel is up, AMQP messages carry no bearer/JWT tokens.
- Certs are long-lived (until expiry/rotation); each connection re-handshakes TLS.

## Key endpoints (test)

- AMQP: `tb.test.nhn.no:5671`
- HelseID token (if you also call REST/FHIR APIs): `https://helseid-sts.test.nhn.no/connect/token`

## References

- Meldingsutveksling med Helsenorge: https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/pages/690913297/Meldingsutveksling+med+Helsenorge
- Krav til oppdatert versjon av Helsenorge Messaging: https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/pages/2904064001/Krav+til+oppdatert+versjon+av+Helsenorge+Messaging
- Krav til bruk av HelseID for system-til-system tilgang til APIer (for REST/FHIR side): https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/pages/2663776258/Krav+til+bruk+av+HelseID+for+system+til+system+tilgang+til+APIer
