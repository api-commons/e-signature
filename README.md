# E-Signature

The common e-signature vocabulary -- the envelopes sent for signature, the documents in them, the people who sign, the fields they fill and the templates they start from -- distilled from the APIs that already exist. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged E-Signature, eSignature, Electronic Signature, Digital Signature, Document Signing, E-Sign, Contract Management, CLM in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| envelope | 35 | 30 | id 93%, name 77%, status 73%, created_at 70%, metadata 50% | documents 26, envelopes 5, submissions 4, envelope 4 |
| signer | 16 | 15 | email 80%, id 73%, status 60%, name 53% | recipients 9, signers 5, submitters 1, recipient 1 |
| template | 25 | 22 | id 96%, name 82%, created_at 59% | templates 22, template 6 |
| signature_field | 14 | 12 | type 83%, id 67%, name 67%, required 58%, signer_id 50% | fields 14, tabs 1 |

Cohort: 72 providers with harvested OpenAPI, 35 crosswalks. Of the providers exposing a envelope: 74% create, 80% list, 77% fetch, 43% update, 71% delete. Generated 2026-11-10 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- A signer agrees on email, name, role and status -- the routing information every signing flow needs -- across DocuSign, Dropbox Sign, PandaDoc, Documenso and the rest.
- Signature fields agree on type, name and whether they are required, so a field layout maps between products even where the documents do not.
- The envelope itself agrees only on id, name, status and created_at: what it carries (documents, signers, expiry) is modelled differently by every provider.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- The cohort is the e-signature and contract-management tags only. With Document Management in it, `/documents` brought in database and editor documents.
- The signing transaction is an `envelope` (`/envelopes`), though most products call it a document: `/documents` is the files context's, and envelope means only one thing.
- `participants` and `parties` are signers only beneath an envelope, document, contract or signature request; a call's participants and a chat room's are not.
- Fields are `signature_field`, DocuSign's tabs and PDF form fields included.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
