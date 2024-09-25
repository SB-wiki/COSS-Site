---
icon: elementor
---

# What is a registry

### Objective <a href="#m47rqi3ejc9l" id="m47rqi3ejc9l"></a>

This document discusses what a registry is and is not. This document articulates the idea of a registry and explains to the readers some fundamental characteristics.

### Concept <a href="#id-2uu7qindfhos" id="id-2uu7qindfhos"></a>

Ledgers and spreadsheets of master data always existed in some form. These were updated for record keeping purposes and were available only at the hands of the administrator. Then they were made viewable to users via web portals. Even then, these were still closed to edits and programmatic access for inter-department consumptions. When a need arose, a copy was taken and the data was duplicated. What we are about to discuss is the Type 4 of this evolution.

![](<../../../.gitbook/assets/0 (1) (1).png>)

Until Type-3, it was the ‘closed’ access and ‘control’ that prevented these data from being ‘up-to-date’. After a while, these data became outdated, losing credibility. Once the truth got lost, the usage of such data was lost along, simply because there was no ‘good’ data to verify or there were doubts lingering about its credibility.

Welcome to Type-4 world. We define Registry as a store-house of data that is true and verifiable. This also implies that it is constantly updateable, leading to a currency of data. These three characteristics - true, verifiable and current - make the registry an attractive go to system for _those specific_ facts. Thus, it also follows that a registry will have to host very focussed and essential data attributes only.

Each of these characteristics can be stated either expressly or can be derived from the mere presence of the record itself. For example, the mere presence of a citizen in the Aadhaar means that he is an Indian resident citizen. An entry in the PIN CODE in India means that it is a valid location and has a well-defined geographical boundary limit. The name of the citizen or an address of the citizen in Aadhaar could be a little out-dated (for a brief period sometimes). The registry makes it possible for users to constantly access, request change and get it ‘verified/approved/validated’ and thereby make it current again. Until it's verified, the other readers also can learn that this is an ‘unverified’ data point. It is this power of transparency through programmatic access that we like to appreciate in a registry.

### What is a registry? <a href="#ykjrjt2t4oo2" id="ykjrjt2t4oo2"></a>

A registry is a datastore of highly usable master data, that is always maintained due to active usage. The master data is true and verifiable.

A registry is generally realized using a database. The converse isn’t true. To state in other words, a) not all databases become a registry and b) registry is not just a database.

[![](<../../../.gitbook/assets/1 (1).png>)](https://www.draw.io/?page-id=E1IasIYdq2JkT9DUw1qI\&scale=auto#G1v8cZNkKmXRfrN8yHOGKbYk2PB0UX862l)

A registry is a datastore of irrefutable master data. Conceptually, there can be no two registries claiming they are the owners of the ‘same’ master data. There could only be a federation of such registries.

Finally, a registry is a concept of building and realizing real-world objects or domain models. This doesn’t refer to a product or a solution by itself. Registry can be realized using an archetype we built like [OpenSABER](https://github.com/project-sunbird/open-saber).

### Characteristics of a registry <a href="#vutufk3z1gr6" id="vutufk3z1gr6"></a>

#### Key characteristics <a href="#os02icrno342" id="os02icrno342"></a>

* Can be accessed via APIs
* Provides views construct for relevant use
* Master datastore of a well-defined schematic entity
* Regularly accessed and is available for all actors (with controls that apply)
* Verifiable information

#### What is not a registry? <a href="#whfji5z2qbvj" id="whfji5z2qbvj"></a>

An application, either website or a general purpose app is built using rigid schema.

### Registry ecosystem <a href="#p8kzmi781qyz" id="p8kzmi781qyz"></a>

The following diagram reflects our thinking on a registry system. Note that each registry has only a link to another unique identifier in the system. Whenever one registry needs information from the other, it just pulls the information and doesn’t necessarily store it (_Note: caches may be allowed for performance reasons, but that’s more towards solutioning. We discuss the architectural concept here)_.

Each registry is an irrefutable holder of certain master data.

![](../../../.gitbook/assets/2.jpeg)

#### Master data vs Mirror data <a href="#rxyqwly2q1jb" id="rxyqwly2q1jb"></a>

#### Actors in a registry <a href="#id-4dngix57b44i" id="id-4dngix57b44i"></a>

* Owner - the owner of the data.
* Custodian - the entity/person hosting the data.
* Admin - the person appointed by a custodian authorized to maintain and run the registry.
* Approver - the person who approves the ‘data’.
* Attestor - can ‘certify’ or vouch for the credibility of the data, usually after verification of data.

#### Custodian vs ownership <a href="#m6cratg2dsfy" id="m6cratg2dsfy"></a>

Custodian is the person that is in-charge of _running or owns running_ the registry. As the name suggests, the person is a mere information collector and controlled distributor of the information collected.

Examples:

1. Social websites hosting personal profile information. So, it is a custodian.
2. UIDAI (one of India identity systems) holds resident Indian information. Therefore, it is a custodian.

Whereas, the owner is the person to whom the information belongs to or is about.

### Examples of some registry we know already <a href="#id-9tzfugc3u0hj" id="id-9tzfugc3u0hj"></a>

| **Name** | **Maintains**                                         |
| -------- | ----------------------------------------------------- |
| IANA     | List of ports and domains (1)                         |
| Aadhaar  | Indian residents information (\*)                     |
| Practo   | List of doctors, their area and specializations (\*). |
| Whois    | List of domains registered                            |

Note:

1. API not available, but is a listing

(\*) These are **not** complete listings of **ALL** Indian citizens or doctors, but are verified / true data.
