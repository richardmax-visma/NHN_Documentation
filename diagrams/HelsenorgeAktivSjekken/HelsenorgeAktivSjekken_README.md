# HelsenorgeAktivSjekken API

Checks if citizens are digitally active on Helsenorge (Norwegian health portal).

## Request

| Field      | Type     | Required | Description                                                      |
| ---------- | -------- | -------- | ---------------------------------------------------------------- |
| `fnrListe` | string[] | ✅       | **Fødselsnummer Liste** - List of national ID numbers (max 1000) |
| `omraade`  | int      | ✅       | **Område** - Context area for the check                          |

## Omraade Enum (Area)

| Value | Name       | Norwegian  | English                             |
| ----- | ---------- | ---------- | ----------------------------------- |
| `3`   | HELSEHJELP | Helsehjelp | Healthcare                          |
| `6`   | UNGDOM     | Ungdom     | Youth (13+, school health services) |

## Response

| Field          | Type                       | Description                 |
| -------------- | -------------------------- | --------------------------- |
| `erAktivListe` | Map<string, ErAktivStatus> | Map of national ID → status |

## ErAktivStatus

| Field             | Type | Norwegian          | English                                               |
| ----------------- | ---- | ------------------ | ----------------------------------------------------- |
| `erAktivSelv`     | bool | Er aktiv selv      | Is active themselves (can be reached directly)        |
| `erAktivViaAndre` | bool | Er aktiv via andre | Is active via others (has a representative)           |
| `tildeltFullmakt` | bool | Tildelt fullmakt   | Assigned power of attorney (not competent to consent) |

## Notes

- Children under 16 cannot be `erAktivSelv` (must go through parents)
- `erAktivViaAndre` = parent representation OR power of attorney
- `tildeltFullmakt` = person cannot consent themselves (e.g., dementia)

## Sources

- HelsenorgeAktiv documentation: https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/pages/1810268162/HelsenorgeAktiv
- HelsenorgeAktivSjekken: https://helsenorge.atlassian.net/wiki/spaces/HELSENORGE/pages/2043478017/HelsenorgeAktivSjekken
- Swagger: https://eksternapi.hn.test.nhn.no/digitaltaktiv/swagger/index.html
