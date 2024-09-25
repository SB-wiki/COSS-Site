---
icon: elementor
---

# Whitepaper on Registry & Credentialing

**Context & Problem Statement**

The 1st generation of registries were purely paper-based lists maintained in registers. As part of early computerisation, such lists got digitized giving birth to the 2nd generation of registries. They were digitized data, but typically maintained in an internal database. With the advent of the Internet and smartphones, as more systems went online, data also migrated to 3rd generation portal-based systems. They partially addressed liveness and reuse. But such portals can only be used by humans by visiting a portal or mobile app, making it non-scalable and costly by not allowing other systems to access data in an automated and trustworthy manner. In-spite of the significant adoption of technology in the recent years, coupled with enhancements in the process of information collection and analysis, the accessibility of datasets has remained constrained due to lack of interoperability. Multiple versions of data sources are used and as data is maintained in legacy systems which are not connected, it leads to duplicates and data full of errors. Furthermore, data governance is not possible without a centralized system for managing master data.

4th generation electronic registries solve the three core issues with a portal based approach by having open APIs through which digitally signed data is made available for read, search, and subsequent usage with the consent of the entities in question.. Open APIs allow automated consented access by external systems, making data use scalable,cost efficient, reliable while also ensuring security & privacy of data in question aligning with a Government’s data privacy policies.. Digitally signed data available via these APIs brings in tamper-resistance, electronic verifiability, and portability of data. These 4th generation electronic registries allow not only storage of data but also support in keeping data up to date via inbuilt mechanisms and offers consented access & verifiability.This Can dramatically reduce the cost of repeated data collection and maintenance of various master data. Examples of registries include geographical data registry, institution registry, school registry, teacher registry, and so on.

**What is a Registry and Digital Verifiable Credentials?**

An electronic registry is a structured & live identification system that gathers, saves, and maintains uniformed updated data or information on an entity, such as a patient, person, employee, student, or facility, and is constantly updated to serve as the entity's "Single Source of Truth'' which is also verifiable. Registries function as a shared digital infrastructure foundational layer for national digital initiatives by facilitating a common source of verifiable data that can be utilized by any Govt or private entity or system with consent for execution of a digital initiative.Such registries enable consented subjects (people, entities, things) to enroll, manage their record with the necessary degrees of verification, and use third-party services that are built on it by using its authentication and KYC services.

Registries are designed keeping certain design principles in mind:

* Minimalism
* Self maintainable
* Secured and consented access
* Verifiable
* Scalable
* Single source of truth.
* Micro-services & API based

The government, educational, industry, and other ecosystems issue certificates (government and non-government issued), licenses, etc. Availability of these in paper form creates issues of low trust, lack of credibility,information asymmetry, time consuming physical verification, and non-portability amongst many others. Additionally, it is difficult to verify the legitimacy of these documents

Verifiable Credentials serve as a robust “instrument of trust” for qualifying a claim made against a specific actor or an event.These are tamper-proof credential, & are independently verifiable (both via online & offline methods) along with supplemental capabilities like multi-lingual extensions & multimodal outputs (i.e. both, paper & digital forms - thus cutting through the digital divide & enhancing the adoption potential for VCs) is that can be verified cryptographically. These are secure, tamper-proof, machine-readable, and easily shareable.

**Terminology**

| **Keyword**  | **Definition**                                                                                                                                                                     |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Actor        | A person, entity, or a thing who/which has been identified                                                                                                                         |
| Attestation  | An act of verifying and authorizing specific data in a digitally signed fashion by an authorized individual/entity (whose identities are typically linked to some other registries |
| Claim        | A statement that is made by an actor which can be verified.                                                                                                                        |
| Credential   | Digitally represented verifiable artifacts containing a qualification, achievement, milestone, fact, etc issued to an actor for them to be able to make claims.                    |
| Consent      | Approval of an actor given to another person/system to access the data of that actor for purposes of the transaction/interaction.                                                  |
| Data         | Electronic data of any type. It could be simple data or composite data.                                                                                                            |
| Database     | A software system that stores and manages data.                                                                                                                                    |
| Entity       | A thing with distinct and independent existence, such as a person, organization, or device that performs one or more roles in the ecosystem.                                       |
| Master Data  | Need Inputs                                                                                                                                                                        |
| Transaction  | Data representing details of an interaction/transaction that was done among one or more actors within a system                                                                     |
| Verification | Need Inputs                                                                                                                                                                        |

**Why Registries and credentialing?**

**Registries**

A fundamental issue with present systems is the dearth of trustworthy and accessible master data.Every digital platform needs to keep master data and actors (persons, entities, or things) data associated to that system for identification, validation, etc. A property tax system, for example, must retain master data on properties, land boundaries, tax codes, tax payers, inspection officers, etc. in a structured and validated manner in order to help in managing the property tax transaction in an efficient manner. Each digital initiative typically maintains its own copy of data, which is challenging to keep updated and prevents data interchange across the programs. Governing bodies have data that is scattered across paperlist, databases & spreadsheets.To combat this issue electronic registries are necessary and provide the foundational layer that manages the key entities and standardized master data required for any transaction in the ecosystem for the enablement of any digital program, running any insurance scheme, Capacity building programs for teachers, non-communicable disease programs etc. The Registry layer forms the base of the services required to manage the master data for all government programs.

All digital platforms require master data and actor (person/entity/thing) data related to that system to be maintained for identification, validation, etc. Although master data is not transactional in nature and does not change often, it does explain transactions.

Having registries in place creates efficiencies, acts as a single source of truth, and provides the metadata needed by other information systems essential for information exchange across data systems. Like Aadhaar is a registry of “Citizens of India”, PAN system is a registry of “persons (people/entity) who are direct taxpayers”, PDS database is a registry of “ Families who receive food subsidy”, and so on. Registries assist in resolving data issues for farms, schools, teachers, and other stakeholders. Data on students, farmers, and teachers can be made available in registries, verified by the appropriate authorities, and then converted into credentials. The appropriate actors have the option to import into their associated Digital Wallets and share these credentials whenever and wherever needed.

Electronic registries with Open APIs for other applications seamlessly validate and use attested and authenticated data. This is even more critical when it comes to people and entities where various claims can be electronically validated against such registries via open APIs avoiding paper-based validations, thus increasing trust while decreasing cost of validation. Registries empower data owners, by giving them the ability to view, initiate correction and control how their information is accessed or used, by giving them the ability to give and withdraw consent at the attribute level (consent-based architecture).

Registries are based on Open Digital Ecosystem approach - The approach of creating shared digital infrastructure so that others can build products and services on top, reflects a radical shift – away from building monolithic, end-to-end solutions – and towards enabling multi-stakeholder collaboration to deliver more user-centric solutions at a larger scale

Registries are often created with the intention of providing restricted or controlled access to an ecosystem. These registries enable the automated and seamless integration of data and information on a large scale.

**Verifiable credentials**

It offers a convenient, secure, and privacy-oriented alternative to current physical and digital identity management systems. A recent example of this is the COVID-19 vaccination certificates. When multiple certificates need to be reviewed quickly, like when boarding a plane or at a football game, it is frequently error-prone and time-consuming to verify paper-based immunization certificates. Additionally, to establish a high level of authenticity Verifiable credentials provide a practical, safe, and privacy-focused alternative to physical forms of identification.

Digital credentials (different certificates in digitally verifiable form) help in automation, reducing time, effort, and cost. The information that a physical credential contains can also be represented by a verifiable credential. Verifiable credentials are more tamper-evident and reliable than physical credentials because of incorporation of technology like digital signatures. By establishing a system of standardized VC documents, one may securely share credentials with anybody, anywhere, expanding their access to opportunities and services. Verifiable Credentials are private, and users can always choose what attributes of their identity they want to disclose. These can be verified everywhere, anytime.

Credentials empowers individuals and organizations to make claims about themselves for the purpose of obtaining services, and the service provider having the ability to validate such claims in a paperless and reliable method

In contrast to traditional verification processes that take ages to complete the traditional verification process, VC may be verified anywhere, at any time, in a matter of seconds.These are portable as holders can store Verifiable Credentials in their digital wallet and take them anywhere while still being verifiable. VC builds trust, reputation, reliability, prevents various frauds and eases out certain processes like settlement of insurance claims,background verification of candidates etc.

Registries & Credentialing as a concept is based on the key principle of **“Single source of Truth”**, and there can be multiple use cases that can be explored which can add value in driving expected outcomes.

**Representative sample use-cases for R & C**

Registries include both personal and community information/ records, that provide a ‘single source of truth’ e.g., financial data, identification data, civil registries, land registries, and Exchanges which facilitate the flow of data being generated by governments, businesses and individuals. Below are a few of the use cases of registries:

**Farmer/Farm Registry:** The Farmer Registry can be built for consolidating the farmer's information. Demographic details of the farmers can be captured along with the Geo- coding. The information of the farmers available in the registry can further be used for things like farmer welfare, farm management, Weather based alert to farmers, Accurate quantification of the farmer crop and yield and for measuring the crop changing pattern in the area and digital information about socio-economic landscape of farmers across India. Moreover, farmer registry can be integrated with certain existing schemes for farmers namely Pradhan Mantri Kisan Samman Nidhi (PMKISAN), Soil Health Card (SHC) and Pradhan Mantri Fasal Bima Yojna (PMFBY)

**Hospital/Facility Registry:** The Hospital or Facility Registry can be built and is essential to enable nationwide health information exchange. Registered Facilities can be allocated a unique identifier for identification of the health facility. A hospital efficiently foresees unmet needs so that a proactive risk mitigation strategy can be created in advance to tackle a pandemic. It can indicate crucial areas for improvement by building new or renovating current medical facilities while considering factors like population density, geography etc.

**Education Registry:** Governments need access to a database of key users, entities, and beneficiaries to develop various policies and schemes. To keep data regarding educational institutions, academic staff, students, administrators, subjects, textbooks, etc., registries are required. At any stage in the ecosystem, it is critical to standardize how schools, teachers, and students are identified. Allocating unique IDs to schools, teachers, and students will make sure that the educational records made for a student can be given to the right person, be within the authority of the student or parent, and be shared or used with consent.The "Sunbird RC educational registry" is a reference solution for creating registers for educational boards, institutions, teachers, and students. It can be used to create registries of all actors in the ecosystem and can also be used to issue verifiable credentials, digital badges, and upskilling.

**National Identity System:** National ID system can serve as the foundation for safe identity verification for users in the public and private sectors by compiling a registry of distinct, verified identities.ID systems can also offer credentials that enable users to authenticate their identities for a range of purposes and industries, in addition to creating an authoritative source of identity information that other systems can use.

**Digital Transcript**:The possibility of issuing fraudulent diplomas and certificates can be eliminated by the issuance of digital transcripts since these registries enable the real-time verification of the credentials of the relevant institution, thus ensuring the entity's legitimacy.

**Healthcare Actor Credentialing:**To ensure the safety of patients and quality of care, it is an essential requirement to ensure reliability of a healthcare actor irrespective of their type (Health professionals, facilities, medical equipment, pharma licenses etc).To ensure safe healthcare delivery to a patient who is a key stakeholder in all healthcare transactions and whose wellbeing can be at stake if the licenses are tempered or faked for healthcare frauds and service delivery, healthcare stakeholder credentialing has been emerging as a critical use case. It is also a critical use case that can streamline payer-provider contracting to avoid fraudulent claims and practices by a healthcare facility using a fake payer contract**.**

**Healthcare Transaction Credentialing:** It has the capability that can not only record and monitor healthcare & service delivery events but also ensure that the desired outcome is achieved. Vaccination credentialing amidst COVID has proven this concept way far beyond imagination where a person’s vaccine credentials can ensure reduced infection level amidst a communicable disease outbreak. Vaccination was just the beginning of event credentialing but there are multiple untapped and unrealized use cases where credentialing can help program manager, Governments and donors to ensure effective program operationalization & execution, Measuring the coverage of programs and ensure event-based justification for effective public health fund management**.** Some of the examples of event/transaction credentialing that can be explored in healthcare includes**:**

* Issuance of QR code-based health ID or program cards
* Digital Certificate Issuance for Immunization Program
* Health worker badge issuance – To enable real time monitoring of health workers

**What is Sunbird RC (Registry & Credentials) and what does it solve?**

An open-source software to rapidly build and deploy next generation electronic registries and verifiable credentials including attestation and verification flows. Sunbird RC can be used to create numerous national registries of individuals, objects, and entries for a variety of domains. Adopters can rapidly build core electronic registries through configurable schemas and workflows. All needed APIs, workflows, and a default user experience are automatically created for key registry stakeholders. Sunbird RC provides microservices to issue portable standard schema based W3C VC complaint credentials with attestation and verification flows. These credentials may be printed with QR codes, can be translated into many languages, and are instantly verifiable. **Sunbird RC**, facilitates enrollment, authentication, data ownership, search, issuance and management of verifiable credentials, claim attestation flows between user and attester, sharing of credentials with [DEPA compliant](https://www.niti.gov.in/sites/default/files/2020-09/DEPA-Book.pdf) user consent, amongst others.

Sunbird RC is listed as a global Digital Public Good (DPG) within the Digital Public Good Alliance registry. It is currently used as part of DIVOC, a globally recognized digital good for vaccination and health credentialing. It is also used as part of DIKSHA, school education platform used at population scale.

[Sunbird RC](https://sunbird.org/projects/sunbirdrc) offers a credible solution with the following key features:

· Open APIs and Universal access

· Secured and Consented access

· Minimalism and Decentralized

· Non repudiable

**Implemented Use cases for Sunbird RC**

**DIKSHA:** [DIKSHA](https://diksha.gov.in/) (Digital Infrastructure for Knowledge Sharing) is a national platform for school education, an initiative of National Council for Educational Research and Training (NCERT), under the aegis of the Ministry of Education (MoE). DIKSHA is built on open source technology, which incorporates internet scale technologies and enables several use-cases and solutions for teaching and learning. DIKSHA is built using MIT licensed open source technology called Sunbird, which is a digital infrastructure for learning and solutions and offers over a 100 micro-services as building blocks for the development of platforms and solutions.The DIKSHA platform has enabled the capability to issue digital credentials to the user on completion of a course or a quiz. The user can share digital credentials with anyone and are digitally verifiable. This is being used extensively for teacher training across states, and for credentialing course completion of COVID warriors on iGOT.

![](<../../../.gitbook/assets/0 (3).png>)

**DIVOC:** The Digital Infrastructure for Vaccination Open Credentialing ([DIVOC](https://divoc.egov.org.in/)) solution to support countries with their vaccination effort. DIVOC builds on top of Sunbird RC to digitize the generation of a vaccination certificate available both in electronic form and printable copy downloaded from the central vaccination database.Verifiable credentialing is the core module of DIVOC. Certificates are natively digital, machine-readable, digitally signed, verifiable, and also printable with a secure and tamper-proof QR code. This makes it easy for people to carry/store it electronically or physically. Templates/formats of the certificates can be configured based on your need.DIVOC can also be explored for creating the registries for facilities and healthcare professionals

Similar to this, many more use cases can be explored, such as the blood donor registry, the automobile registry, and the employee registry and Verifiable Credentials can be used in multiple domains like providing digital transcripts to students, Prescribing medications to the patients, banking services like money transfer etc. It has been implemented in 5 countries over 2 Bn+ COVID-Certificates issued till date

[https://docs.sunbirdrc.dev/example-use-cases/edu-registries](https://docs.sunbirdrc.dev/example-use-cases/edu-registries)
