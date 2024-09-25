---
icon: elementor
---

# Nouns and verbs in registries

### Nouns in Registries-VC-VP <a href="#e2fj4pl534d3" id="e2fj4pl534d3"></a>

Adapted and annotated version of [https://www.w3.org/TR/vc-use-cases/#terminology](https://www.w3.org/TR/vc-use-cases/#terminology)

1. **Issuer**
   1. _W3C definition:_ A role an[ entity](https://www.w3.org/TR/vc-use-cases/#dfn-entities) can perform by asserting[ claims](https://www.w3.org/TR/vc-use-cases/#dfn-claims) about one or more[ subjects](https://www.w3.org/TR/vc-use-cases/#dfn-subjects), creating a[ verifiable credential](https://www.w3.org/TR/vc-use-cases/#dfn-verifiable-credentials) from these[ claims](https://www.w3.org/TR/vc-use-cases/#dfn-claims), and transmitting the[ verifiable credential](https://www.w3.org/TR/vc-use-cases/#dfn-verifiable-credentials) to a[ holder](https://www.w3.org/TR/vc-use-cases/#dfn-holders).
   2. Issuer always issues verifiable credentials, holder issues verifiable presentations.
2. **Verifier**
   1. _W3C definition:_ The[ entity](https://www.w3.org/TR/vc-use-cases/#dfn-entities) verifying a[ claim](https://www.w3.org/TR/vc-use-cases/#dfn-claims) about a given[ subject](https://www.w3.org/TR/vc-use-cases/#dfn-subjects).
3. **Subject**
   1. The[ entity](https://www.w3.org/TR/vc-use-cases/#dfn-entities) about whom a[ claim](https://www.w3.org/TR/vc-use-cases/#dfn-claims) is issued.
4. **Holder**
   1. _W3C definition:_ A role an[ entity](https://www.w3.org/TR/vc-use-cases/#dfn-entities) may perform by possessing one or more[ verifiable credentials](https://www.w3.org/TR/vc-use-cases/#dfn-verifiable-credentials).
   2. A[ holder](https://www.w3.org/TR/vc-use-cases/#dfn-holders) is usually, but not always, the[ subject](https://www.w3.org/TR/vc-use-cases/#dfn-subjects) of the[ verifiable credentials](https://www.w3.org/TR/vc-use-cases/#dfn-verifiable-credentials) that they are holding.[ Holders](https://www.w3.org/TR/vc-use-cases/#dfn-holders) store their[ credentials](https://www.w3.org/TR/vc-use-cases/#dfn-credential) in[ credential repositories](https://www.w3.org/TR/vc-use-cases/#dfn-credential-repository).
   3. The holder may or may not be the subject of the credential e.g. declaration by forest official that land parcel #23A is environmentally cleared.
5. ~~Self declared data~~
   1. ~~Self declared information by holder or issuer.~~
   2. ~~This may be part of a verifiable presentation issued by the holder.~~
6. **Claim**
   1. A claim is any assertion about an attribute e.g. date of birth, address, related to the holder or subject
   2. A claim is part of a verifiable credential issued by an issuer
7. **Verifiable credential** (VCs)
   1. A Verifiable Credential is a tamper-evident data file with a set of claims about a person, organization, or thing that can be cryptographically verified.
8. **Templated presentation** (for retrieval and display)
   1. _W3C definition of ‘Presentation’:_ Data derived from one or more[ verifiable credentials](https://www.w3.org/TR/vc-use-cases/#dfn-verifiable-credentials), issued by one or more[ issuers](https://www.w3.org/TR/vc-use-cases/#dfn-issuers), that is shared with a specific[ verifier](https://www.w3.org/TR/vc-use-cases/#dfn-verifier).
   2. Verifiable presentation is a data exchange model built on top of the VC, whereas a templated presentation is like a UI attached to the VC data.
   3. The vaccine certificate issued by NHA is a verifiable credential. After that moment, when the holder shares the vaccination details with any other verifiers, either fully or partially is a verifiable presentation. A presentation of the verifiable credential, as a PDF or an on-screen display, is only a templated presentation. A templated presentation usually have an interaction mechanism attached to it like a QR code.
   4. The verifiable presentation comes into play when the holder shares data with another party.
9. **Verifiable presentation** (VPs)
   1. _W3C definition of verifiable presentation::_ A verifiable presentation is a tamper-evident presentation encoded in such a way that authorship of the data can be trusted after a process of cryptographic verification. Certain types of verifiable presentations might contain data that is synthesized from, but do not contain, the original[ verifiable credentials](https://www.w3.org/TR/vc-use-cases/#dfn-verifiable-credentials) (for example, zero-knowledge proofs).
   2. VP is always issued by the holder of a credential.
   3. Every verifiable presentation is a self attested proof based on a VC
   4. VC is the interaction between the issuer and the holder, whereas VP is between a verifier and the holder. A valid VP originates from a VC.
   5. Self declaration in the form of a verifiable presentation collating a number of other credentials could exist eg. "I am a male of 18+ years from Nashik" <-- attributes here can be backed up by a collection of claims.
10. **Repository**
    1. _W3C definition:_ A program, such as a storage vault or personal[ verifiable credential](https://www.w3.org/TR/vc-use-cases/#dfn-verifiable-credentials) wallet, that stores and protects access to[ holders'](https://www.w3.org/TR/vc-use-cases/#dfn-holders)[ verifiable credentials](https://www.w3.org/TR/vc-use-cases/#dfn-verifiable-credentials).
    2. Repositories are typically of two types -
       1. **Registry**
          * Collection of credentials of multiple holders from a single issuer in one place
          * Could also store schemas that define the credentials, templates that define the presentation, et al.
       2. **Wallet** (personal repository)
          * A wallet is a collection of credentials e.g. license, Aadhar, PAN, vaccine certificate, boarding pass, transcript, etc for a single user (or a team) stored in a wallet owned by the user, e.g. Digilocker, Google Wallet, Apple Wallet
          * A wallet can be -
            1. a store, perhaps a secure cloud storage which is accessed through identification and authentication e.g. Digilocker
            2. As a software (or, optionally a hardware) component which is used to manage private keys, cryptographic secrets and material which are addressed to the designated owner/controller of the component. E.g. [https://tor.us/](https://tor.us/)
11. **Verification**
    1. _W3C definition_: The evaluation of whether a[ verifiable credential](https://www.w3.org/TR/vc-use-cases/#dfn-verifiable-credentials) or[ verifiable presentation](https://www.w3.org/TR/vc-use-cases/#dfn-verifiable-presentations) is an authentic and timely statement of the issuer or presenter, respectively. This includes checking that: the credential (or presentation) conforms to the specification; the proof method is satisfied; and, if present, the status is successfully checked.

Conditionality?

![](<../../../.gitbook/assets/0 (1) (1) (1).png>)

[https://learn.microsoft.com/en-us/azure/active-directory/verifiable-credentials/how-to-use-quickstart-selfissued](https://learn.microsoft.com/en-us/azure/active-directory/verifiable-credentials/how-to-use-quickstart-selfissued)

The employment credential seems to be a ‘if you do X, you can get the credential’. Is this part of W3C?
