# Baseline Profile Proposal
This document defines a profile for OpenID for Verifiable Credentials protocol family in combination with the credential format SD-JWT VC DM. The aim of the Baseline Profile is to specify a minimalistic feature set of the the OID4VP protocol family to enable interoperability among issuers, wallets, and verifiers. The Baseline Profile also acts as a minimum viable interoperability specification for the OID4VC protocol family. 

The profiled specification includes [OID4VCI](https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0.html), [OID4VP](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html), and [SD-JWT VC DM](https://github.com/danielfett/sd-jwt-vc-dm).
## Introduction
This document defines a minimalistic set of requirements for the existing specifications to enable interoperability among issuers, wallets, and verifiers. This specification acts as a simple implementation of the [OID4VCI](https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0.html) and [OID4VP](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html) specifications, therefore, as an entry to the OID4VC protocol family for implementors due to its minimalistic set of features.

todo: mention that this profile aims for a lower level of assurance than HAIP

The Baseline Protocol aims for a lower level assurance than [HAIP](https://openid.github.io/oid4vc-haip-sd-jwt-vc/openid4vc-high-assurance-interoperability-profile-sd-jwt-vc-wg-draft.html).
## Terminology TBD

## Scope
The following aspects are in scope of this interoperability profile:
- Protocol for Issuance of Verifiable Credentials (OID4VCI)
- Protocol for online presentation of Veifiable Credentials (OID4VP)
- Credential format (SD-JWT VC DM))
- A revocation mechanism
- Cryptographic holder binding
- Issuer key resolution
- Cryptographic suite
### Out of Scope TBD

### Scenarios TBD

## Credential Format
- The credential format must be [SD-JWT VC DM](https://github.com/danielfett/sd-jwt-vc-dm)

## Key Bindings
- Key binding: cnf, with jwk or kid (with did:jwk) 
- Issuer keys: did:web or jwt-issuer 
- Issuers decide between key methods and key binding options
- Wallets and RPs MUST support both key methods and binding options
- Issuers, holders and RP MUST support P-256 (secp256r1) as a key type with ES256 JWT algorithm for signing and signature validation ([OID4VC HAIP 8.](https://openid.github.io/oid4vc-haip-sd-jwt-vc/openid4vc-high-assurance-interoperability-profile-sd-jwt-vc-wg-draft.html#name-openid-for-verifiable-prese))
- Compact serialization must be supported as defined in [[I-D.ietf-oauth-selective-disclosure-jwt](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-selective-disclosure-jwt-08)].

## Revocation
- Revocation is handled via a JWT status list with 1 bit status. ([Token Status List](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-status-list-02))

## OpenID for Verifiable Credential Issuance (TBD)


## OpenID for Verifiable Presentations
### Device Flows
Both same device and cross device flows MUST be supported.
### Authorization Request
- As a way to invoke the Wallet, the custom URL scheme `openid-baseline://` MUST be used.
- The authorization request MUST contain `request_uri` parameter. 
- `response_type` MUST be `vp_token`. ([OID4VP 5.4](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html#name-response-type-vp_token))
- `response_mode` MUST be `direct_post`. ([OID4VP 6.2](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html#name-response-mode-direct_post))
- For same device flow, the Request Object resolved in `request_uri` MUST contain `redirect_uri`. ([OID4VP 6.2](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html#name-response-mode-direct_post))
- Request Object resolved from `request_uri` MUST contain a `presentation_definition`.
- The Client Identifier Scheme MUST be `x509_san_dns`. ([OID4VP 5.7](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html#section-5.7))
- `state` and `nonce` MUST be present ([OID4VP 6.2](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html#section-6.2))
### Presentation Definition
- The  `presentation_definition` must contain the following JSON parameters: ([OID4VP 5.1](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html#name-presentation_definition-par))
   ```
   id
   input_descriptors.id
   input_descriptors.constraints
   input_descriptors.formats
   input_descriptors.name - optional
   input_descriptors.purpose - optional
   formats
   ```
Formats MUST be vc+sd-jwt

### Error Response
Error response is not a part of profile but SHOULD be there for every profile according the ([OID4VP 6.4](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html#section-6.4))

