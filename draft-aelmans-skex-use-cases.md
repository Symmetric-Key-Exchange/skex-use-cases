---
title: "Symmetric Key Exchange Use Cases"
abbrev: "TODO - Abbreviation"
category: info

docname: draft-todo-aelmans-use-cases-latest
submissiontype: IETF
number: 00
date:
consensus: true
v: 3
# area: SEC
# workgroup: SKEX
keyword:
 - symmetric key establishment
 - key distribution
 - quantum safe

venue:
#  group: WG
#  type: Working Group
#  mail: skex@ietf.org
#  arch: https://example.com/WG
  github: "Symmetric-Key-Exchange/skex-use-cases"
  latest: "https://Symmetric-Key-Exchange.github.io/skex-use-cases/draft-todo-aelmans-use-cases.html"

author:
 -
    fullname: Melchior Aelmans
    organization: Juniper Networks
    email: melchior@juniper.net

normative:

informative:


--- abstract

Symmetric key distribution mechanisms have the potential to improve widely used security protocols by supplementing them with additional, out of band, key material, thus making these protocols quantum safe. This document provides an overview of some applications that are expected to benefit from additional key material and categorizes them. Some general requirements for the symmetric key distribution mechanisms are also described.


--- middle

# Introduction

Introduction
The development of new standards are aimed at harmonizing architectures, designs and implementations in an area of focus.  The quantum threat has catalyzed an appetite for symmetric keys in communication.
IETF documents that describe consumption of pre-shared keys (PSKs) include:
 - RFC 8696: Using Pre-Shared Key (PSK) in the Cryptographic Message Syntax (CMS)
 - RFC 8784: Mixing Pre-Shared Keys in the Internet Key Exchange Protocol Version 2 (IKEv2) for Post-quantum Security
 - RFC 9257: Guidance for External Pre-Shared Key (PSK) Usage in TLS
    RFC 9258: Importing External Pre-Shared Keys (PSKs) for TLS 1.3

Other aspects of PSK use and communication occur in:
 - WireGuard®
 - ETSI GS QKD 014
 - ETSI GS QKD 020 (a draft at this time)

This document motivates the need for providing key establishment standards by listing expected common use cases that will benefit from standardization.


# Conventions and Definitions

{::boilerplate bcp14-tagged}


# Security Considerations

TODO Security


# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.

# Use Cases

There are existing and potential future use cases that will benefit from symmetric key establishment:
 - **Existing cryptographic management protocols with defined dependence on PSK**: This group of cases, which includes CMS, IKE and IKEv2, may be described as having cryptographic security management at its core, but where the context demands quantum safety as a security property of these protocols. These relate also to communication use cases (IPsec, etc., below).
 - **Existing internet protocols with defined dependence on PSK for general-purpose client–server connections**: This group of cases, which includes TLS 1.2, TLS 1.3, DTLS 1.3 and QUIC, all provide the possibility of accepting a PSK input for the purpose of quantum safety, or in some cases, with the possibility for replacing asymmetric key establishment. The ability to update the PSK during an active session must be considered for these use cases.  These use cases are diverse, and include websites, VPNs and more.
  - **IPsec connections**: This is a general-purpose secure protocol with a defined dependence on a PSK input.  These connections can be dedicated high-volume connections, including point-to-point dedicated connections, VPNs and more. The ability to replace PSKs regularly throughout a session is essential to achieve the quantum-safe security requirement.
 - **MACsec connections**: This is a low-level secure protocol that uses symmetric keys that must be shared.  A means of establishing and synchronising session keys is necessary.
 - **Zero-trust architecture (ZTA)**: Applications must establish end-to-end security in this architecture.  This implies the establishment of end-to-end keys, with no intermediary (such a key management system) having access to these keys.  This includes applications such as secure email, messaging applications, and the like, including between mobile platforms.  Quantum safety requirements in a ZTA demand a symmetric key establishment method in addition to the asymmetric key exchange algorithms.
 - **Internet of Things (IoT)**: This use case is often characterized by the need for lightweight cryptography.  IoT connections include device-to-device and device-to-hub/server.  Symmetric key establishment that does not rely on asymmetric cryptography may be well-suited to such use cases.
 - **Quantum Key Distribution (QKD) authentication**: QKD links require securely established keys for endpoint authentication. 
 - **QKD alternative or extension**: QKD itself is an example of a key establishment protocol. The rate–distance tradeoff limitation of QKD has the effect that many locations are too remote to be bridged by QKD links, or that multiple links must be cascaded by means of intermediary trusted nodes.  QKD’s physical infrastructure requirements, immaturity and cost can also prove prohibitive.  Other key establishment protocols may also be used to bridge nodes in such a network.
 - **Replacing existing manual and physical key distribution mechanisms**: Diverse systems need manual key distribution, including for pre-placed keys.  A suitably key establishment system has the potential of replacing and consolidating such systems, with significant potential logistical, security and operational benefits.  Examples include military systems and the like.
 - **Key establishment with limited trust**: systems of communicating organizations that must be symmetric in their control or are even not mutually fully trusted could be covered as a use case under the general umbrella of symmetric key establishment.  Examples might include peer companies or even countries in loose communication networks. 

# Security Properties for Use Cases

In considering use cases, each case might require several security properties.  Here are several such properties that may be relevant to any given uses, and relate to security properties of the keying system:
 - **Identity assurance**: The identity of the remote communicating partner is assured based on some trusted premise.
 - **Authenticity**: Only the purported sender can generate a message that will be accepted by the receivers as being from that sender.
 - **Integrity**/**non-malleability**: The receivers will reject any message that is altered from what was generated by the sender.
 - **Confidentiality**/**secrecy**: Only the intended recipients can obtain information about the content of communication (often relaxed to allow leakage of metadata such as source, destination, message length, and timing of the communication).
 - **End-to-end security**: Absolute trust in intermediaries is not required for assuring the required security properties.
 - **Perfect forward secrecy (PFS)**: Compromise of any session key does not compromise any other session key.
 - **Information-theoretic security**: An adversary with unbounded computational resources (either classical or quantum) and unlimited access to communication channels has no advantage in compromising the correctness and confidentiality security properties.
 - **Communication robustness**: Compromise of elements of the communication infrastructure have little or no impact on the reliability of communication.
 - **Replay resistance**: A receiver can identify when a message is not 'fresh'.
 - **Timestamping**: A receiver can securely determine a window in which the message was generated by the sender.

