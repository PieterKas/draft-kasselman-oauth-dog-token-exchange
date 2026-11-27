---
title: "Delegated Operation Grant Issuance using Token Exchange and Workload Authorization Grants"
abbrev: "DOG Issuance via Token Exchange"
category: std

docname: draft-kasselman-oauth-dog-token-exchange-latest
submissiontype: IETF
number:
date:
consensus: true
v: 3
area: "Security"
workgroup: "Web Authorization Protocol"
keyword:
 - OAuth
 - delegated operation grant
 - token exchange
 - workload
 - agent
venue:
  group: "Web Authorization Protocol"
  type: "Working Group"
  mail: "oauth@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/oauth/"
  github: "PieterKas/draft-kasselman-oauth-dog-token-exchange"
  latest: "https://PieterKas.github.io/draft-kasselman-oauth-dog-token-exchange/draft-kasselman-oauth-dog-token-exchange.html"

author:
 -
    fullname: Pieter Kasselman
    organization: Defakto Security

normative:
  RFC6749:
  RFC8693:
  RFC7523:
  DOG:
    title: "OAuth 2.0 Delegated Operation Grant"
    author:
      -
        fullname: Nick Steele
    date: 2026-11-24
    target: https://nicksteele-oai.github.io/ietf-drafts/delegated-operation-grant/
  I-D.ietf-oauth-deferred-token-response:
  I-D.carleton-workload-authz-grant:

informative:
  I-D.ietf-oauth-identity-assertion-authz-grant:
  I-D.rosomakho-oauth-txn-challenge:
  RFC9449:

--- abstract

The OAuth 2.0 Delegated Operation Grant (DOG) is a JSON Web Token (JWT) authorization grant that authorizes specific operations at a protected resource. An intermediary, such as a platform or credential manager, holds the DOG and does not disclose it to the workload or agent that performs the operations. This document specifies how the intermediary obtains, presents, and uses a DOG on behalf of a workload or agent that acts either on its own behalf or on behalf of a user. The intermediary can exchange the DOG for an OAuth access token or present it directly to a resource server that is not protected by an OAuth authorization server.

--- middle

# Introduction {#intro}

TODO The problem in one paragraph, what {{DOG}} specifies and what it
leaves to deployments, and the claim that existing building blocks
({{RFC8693}}, {{I-D.carleton-workload-authz-grant}},
{{I-D.ietf-oauth-deferred-token-response}}) fill those gaps without
changing the DOG itself.

# Introduction {#intro}

The OAuth 2.0 Delegated Operation Grant (DOG) {{DOG}} is a JWT used as an
authorization grant, as described in {{Section 2.1 of RFC7523}}. An
intermediary, such as a platform or credential manager, holds the DOG and
uses it to obtain access for a workload or agent that runs in a less
trusted environment. The workload or agent performs the authorized
operations but never receives the DOG itself.

This document defines:

* The DOG format: A DOG is a signed JWT with the `typ` header value `oauth-dog+jwt`. It names one resource authorization server (`aud`) and one protected resource (`resource`), lists the authorized operations (`scope`), and binds the grant to a key (`cnf`).

* Requesting a DOG: The intermediary requests a DOG using OAuth 2.0 Token Exchange {{RFC8693}}. It presents a Workload Authorization Grant (WAG) {{I-D.carleton-workload-authz-grant}} that identifies the workload or agent. When the workload or agent acts on behalf of a user, the request also includes a subject token that identifies the user.

* User Interaction: When the authorization server requires user interaction, it uses a Deferred Token Response {{I-D.ietf-oauth-deferred-token-response}}. The user authenticates and consents at an interaction URI while the intermediary polls for the result. When no interaction is required, the authorization server issues the DOG immediately.

* DOG Presentation: The intermediary presents the DOG to a resource authorization server as a JWT authorization grant {{RFC7523}} and receives an access token. It can also present the DOG directly to a resource server that is not protected by an OAuth authorization server, which returns a session cookie.

* Access Credential Use: The intermediary delivers the resulting access token or cookie to the workload or agent, or injects it into the requests that the workload or agent makes.

# Conventions and Definitions

{::boilerplate bcp14-tagged}

TODO Terms: agent, platform, issuing authorization server, resource
authorization server, web server. Agent = workload, runs on the platform.


# Overview {#overview}

TODO One sequence diagram covering both the immediate and the deferred
(interactive) paths, followed by a numbered walk-through.


# Requesting a DOG {#request}

TODO Token exchange request parameters: subject_token (ID token or refresh
token identifying the user), how the WAG is presented (open: actor_token?),
requested_token_type, resource/audience (single-valued), operations, and
the completion_mode opt-in.

Open: token type identifier for a DOG; proof-of-possession key and how it
becomes the DOG's cnf.


# User Consent using a Deferred Token Response {#consent}

TODO Profile the interaction_uri semantics: user authentication, consent to
specific operations, polling for completion. Issuance without interaction
when policy allows.


# Token Exchange Response {#response}

TODO The DOG returned in access_token with token_type N_A and the
issued_token_type, immediately or after polling.


# Using the DOG {#use}

## At a Resource Authorization Server {#use-as}

TODO The platform obtains an access token on the agent's behalf and
delivers it to, or injects it for, the agent.

## At a Web Server {#use-web}

TODO Direct presentation of the DOG to a web server that returns a cookie.
Open: request format.


# Relationship to the Delegated Operation Grant {#relationship}

TODO Condensed comparison with {{DOG}}: what is the same, what this
profile supplies, and where the mechanisms differ.


# Security Considerations {#security}

TODO Security


# Privacy Considerations {#privacy}

TODO Privacy


# IANA Considerations {#iana}

TODO Possibly a token type URI for a DOG.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
