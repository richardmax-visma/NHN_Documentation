# Classes

FHIR resource snippets for Medlemstjenester (health offerings and member lists).

- [HealthcareService.mmd](HealthcareService.mmd) – Offered service

```mermaid
classDiagram
class HealthcareService {
	+string identifier
	+bool active
	+string name
	+string comment
	+Reference providedBy
	+Reference location
	+Endpoint endpoint
}

```

- [Organization.mmd](Organization.mmd) – Providing organization

```mermaid
classDiagram
class Organization {
	+string identifier
	+string name
	+Endpoint endpoint
}

```

- [Location.mmd](Location.mmd) – Service location

```mermaid
classDiagram
class Location {
	+Address address
	+Telecom[] telecom
}

```

- [Endpoint.mmd](Endpoint.mmd) – Communication endpoint

```mermaid
classDiagram
class Endpoint {
	+string identifier
	+string id
}

```

- [Address.mmd](Address.mmd) – Postal address

```mermaid
classDiagram
class Address {
	+string line
	+string city
	+string postalCode
}

```

- [Telecom.mmd](Telecom.mmd) – Contact points

```mermaid
classDiagram
class Telecom {
	+string system
	+string value
}

```

- [Patient.mmd](Patient.mmd) – Member record

```mermaid
classDiagram
class Patient {
	+string identifier
	+Contact contact
}

```

- [Contact.mmd](Contact.mmd) – Member contact linkage

```mermaid
classDiagram
class Contact {
	+Reference organization
	+Period period
}

```

- [Period.mmd](Period.mmd) – Service period

```mermaid
classDiagram
class Period {
	+date start
	+date end
}

```
