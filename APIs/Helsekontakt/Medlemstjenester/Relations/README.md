# Relations

Mermaid diagrams of resource relationships for Medlemstjenester.

- [HealthcareServiceRelations.mmd](HealthcareServiceRelations.mmd) – Offered services and endpoints

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

class Organization {
	+string identifier
	+string name
	+Endpoint endpoint
}

class Location {
	+Address address
	+Telecom[] telecom
}

class Endpoint {
	+string identifier
	+string id
}

class Address {
	+string line
	+string city
	+string postalCode
}

class Telecom {
	+string system
	+string value
}

HealthcareService --> Organization : providedBy
HealthcareService --> Location : location
HealthcareService --> Endpoint : endpoint
Organization --> Endpoint : endpoint
Location --> Address : address
Location --> Telecom : telecom

```

- [PatientRelations.mmd](PatientRelations.mmd) – Member-to-organization linkage

```mermaid
classDiagram

class Patient {
	+string identifier
	+Contact contact
}

class Contact {
	+Reference organization
	+Period period
}

class Period {
	+date start
	+date end
}

Patient --> Contact : contact
Contact --> Period : period

```
