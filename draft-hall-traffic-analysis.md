---
title: "Traffic Analysis: Threats and Mitigations"
abbrev: Traffic Analysis
docname: draft-hall-traffic-analysis-latest
category: info
ipr: trust200902

stand_alone: yes

author:
 -
    ins: J. Hall
    name: Joe Hall
    org: CDT
    email: joe@cdt.org
 -
    ins: M. Thomson
    name: Martin Thomson
    org: Mozilla
    email: martin.thomson@gmail.com

normative:

informative:

--- abstract

Traffic analysis is the practice of using secondary information exposed by
network traffic to recover information that would otherwise be confidential.
This document discusses the various techniques that are used for traffic
analysis.  A general framework for protecting information against recovery via
traffic analysis is offered.


--- middle

# Introduction

Traffic analysis is the practice of assembing and analysing information leakage
- or side-channels - from confidential communications.  Implementations of many
common protocols reveal small amounts of information, often inadvertently, as
part of their operation.  Traffic analysis observes encrypted communications and
uses leaked information to learn things about either the communication session
or the participants in that session.

These side-channels can be used in various ways to extract information.
Analysis might be performed on an individual communications session, or on
communications in the aggregate.  Often, traffic analysis techniques are
stochastic in nature, producing probabilistic results rather than a specific
plaintext.

Traffic analysis don't rely on cryptanalysis or the breaking of the
cryptographic algorithms or protocols that are in use.  Rather, they concentrate
on what the cryptography fails to protect, extracting as much information as
possible.  Notably, recent research in the area shows that some information can
be extracted with a high degree of accuracy.

For example, the traffic analysis performed in
{{?CLINIC=DOI.10.1007/978-3-319-08506-7_8}} used the size and relative position
in time of encrypted HTTPS exchanges to recover information on what pages were
being requested.

This document doesn't intend to examine the reasons that traffic analysis is
employed.  Instead it aims to offer an overview of the techniques that can be
employed and to offer ways in which those techniques can be countered.  Each of
these mitigations outline whether changes to protocols are needed to facilitate
them and - where possible - reference documents that describe best practices for
their use.

Furthermore, this document doesn't aim to address specific flaws, either in
protocols or implementations that might make traffic analysis more effective.
Instead, the hope is that this document might raise awareness of the sorts of
considerations that affect traffic analysis and thereby reduce the incidence of
such problems.

The reader is advised to consult RFC 2804 {{?RAVEN=RFC2804}} for a discussion of
protocol mechanisms that facilitate the extraction of information without
knowledge of communications peers.


# Traffic Analysis Techniques

## Size

The overall length of packets, or sequences of encrypted packets can reveal
information about the length of the cleartext.

For instance, prior to the addition of padding in TLS 1.3
{{?TLS13=I-D.ietf-tls-tls13}}, records in the TLS protocol included between 1
and 256 octets of padding, but only if block ciphers were used.  The more modern
AEAD algorithms {{?AEAD=RFC5116}} reveal the length of plaintext precisely.



## Duration and Timing

Discuss real-time protocols vs. streaming vs. bulk transfer protocols.  Cite I
know why you went to the clinic and the netflix thing.

Discuss the timing of responses in relation to their requests.


## Session Correlation

Discuss linkage of sessions and the information that can reveal.

Discuss fingerprinting, {{?PANOPTICLICK=DOI.10.1007/978-3-642-14527-8_1}},
etc...


## Headers from Unprotected Protocols

End-to-end confidentiality protection is often added at higher layers of the
protocol stack.  Some of the information exposed at lower layers of the stack
are necessary for the correct operation of that layer.  For instance, the IP
address is a valuable source of information about the identity of communicating
endpoints, but it is also necessary in ensuring that packets arrive at their
intended destination.

### Link Layers

Ask Juan Carlos to provide a brief summary of the IEEE fingerprinting

### The IP Header

Ask Fernando to help out regarding draft-gont-predictable-numeric-ids

### Transport Protocols

Ideally find a citation here for TCP.

### The DNS

DNS is still (alas) largely in the clear.

### The TLS Handshake

Cite McGrew on profiling TLS handshakes {{?MALWARE=DOI.10.1145/2996758.2996768}}.

Talk about SNI {{?RFC6066}}.

Talk about ALPN {{?RFC7301}}.


# Mitigations

## Padding

TLS 1.3 does this, but no earlier versions.  Higher layer protocols might add their own.

Find out state of play regarding IPsec.

## Send Rate Modifications

## Mixnets

Talk about TOR (note also that TOR does some of the other things too)

## Moar Encryption

Cite DPRIVE for DNS, QUIC for transport, IPsec


# IANA Considerations {#iana}

\[\[RFC EDITOR: please remove this section before publication.]]
This document makes no request of IANA.

# Security Considerations {#security}

This entire document is a discussion of the security considerations of traffic
analysis.

--- back
