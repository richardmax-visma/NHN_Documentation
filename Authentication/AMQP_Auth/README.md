# AMQP Authentication (NHN messaging)

Helsenorge messaging (E-kontakt, Helsekontakt AMQP flows) uses AMQP as transport protocol via NHN "Tjenestebuss".
Authentication to the broker is done with mutual TLS (client certificate), not HelseID bearer tokens.

See also: [HelseID Authentication](../HelseID_Auth/) for system-to-system REST/FHIR API access tokens.
See also: [Test Environments](../../Test_Environments/) for environment-specific endpoints and connectivity constraints.

## What you need

- NHN-issued client certificate and private key (Virksomhetssertifikat) registered for Tjenestebuss.
- Trust chain for NHN/CA (Buypass/Commfides) installed so the broker cert is trusted.
- Queue/virtual host permissions from NHN.
- If you use the official SDK: Helsenorge.Messaging (upgrade requirement: ≥ 6.0.3).

## How it works

- Client presents cert/key during TLS handshake to Tjenestebuss (RabbitMQ). Broker authenticates via the client cert subject and applies queue/vhost ACLs.
- HelseID access tokens are used for REST/FHIR APIs; they are not used to authenticate the AMQP connection itself.
- Certs are long-lived (until expiry/rotation); each connection re-handshakes TLS.

## Key endpoints

### Test

- AMQP: `tb.test.nhn.no:5671`
- HelseID token (if you also call REST/FHIR APIs): `https://helseid-sts.test.nhn.no/connect/token`

### Production

- AMQP: `tb.nhn.no:5671` (Helsenett only)
- HelseID token (if you also call REST/FHIR APIs): `https://helseid-sts.nhn.no/connect/token`

## Library upgrade requirement (if using Helsenorge.Messaging)

- Minimum required version: `6.0.3`
- Deadline in test: `1.10.2025`
- Deadline in production: `1.12.2025`

## Sources

- Meldingsutveksling med Helsenorge: https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/pages/690913297/Meldingsutveksling+med+Helsenorge
- Krav til oppdatert versjon av Helsenorge Messaging: https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/pages/2904064001/Krav+til+oppdatert+versjon+av+Helsenorge+Messaging
- Krav til bruk av HelseID for system-til-system tilgang til APIer (for REST/FHIR side): https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/pages/2663776258/Krav+til+bruk+av+HelseID+for+system+til+system+tilgang+til+APIer
