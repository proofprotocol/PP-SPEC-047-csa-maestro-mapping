# PP-SPEC-047: Proof of Efficacy Mapping to CSA MAESTRO

| Field | Value |
|---|---|
| Status | DRAFT v0.1 |
| Author | Craig Ellrod, Nebulonium, Inc. (dba HACKERverse®) |
| Date | October 8, 2026 |
| License | CC BY 4.0 |
| Maps to | Cloud Security Alliance MAESTRO (Multi-Agent Environment, Security, Threat, Risk, and Outcome) |
| Series | Proof Protocol Framework Mapping Specifications |

---

## 1. Purpose

This specification defines how threat context produced with MAESTRO (Multi-Agent Environment, Security, Threat, Risk, and Outcome), the agentic AI threat modeling framework published by the Cloud Security Alliance (CSA), can be bound to Proof Protocol test cases, evidence, and efficacy results.

MAESTRO remains authoritative for its own layers, terminology, and threat modeling method. This document defines a **Proof Protocol mapping** and does not supersede or modify MAESTRO.

## 2. Scope

MAESTRO was introduced by CSA in February 2025 (author: Ken Huang) as a layered threat modeling approach for agentic AI systems. It organizes analysis across seven layers, from Layer 1 (Foundation Models) through Layer 7 (Agent Ecosystem), with Security and Compliance treated as a vertical layer, and it considers threats that span or chain across layers. MAESTRO is not published with a version number; as of October 2026 CSA describes it as actively evolving based on implementer feedback, and CSA hosts a MAESTRO landing page and a MAESTRO Threat Analyzer tool repository.

MAESTRO supplies agentic AI threat context that can identify what should be exercised. Proof Protocol supplies an independent evidence model for determining what happened during a test and whether a selected defensive control performed as claimed.

Independent witnessing and evidence-capture implementation are defined elsewhere in the Proof Protocol specification family.

## 3. Core Question

Proof of efficacy asks:

> **Was there a control, and did it work?**

A MAESTRO threat model identifies threats at a layer, or threats that propagate across layers. A product, architecture, policy, or safeguard may claim to mitigate those threats. Proof Protocol binds the MAESTRO layer and threat context, adversarial test, control, observed behavior, downstream outcome, and evidence into a result that can be independently examined.

## 4. Metric Definitions

Against a defined adversarial corpus, each case is recorded as **blocked**, **detected**, **missed**, or **INVALID**.

Relevant measurements include:

- containment rate;
- detection rate;
- miss rate;
- false-positive rate against paired benign cases;
- robustness against manipulation, bypass, escalation, poisoning, tool misuse, identity abuse, memory abuse, cross-layer propagation, or other applicable agentic attack variants;
- version-level results; and
- INVALID status when required evidence is incomplete or broken.

Target levels are engagement- and risk-specific rather than imposed by this mapping.

## 5. Evidence Produced

Mapped tests can produce:

- **Proof records** binding MAESTRO layer and threat context, test case, control, system/version, verdict, timestamp, and evidence references;
- **ProofStamp™** trusted timestamps bound to evidence/verdict objects;
- **ProofBundle™** packages containing proof records, metrics, corpus manifests, and environment/context;
- **ProofRegister™** records for issued proof artifacts; and
- corpus and environment manifests identifying the tested agentic conditions.

## 6. Mapping to CSA MAESTRO

MAESTRO layer names and any threat identifiers SHOULD be taken from the authoritative CSA source being used and recorded in the ProofBundle™ together with the date or revision of that source, because MAESTRO does not carry a formal version number. This specification does not redefine MAESTRO layers or threats.

| MAESTRO context | Proof Protocol treatment | Evidence |
|---|---|---|
| Layer (Layer 1 to Layer 7) | Record the MAESTRO layer where the threat originates or is exercised as test context. | Corpus/test metadata |
| Vertical layer (Security and Compliance) | Record the asserted security or compliance control separately from its observed effect. | Control descriptor |
| Layer-specific threat | Represent the threat as one or more reproducible, independently authored test cases. | Proof record; corpus manifest |
| Cross-layer threat chain | Exercise the full chain across the affected layers and record each hop where observable. | Execution evidence per layer |
| Threat model scope (system, agents, components) | Bind the tested system boundary, agents, tools, and data flows named in the threat model. | Environment descriptor |
| Mitigation or control claim | Record the asserted prevention, detection, or response behavior separately from observed effect. | Control descriptor |
| Agent action and tool use | Capture what the agent attempted and which actions or tools were invoked. | Execution evidence |
| Detection outcome | Record whether the control identified the exercised condition. | Detection result |
| Prevention/containment outcome | Determine whether the adversarial objective reached the protected target or caused the prohibited action. | Target/outcome evidence |
| Evaluation and observability signals (Layer 5) | Treat telemetry as evidence inputs only; telemetry alone does not establish efficacy. | SIEM/log evidence |
| Risk and outcome assessment | Keep the MAESTRO risk rating as context; the Proof Protocol verdict is determined from evidence. | Proof record |
| System/version context | Bind material agent, model, framework, policy, tool, control, and environment versions to the result. | Environment descriptor |

## 7. Interoperability Rules

1. The MAESTRO layer, threat, and source reference (URL and date or revision) SHOULD be recorded when applicable.
2. MAESTRO identifiers, names, and terminology MUST NOT be silently redefined.
3. Proof Protocol verdicts are Proof Protocol results; they are not Cloud Security Alliance scores, certifications, or endorsements.
4. A control's presence, configuration, activation, and efficacy are distinct facts.
5. A policy decision, alert, or control trigger does not by itself establish efficacy when the claim concerns a downstream protected outcome.
6. Target, application, tool, SIEM, vendor, or equivalent evidence SHOULD complete the evidence round trip when required to establish the result.
7. Missing required evidence MUST yield **INVALID**, not PASS.
8. Material changes to the tested system, model, policy, tools, permissions, control, environment, MAESTRO mapping, or corpus SHOULD trigger retesting where they can affect the result.
9. A MAESTRO risk or likelihood assessment is threat model context; it MUST NOT be reported as a Proof Protocol efficacy result.

## 8. Framework-Agnostic Architecture

> **Threat frameworks are pluggable inputs to Proof Protocol. Proof Protocol is framework-agnostic.**

External frameworks can identify **what to test**: threats, vulnerabilities, techniques, risk categories, controls, design assertions, identity claims, tool permissions, or other risk conditions. Proof Protocol independently establishes **whether the control worked and what evidence proves that result**.

No external framework is required for Proof Protocol to operate. A Proof Protocol implementation MAY use CSA MAESTRO, MITRE ATLAS, MITRE ATT&CK®, OWASP, AIVSS, AAGATE, a proprietary threat model, another recognized framework, or no external framework at all when the test condition is otherwise sufficiently defined.

Adding, replacing, muting, or removing a framework mapping does not alter the Proof Protocol architecture, evidence model, Proof of Efficacy determination, ProofBundle™, ProofStamp™, ProofRegister™, or independent corroboration requirements.

A framework mapping therefore establishes **interoperability**, not architectural dependency.

## 9. Relationship to Proof Protocol

This mapping is part of the Proof Protocol specification family maintained by Nebulonium, Inc.

The relationship is intentionally asymmetric:

> **CSA MAESTRO supplies layered agentic AI threat modeling context. Proof Protocol supplies the evidence model for determining whether a selected defensive control performed as claimed.**

No affiliation, endorsement, certification, or sponsorship by the Cloud Security Alliance is implied.

## 10. Source Framework, Attribution, and License

MAESTRO is external work published by the Cloud Security Alliance. CSA names, MAESTRO names, layer names, trademarks, and expressive framework content remain subject to CSA's applicable terms.

The primary MAESTRO source is a CSA blog article by Ken Huang published February 6, 2025 (https://cloudsecurityalliance.org/blog/2025/02/06/agentic-ai-threat-modeling-framework-maestro). That page carries the site-wide notice "© 2009–2026 Cloud Security Alliance. All rights reserved." and states no separate open license for the framework text. CSA's Website Terms and Conditions (https://cloudsecurityalliance.org/legal/website-terms-and-conditions) permit use of site Material for education and understanding, require retention of copyright, trademark, and other proprietary notices, and restrict commercial copying, modification, or creation of derivative works of Material without an appropriate license from CSA. CSA trademarks may not be used without CSA's express written permission except as those terms provide. CSA working group Publications may carry their own terms; any such terms SHOULD be checked at the authoritative source before reuse.

The CSA MAESTRO Threat Analyzer repository (github.com/CloudSecurityAlliance/MAESTRO) is distributed under the MIT License. That license covers the tool code, not the MAESTRO framework text. This specification does not use or incorporate that code.

This Proof Protocol mapping is independently authored and Licensed under the Greater Good Commercial License 1.0 (see LICENSE.md); text CC BY-ND 4.0 under its Part S. Original inventor: Craig Thomas Ellrod (ORCID 0009-0004-1058-7666).

### Required attribution

CSA does not publish a specific attribution string for referencing MAESTRO. The following recommended attribution is used:

> MAESTRO (Multi-Agent Environment, Security, Threat, Risk, and Outcome) is an agentic AI threat modeling framework published by the Cloud Security Alliance. Source: Ken Huang, Cloud Security Alliance, February 6, 2025, https://cloudsecurityalliance.org/blog/2025/02/06/agentic-ai-threat-modeling-framework-maestro. © 2009–2026 Cloud Security Alliance. All rights reserved.

This specification reproduces only the MAESTRO name, its acronym expansion, the layer numbers and layer names, and short factual statements about the framework. It does not reproduce, translate, or adapt MAESTRO descriptive text, threat lists, diagrams, or CSA Publications, and it does not use CSA logos or marks beyond nominative reference. Implementations that reproduce any CSA text MUST retain CSA's copyright and proprietary notices and comply with CSA's terms, including any terms attached to a specific CSA Publication.

## 11. Versioning

This mapping is versioned independently of MAESTRO. Because MAESTRO does not carry a formal version number, each ProofBundle™ SHOULD record the CSA source URL and its publication or revision date. Material upstream changes, including changes to layer structure or names, SHOULD trigger a mapping review and, where necessary, a new version identifying the MAESTRO source mapped.

---

*Proof Protocol · proofprotocol.io · CC BY 4.0*
