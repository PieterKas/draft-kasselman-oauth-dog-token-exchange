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

TODO Abstract. One paragraph: the Delegated Operation Grant (DOG) leaves
issuance, consent and delivery to the deployment; this document profiles
them using OAuth 2.0 Token Exchange, a Workload Authorization Grant (WAG)
that identifies the agent, and the Deferred Token Response for user consent.


--- middle

# Introduction {#intro}

TODO The problem in one paragraph, what {{DOG}} specifies and what it
leaves to deployments, and the claim that existing building blocks
({{RFC8693}}, {{I-D.carleton-workload-authz-grant}},
{{I-D.ietf-oauth-deferred-token-response}}) fill those gaps without
changing the DOG itself.


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
