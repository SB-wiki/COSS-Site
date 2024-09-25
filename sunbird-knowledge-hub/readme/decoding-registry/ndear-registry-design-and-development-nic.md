---
icon: elementor
---

# NDEAR Registry Design & Development - NIC

### National Informatics Centre <a href="#id-999cwujf1qyu" id="id-999cwujf1qyu"></a>

### **NDEAR Registry Design & Development** <a href="#pmzdo4x0gbth" id="pmzdo4x0gbth"></a>

### Summary: <a href="#gxj645wq9ty9" id="gxj645wq9ty9"></a>

NDEAR, launched by the Honorable Prime Minister of India on 29th July 2021, is a technological framework that aims to enable existing systems to upgrade and become interoperable, while making available the building blocks for the creation of new tools and solutions. Para 3.3 of NEP 2020 requires achievement of universal participation in school by carefully tracking students, as well as their learning levels which necessitates uniquely identifying each actor / entity (institute/teacher / student) in the education ecosystem.

The subsequent section of this note indicates how NDEAR recommends a registry infrastructure (core building block) that acts as Single Source of Truth and/or System-of-Record (SoR) and is offered as hosted services/application at appropriate administrative levels. Registry enables consenting actors to enroll and avail various services built on and around it, and is aimed at enabling multiple use cases such as visibility to progress to take targeted actions, school transfers, college admissions, scholarship disbursement, easy access to education, health records, etc.

The design principles for building registry are also referenced, that will drive data accuracy and build trust in the system among the actors of the ecosystem. There are details of the work that has already been undertaken by the NIC in this regard - the Education Institute Registry. This note concludes by providing recommendations and the high-level approach for building a registry in a federated fashion as envisioned by the NIC, with the goal of enabling various use cases in the education ecosystem.

Contents

### &#x20;<a href="#txza50h1jwx1" id="txza50h1jwx1"></a>

* Overview
* Key Registry Principles
* Institute, Learner & Teacher Registry - policy purview
* The Road to Registries
* Institute, Learner & Teacher - Registry Use Cases
* NIC - Education Institute Registry POC
* Implementing Federated NDEAR Registries to enable benefits
* Policy Upgrades recommended
* Open Questions
* FAQs

Appendix

Draft approach for leveraging Aadhaar for Student Registry

### &#x20;<a href="#osn8mk8om8dp" id="osn8mk8om8dp"></a>

### &#x20;<a href="#robzblpqi2ax" id="robzblpqi2ax"></a>

### Overview: <a href="#wx1uug12w8y9" id="wx1uug12w8y9"></a>

India has been successful in leveraging technology across diverse sectors, particularly with developing digital infrastructure. The Union Budget 2021-22 laid emphasis on strengthening India’s digital infrastructure for education and announced the setting up of a National Digital Educational Architecture (NDEAR) to support teaching and learning/skilling and also educational planning, governance administrative activities of the Centre and the States & Union Territories.

In line with the policy direction of NEP 2020, the NDEAR blueprint was launched by the Honorable Prime Minister of India on 29th July 2021 with a vision to create a “Unifying national digital infrastructure to energize and catalyze the education & skilling ecosystem”. In his address, he highlighted the importance of NDEAR in education and skilling, and compared it with the revolution UPI brought about in financial transactions in the country. He stated, “NDEAR is an enabler of NEP-2020 and will act as a ‘super connector’ between various academic and skilling activities in the same way as the UPI interface revolutionized the banking sector.”

The Government of India and the Education ministry have recognized the importance of digitization and adoption of technology in education for inclusive development as reflected in NEP 2020. A critical initiative in this regard is to empower the learners and the teachers of the country with a record system that gives them a single unified view of their lifelong journey as a learner/ teacher. This will be driven by creation of a benefit-led lifelong (KG to PG & skilling) registry system with a unified view for students, teachers and institutions across the country. Subsequent sections in this document detail the use cases that have been envisioned, and the benefits they will provide for the end users.

As the frontrunner in this effort, the National Informatics Centre has already carried out work in this regard, working in consultation with concerned stakeholders (MeiTY - NIC, DIC, UIDAI, MSDE, MoHFW - NHA, MoE - DoSEL, DoHE,NETF, MoWCD etc.), to formulate key design principles for the Registries, and to explore various options to initiate the learner and teacher registry for the nation. The NIC has also designed and implemented [https://institutes.ndear.gov.in/#/home](https://institutes.ndear.gov.in/#/home) , a master Registry construct for all educational institutions in the country - in keeping with the principles of federation and interoperability as laid down by [NDEAR](https://www.ndear.gov.in/index.html) and the [InDEA 2.0](https://www.meity.gov.in/writereaddata/files/InDEA%202\_0%20Report%20Draft%20V6%2024%20Jan%2022\_Rev.pdf) framework. This document further discusses the approach adopted by NIC, the principles applicable for Registries (as specified by NDEAR as well as InDEA 2.0), and the details of the work carried out by NIC so far. Based on these learnings, there are also recommendations from the NIC in terms of the approach that can be followed, in order to enable the envisioned Registry use cases and create significant value for the digital ecosystem of the country.

### Key Registry Principles <a href="#u4ybvsdkxfwa" id="u4ybvsdkxfwa"></a>

1. **Purpose driven, Federated design**: Creation of a “federated set of registries”, each of which is meant for a “specific purpose” rather than a universal, all inclusive registry. Such registries may get interlinked via registry IDs depending on the policies that allow such linking. Interlinked registries may be required to provide an unified view of benefits delivery.
2. **Digital identifier as key to Registry, with usage of familiar, existing IDs for end users**: All registries should have a digital identifier to uniquely identify a record. When registering, end users must be given an option to link their records to existing and familiar digital IDs (such as Aadhaar, mobile, GSTN etc.). This will ensure users only have to remember a minimal set of key/ familiar Digital IDs, and can use the same ones to access their record across multiple Registry systems. so that they are not burdened with
3. **Purpose driven Uniqueness**: Actions such as de-duplication of a record within a Registry may be considered only when the use case for the Registry demands it. Existing systems such as Aadhaar have already carried out such an exercise for the populace of the nation, and must be leveraged when necessary, to carry out such checks, instead of attempting to repeat the entire exercise again within each system.
4. **Trustability of data**: Registries should support user led self declaration of data as well as attestation of data as a means to ensure non-repudiation of credentials and facts as an embedded feature using user authentication and digital signatures. Credentials should, by design, ensure verifiability, portability, permanence and inclusivity, while incorporating consent based and self describing properties.
5. **Empowerment**: Empowering data owners by giving them the ability to view, initiate correction and control their information, and how their information is accessed and used, by giving them the ability to give and withdraw consent at the attribute level (consent-based architecture). Credentials (various certificates in digitally verifiable form) enable people and entities to make claims about them (e.g., claims about academic degree or work experience) for availing services and the service provider having the ability to verify those claims in a paperless and trusted manner.
6. **Security**: Ensuring that data is exchanged in a secured manner with well defined privacy rules and in alignment with access allowed by data owner and issuer
7. **Universal Access and Interoperability**: Enable secure digital access and interoperable communication across systems using secure APIs to ensure seamless integration across diverse systems - allowing them to communicate in a trusted fashion.
8. **Use case centric design**: Registry design needs to be user-centric, rooted in use cases that will ensure active usage of the Registry. Likewise, registry adoption must be driven via use cases that deliver concrete value to the end user, and incentivise them to take consented control of their data.
9. **Minimal data models**: The unified data model for the Registry must be minimal, and evolved based on the needs for which the Registry is being built - it should be kept to a minimum so as to enable envisioned use-cases, and not be allowed to grow unchecked.

### Institute, Learner & Teacher Registry - Policy Purview <a href="#id-6obmimxzg1op" id="id-6obmimxzg1op"></a>

The following are the key non-negotiable policy elements to be adhered to, by any entity considering creation, implementation, hosting as well as usage of Registries. These are quoted from the [NDEAR](https://www.ndear.gov.in/policies-and-standards.html) report as well as the [InDEA 2.0](https://www.meity.gov.in/writereaddata/files/InDEA%202\_0%20Report%20Draft%20V6%2024%20Jan%2022\_Rev.pdf) policy framework laid out by MeITY, and make for critical consideration - as the entities hosting, managing and processing the data in the Registry will be held accountable for data protection obligations and relevant compliance requirements as stated by applicable laws.

* Institute Registries may be hosted centrally, but will have to be attested in a decentralized fashion.
* _School ID shall be generated as part of the national registry but the control of data and attributes will be decentralized to State or district or school levels, as appropriate._

NDEAR Main Report, 2.4.1 - Federated Architecture Principles, Page 50

* Teacher and Learner registries must be deployed in a federated fashion.
* _Student and teacher registries will be held at the school level, school management level and state level, as appropriate. Student and teacher registries will not be held at the national level. Non-PII metadata can be stored at the national level for analytics and open data purposes._

NDEAR Main Report, 2.4.1 - Federated Architecture Principles, Page 50

* Data sharing can be carried out only with user consent based on DEPA and complying to data protection bill (2022)
* _Granular consent shall be required for data sharing, following the principle of purpose limitation. Parental consent shall be adopted for minors. Access to any personal data (data containing PII) enabled through NDEAR services will only be possible via electronic consents._

NDEAR Main Report, 2.4.1 - Federated Architecture Principles, Page 50

* Compliance with data protection and privacy laws as applicable is mandatory.
* _The data fiduciary managing the data and the data processor holding and processing the same shall be responsible for the data protection obligations and compliances under the applicable laws._

NDEAR Main Report, 2.4.1 - Federated Architecture Principles, Page 50

* Reuse of existing systems and simplification of usage for end users via existing and familiar national digital IDs
* _Linking of electronic Registries and re use of Registries to eliminate repeated verification processed, and not cause inconvenience to citizens_

InDEA 2.0, 4.2.5 - Federated Registries, page 33

* Employ existing and familiar digital IDs (national IDs) for onboarding users onto, as well as usage of Registries.
  * _While domain specific platforms are popular, it is important to leverage the JAM identities as the universal IDs that are already used by almost everyone in India. It is thus recommended that other Government systems trying to create a “state controlled'' unique ID are encouraged to achieve it through Aadhaar authentication and eKYC. But, if that system is creating a “user controlled” ID, then, typically the user is allowed to use mobile number/email etc as a means to sign in._

InDEA 2.0, 4.2.2, PDF page 41, doc page 31

* _A Digital ID by itself does not independently exist nor has any stand-alone benefit unless accompanied by appropriate trust levels and used by other systems using authentication and consented profile sharing (KYC) service._
* _A digital identifier, therefore, is the ‘key’ to a registry where the subject (ID holder) is present who, in turn, is empowered to control her ID, manage the registry record (her profile in that registry), choose to use it for availing other 3rd party services through authentication and consented eKYC (digitally signed profile sharing)._
* _In every registry it is necessary that the subjects in that registry are “identified” in a unique and trusted fashion. These identifiers may be purely numeric (e.g. Aadhaar number, mobile number, health ID within ABDM, etc.) or alpha-numeric (e.g. PAN number, Vehicle number, email address, UPI Address, etc.) with or without any logic attached in generating the identifier itself (random vs logic based identifier)._
* _Depending on the policy, uniqueness can be either “user controlled” (user may have more than one ID within the same registry, say, using two different mobile numbers) or “state controlled” (by linking the ID to a globally unique ID like Aadhaar, and hence making sure a user has one and only one entry within the registry)._
* _Custodians of such registries should ensure appropriate policy is applied to either allow user controlled uniqueness or state controlled uniqueness. In addition, the fields in the record of that subject are to be verified/attested or marked as self-declared. When registering, people must be given an option to use their existing digital IDs such as Aadhaar, mobile, etc as appropriately to fit the purpose of that registry and also allow people to control, update, manage their record using the common IDs such as Aadhaar, mobile, etc._”

Section 4.2.4, PDF page 41/42, doc page 31/32

The following are the overall guidelines and recommendations from the [InDEA 2.0](https://www.meity.gov.in/writereaddata/files/InDEA%202\_0%20Report%20Draft%20V6%2024%20Jan%2022\_Rev.pdf) framework on building Registries at scale for delivering value:

_1. Under the federated architecture approach of InDEA 2.0, it is important to create a “federated set of registries”, each of which is meant for a “specific purpose” rather than a universal, all inclusive registry._

_a. Given the federated nature of service delivery and Government systems, it is essential that each registry be maintained in an autonomous way with its own workflows, purposes, rules of participation, etc._\
_b. Any registry provider/custodian must design the registry with the subject (person) in the centre and ensure convenience, inclusion, data empowerment, and meaningful choice for them to control and manage their own record within the registry._\
_c. All registry providers/custodians must ensure personal data protection and consented access fully and ensure appropriate security and privacy measures to protect the data within the registry._

_2. All such registries should have their own “digital ID” internally to uniquely identify a record. a. These internal IDs should ideally be “user managed” (like a “user ID”) making it easier for them to remember and reuse. b. If not, a random number may be used with an option to attach a user ID._

_3. Handling uniqueness:_

_a. When global state-controlled uniqueness is necessary, allow users to link their Aadhaar or other Aadhaar linked or Aadhaar derived or Aadhaar based digital IDs to achieve it._

_b. If not (if it is user-controlled uniqueness), then allow common identifiers such as mobile numbers or other acceptable Digital IDs to be used and still allow users to voluntarily use their Aadhaar._

_c. This allows minimizing the need to remember and use many IDs by the citizens and provides convenience of managing their account using either Aadhaar or mobile or other acceptable digital IDs._

_4. Authentication, eKYC, and SSO:_

_a. All registries should be built as a “building block” to be “reused” as “sources of truth” in a paperless and trusted manner for the sake of simplifying citizen service delivery process and reducing costs_

_b. All registries should offer authentication/Single-Sign-On along with eKYC (consented digitally signed profile sharing) capabilities using the primary ID of that registry_

_c. The SSO should cater to cross-domain and should facilitate identity management among multiple SSO providers. SSO mechanisms should be resilient enough to handle multiple points of failure. Also, it should identify and address security breaches in SSO in a proactive and reactive manner systematically._

_d. All registries should accept and allow citizens to enroll and sign-in with other available digital IDs (white listed as per their policies) to provide 1-click enrolment and sign-in for citizens._

_e. Items b & c above ensure that the registries are not siloed and stand-alone systems, but a true digital building block for other systems, providing citizen convenience and eliminating repeated data capture and verification complying with appropriate policies/laws._

\
Section 4.3, PDF page 43/44, doc page 33/34

### The Road to Registries: <a href="#a5sv47rhounw" id="a5sv47rhounw"></a>

Various steps have already been taken to make concrete progress in the direction of building Institute, Learner and Teacher Registries. The following is a brief outline of different stages in the ideation and design process, the different discussions that have happened in this context, and the ou

* Establishing Registry usage precedents: The usage of large scale electronic Registries for a wide variety of use cases that deliver value to the citizens of the nation has been established by the implementation of systems such as PAN, Aadhaar, Vahan etc. - These are credible examples of registries with Open APIs for authentication and consented linkages.
* The [NDEAR](https://www.ndear.gov.in/policies-and-standards.html) report clearly calls out the need for learner, teacher, institute registries that are built in a federated and interoperable manner with Open APIs
* The [InDEA 2.0](https://www.meity.gov.in/writereaddata/files/InDEA%202\_0%20Report%20Draft%20V6%2024%20Jan%2022\_Rev.pdf) report from MeitY defines Registries and IDs, and lays out the principles for building electronic registries
* NDEAR Student Registry Committee discussions
  * Registry admin and policy working group (Note #6, File no. 1-45/2021-DIGED-Computer no. 3182345)
  * Registry Specifications Technology Working Group (Note #6, File no. 1-45/2021-DIGED-Computer no. 3182345)
* Working Group consultations and deliberations
  * WCD, MSDE, UIDAI, MeitY, States
  * Draft design and specs for Registries discussed
  * Teacher Registry PoC conducted by NIC in KV, JNV - Delhi (July 2021)
* Identification of core applications for Phase 1 and Phase 2
  * Reference - page 6, note #10
* Employing the PPP-R framework to arrive at the principles and the approach for Registry design - as laid out in the ‘Registry guardrails - Principles framework’ document. This was used to derive the principles based on which Registries that deliver value to the end users can be developed.

### &#x20;<a href="#id-3yc6uky03q6" id="id-3yc6uky03q6"></a>

### Institute, Learner and Teacher - Registry Use Cases: <a href="#x23eodf5b2kl" id="x23eodf5b2kl"></a>

Listed below are few of the initial envisioned use cases for federated interoperable registries in the education and skilling ecosystem across school, higher education and skilling domains in the country.

#### Visibility to progress & enabling targeted decision-making <a href="#id-4f0vjzo0ypb9" id="id-4f0vjzo0ypb9"></a>

Para 3.3 of NEP 2020 requires achievement of “universal participation in school by

carefully tracking students, as well as their learning levels, in order to ensure that they (a)

are enrolled in and attending school and (b) have suitable opportunities to catch up and re-enter school in case they have fallen behind or dropped out.” The federated registries will be used to help map and facilitate the entire journey of a learner spanning across different stages of scholarly life. It will ensure that the education credentials for a learner can be issued to the correct individual, they are in the control of the student/ parent, and can be shared/ used using consented access. It will enable a learning and credentials profile of the learners and will help the teachers to craft a learning journey for their students. The data analytics services enabled through Vidya Samiksha Kendra (VSK) will also allow the teachers as well the administrators to track the achievement of Learning Outcomes (LOs) and drive interventions accordingly in order to achieve the same (Ref. Case Study-E., Chapter-3, Part-A of NDEAR Report)

Easy access to Education & Skilling credentials for beneficiaries

Leveraging & using education & skilling credentials is required by the beneficiary to ease access to various benefits, schemes and also for transfers & admissions. Federated Registries with appropriate verifiable digital credentials will enable this. Unified Learner’s Passport (ULP) allowing them to have visibility & use of their credentials including their Academic Bank of Credits (ABCs) will enable this for each learner, updated against her unique identity throughout her learning journey in a verifiable manner, easily accessible by the ecosystem.

#### Transfers and Migration <a href="#u78pq5n31aho" id="u78pq5n31aho"></a>

Students have multiple entry and exit points in the academic journey. They also undergo transfer and migration from one location to another - both intra-state and inter-state. This requires finding a school in the new location, getting all necessary paperwork from the old school, giving it to the new school, finding financial support, exploring additional skilling opportunities etc. All these, while parents and students settle into the new place. A dynamic and federated registry at all administrative levels will help ease out the entire process for students, parents and administration. Digital records and credentials will enable access to the academic credits obtained by students, grade level competency achieved by the students, transfer and migration certificate records from previous institutions etc. across systems in a trusted fashion, erasing the need for any cumbersome, expensive and time-consuming paperwork (Ref. Case Study-B., Chapter-3, Part-A of NDEAR Report)

#### Admissions leveraging verifiable Credentials <a href="#id-1xc2dvmozg0u" id="id-1xc2dvmozg0u"></a>

Students get admission in School / higher education institutes which require them to produce all necessary documents for verification. Institutes encounter students who submit false academic records & achievements. Verification delays the time for admitting students and starting the academic year. Furthermore, students and parents find it difficult to arrange, attest and submit all the documents as hard copy and is often time consuming. With a Registry, the higher education institute can digitally verify trusted academic credentials till date, after consent, to proceed with the document verification process.

Scholarships & Benefits

Based on the demographic details and academic performance of a student, students are eligible for merit scholarships by the government or any other civil society organizations. It becomes difficult for administrators to track potential beneficiaries. Also, the beneficiaries have to ensure safekeeping of the credentials earned over the lifetime. A Registry can enable Centre, States/UTs, Boards, and ecosystem partners to provide benefits for teachers and learners in a trustworthy fashion, based on verifiable credentials that are produced by claimants. Registries at various administrative levels can provide a holistic view of benefits available versus benefits actually claimed by the end beneficiary and will enable administrators to design targeted interventions and also help plug the gaps, if any.

### &#x20;<a href="#ojbmh948iqsj" id="ojbmh948iqsj"></a>

### NIC - Education Institute Registry <a href="#id-2bdh7khhhn5j" id="id-2bdh7khhhn5j"></a>

NIC has carried out significant development work in the effort towards creation of national Registries in the education domain. One such key initiative is the Education Institute Registry, envisioned as a PoC for a master Registry of institutions across the nation. This has been developed taking into account the key Registry principles, and is meant to set an example of a federated and interoperable model for any entity that considers creation of a Registry of its Institutes (State Boards, CBSE or ICSE boards, Skilling Dept. etc.)

Version 1.0 of the system, which can be accessed at [https://institutes.ndear.gov.in/#/home](https://institutes.ndear.gov.in/#/home) showcases how various federated registries hosted by different entities such as CBSE, State boards etc. can be unified to provide an aggregated, national view for administrators.

![](<../../../.gitbook/assets/0 (2).png>)

* The Institute Registry employs data from existing institute systems - such as UDISE, various state boards, CBSE etc. to ensure reuse of existing data and systems. The Institute Registry will be populated in a federated manner, driven by the trusted data that is already available in such existing Registries. This is in line with the recommendation of Federated Registries in chapter 4.2.5, page 32 of [InDEA 2.0](https://www.meity.gov.in/writereaddata/files/InDEA%202\_0%20Report%20Draft%20V6%2024%20Jan%2022\_Rev.pdf)
* The system generates a unique ID for institute entries into the Registry (PIE - Premier Institute Identifier for Education), which can become the Digital Identifier for the entity within the system. This identifier could be used for system to system interactions, and users need not remember such system specific IDs. Usage can be simplified by allowing for linking of existing common Digital IDs that are in use (Aadhaar, PAN, GSTN, for example) to the Registry records, and allowing users to retrieve their data using the common linked IDs. Login into Registry systems can also be simplified using common authentication systems such as SSO or login with Digilocker. (Ref:[ InDEA 2.0](https://www.meity.gov.in/writereaddata/files/InDEA%202\_0%20Report%20Draft%20V6%2024%20Jan%2022\_Rev.pdf), chapter 4.2.4, page 31 & 32)
* Any system that has a need to leverage master institute data from the Education Institute Registry can do so using Open APIs in a trusted, easy and secure fashion - making the data available for a plethora of different use cases

### Implementing Federated NDEAR Registries to enable Benefits <a href="#yphy2lsnf6qp" id="yphy2lsnf6qp"></a>

Leveraging Federated Registries alongside existing and familiar digital systems such as Digilocker and Reporting systems such as VSK/ UDISE

* Simplify on-boarding for users by leveraging existing digital systems that are in use.
* Ensure users do not have to remember multiple IDs, and can use commonly used national IDs and infrastructure to access details and get a unified view.
* explore and explode the power of trusted, verified and reliable data.

![](<../../../.gitbook/assets/1 (1) (1).png>)

Federated Registries that are Issuers on Digilocker - thereby allowing users the convenience of leveraging their existing Digilocker accounts to get a unified view of all their credentials from one location. (Edu locker)

![](../../../.gitbook/assets/2.png)

![](../../../.gitbook/assets/3.png)

Employ existing and familiar digital IDs (national IDs) for onboarding users onto, as well as usage of Registries - offering 1-click enrolment and sign in for end users.

![](../../../.gitbook/assets/4.png)

Visualizing Actors & Actions

![](../../../.gitbook/assets/5.png)
